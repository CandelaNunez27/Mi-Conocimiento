# Práctica: Arquitectura Cloud con Ingress Controller y Volumenes Persistentes
### Preparación

Estructura del proyecto:

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802185115.png)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802184831.png)

1. Asegurarse que el servicio docker este levantado
	 `systemctl status docker`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802185309.png)
	 

2. arrancar un minikube:
	 `minikube start` para arrancar el minikube default, default porque no se le coloco nombre
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802201425.png)
	
	 `minikube status` Se ve el estado running y que se llama minikube.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802201549.png)
	 
	 
	
	 `minikube addons list ` lista de agregados / plugins que tiene minikube y que se pueden utilizar que son de terceros. De esa  lista vamos a activar el ingress que es creado por kubernetes. Hay otros addons interesantes como ingress-dns creado por minikube, istio y inspecktor-gadget creado por 3rd party
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802201746.png)
	
	
	 
	 `minikube addons enable ingress` se vera enable en la lista
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802202311.png)![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802202653.png)
	 


3. En la carpeta docker
	 La carpeta docker tiene dos carpetas, una llamada backend y otra frontend.
	 `cd backend` nos movemos para la carpeta backend
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802185358.png)
	
	 `docker build -t courseipap/frontend:1.0.0 -f Dockerfile.backend --no-cache .` y nos vamos a la carpetas de frontend y tiramos `docker build -t courseipap/frontend:1.0.0 -f Dockerfile.frontend --no-cache .` se buildea las imagenes,  -f es para colocarle el nombre del archivo.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802191621.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802191343.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802191358.png)

4. Cargar imagenes a minikube:
	 `docker image ls |grep ipap` para ver las imagenes que ya tenemos creadas  en nuestra maquina, pero minikube todavia no los reconoce.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802191652.png)
	 
	 `minikube image load courseipap/backend:1.0.0` y `minikube image load courseipap/frontend:1.0.0` quedan cargadas las imagenes en minikube
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802203753.png)
	 
	 `minikube image ls` vemos si se cargaron correctamente
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803101610.png)
	 
	 


### Despliegue de arquitectura

1. Creamos el namespace:
	 Volvemos a la carpeta repaso que es la que contiene todo la actividad `cd ..`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802204328.png)
	 
	 `kubectl create namespace labipap` lo crearemos desde la consola ya que crear el archivo yaml como la clase pasada no es tan necesario ya que son muy poquitas lineas. `kubectl get ns`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803002740.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803002822.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803003045.png)Tenemos el archivo  postgres_deployment.yaml que tiene apiversion, kind Deployment, name postgres-db, spec containers volieMounts, secretkey que apunta al otro archivo db-secret-config.yaml. etc, con su servicio. luego un backend con su servicio, y por ultimo un frontend con su servicio
	 
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803003426.png)
	 Tenemos el archivo db-secret-config.yaml que tiene apiversion, kind Secret, name db-credentials, data usarname y passwoed en codificacion en bash64. Tambien tiene un Kind ConfigMap, name db-config, data db_name "mini_commerce"
	 

2. Deployment:
	 Ahora si empezamos a desplegarlo en nuestro namespace
	 `kubectl apply -n lapipap -f db-storage.yml` y `kubectl apply -n lapipap -f db-secret-config.yaml`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803003838.png)
	 
	 
	 `kubectl get all` o `kubectl get all -n labipap`no va a mostrar lo que creamos porque get all muestra más que nada servicios basicos, pods, etc
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803004042.png)
	 
	 `kubectl get secret -n labipap` aca si se mostrara el db-credentials
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803004201.png)
	 
	 `kubectl get cm -n labipap` mostrara el db-config y kube-root-ca.crt
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803004239.png)
	 
	 `kubectl get pv -n labipap` mostrara los volumenes presistentes
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803004355.png)
	 
	 Ahora seguimos desplegando con `kubectl -n labipap apply -f postgres-deployment.yaml`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803004831.png)
	 
	 Y ahora como ya lo desplego todo el deployment lo veremos en `kubectl get all -n labipap` aunque nos aparece el pod de backend ready 0, puede ser un problema de la imagen pero para mas info tiramos `kubectl -n labipap describe pod backend-7cd7d84568-wkx8q 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803005510.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803005953.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803010140.png)
	 
	 Buscamos el bloque de eventos, nos muestra el error con la imagen courseipap/backend:1.0.4. esa linea esta en el postgres-deployment.yaml en la parte del backend por ende lo cambiamos a courseipap/backend:1.0.0. 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803010528.png)
	 
	 Pero si tiramos `kubectl get pods -n labipap` nos sigue saliendo en ready 0. para eso se tiene que volver a ejecutar `kubectl -n labipap -f postgres-deployment.yaml` . Todo esto es para ver como se soluciona un error y siempre se suguiere que se haga un reinicio desde la mamusca mas grande en nuestro caso el deployment
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803010708.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803010857.png)
	 
	 ahora estara todo bien en `kubectl get all -n labipap` y en `kubectl -n labipap describe pod backend-5bd4db5b4-krsgv`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011115.png)
	
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011235.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011312.png)

### Generamos la rutas de conectividad segun el grafico de la aquitectura
 
 1. Probamos desde nuestra pc
	 `curl -v localhost` no nos muestra nada porque aun nos falta el ingress controler para que direccione todo.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011401.png)

2. Ingress (recurso de kubernetes):
	Tenemos el archivo app-ingress.yaml  
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011449.png)
	 
	 
	 `kubectl -n labipap apply -f app-ingress.yaml` para que se cree. y nuevamente `kubectl get all -n labipap ` no lo va a mostrar porque no es un recurso basico. para verlo usamos `kubectl get ingress -n labipap`  con eso ya tendriamos las rutas de comunicacion.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011549.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011605.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011652.png)
	 
	 
	 Tiramos nuevamente `curl -v localhost` pero falla nuevamente por estar usando minikube. para eso hacemos como la clase anterior un tunel en una nueva terminal.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011744.png)
	 
	 
	 `minikube tunnel` creara el tunel luego de pedirnos la contraseña de nuestra pc y nos quedara tomada la terminal.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803011927.png)
	 
	 nuevamente volvemos a `curl localhost` (en mi caso `curl 192.168.58.2`) y probamos en el navegador `http://localhost` (`http://192.168.58.2`) y. Ahora si nos anda los dos. 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803012840.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803102820.png)
	 
	 También probamos `curl localhost/api` nos sale un error pero medio engañoso, el api es un recurso que esta en nuestro ingress controler pero es algo de nuestro index.js que esta en nnuestra carpeta de docker > backend. si revisamoes ese index.js tiene atributos api/data por ende lo probamos, `curl localhos/api/data` este no nos devuelve nada.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803012928.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803102901.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803013115.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803013138.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803013005.png)
	 
	 Este error no es un error de kubernetes si no es un error un de la configuracion. lo encontramos en el app-ingress.yaml en annotations. un rewrite-target es para las consultas localhost/.... a kubernetes no le interesa lo que se coloque despues del / . para ello se cambia el archivo app-ingress.yaml a por el archivo app-ingress.yml donde se le saca el rewrite. En este nuevo si les coloca las posibilidades que hay si se le coloca cosas distintas luego de la /.  Esto es bueno para generar estos dos caminos que vemos en el grafico de la arquitectura.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803013238.png)
	 
	 Entonces para que funcione colocamos `kubectl -n labipap apply -f app-ingress.yml` y revisamos que siga corriendo el tunel
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803013321.png)
	 
	 Luego de volver a aplicar se vera que `curl localhost/api/data` (`curl 192.168.58.2/api/data`) nos muestra una base de datos vacia, pero una base de datos existente.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803013618.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803102949.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803103053.png)

### Compra del cliente, prueba de resiliencia y de persistencia

1. Escribir en la base de datos (compra ecomers)
	 Actualmente la base de datos esta vacia por ende con este comando le colocaremos una "compra" `curl -X POST http://localhost/api/data -H "Content-Type: application/json" -d '{"nombre": "Estudiante", "clase": "Kubernetes"}' ` (`curl -X POST http://192.168.58.2/api/data -H "Content-Type: application/json" -d '{"nombre": "Estudiante", "clase": "Kubernetes"}'`)  para ver que se guardo con éxito ejecutamos `curl localhost/api/data` (`curl 192.168.58.2/api/data`) y nos sale.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803104857.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803104948.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803105001.png)

2.  Resiliencia en vivo (gran ventaja de kubernetes que no es tan fácil con kubernetes):
	 Para ver como se logra la resiliencia en una terminal dejamos corriendo `while true; do curl -s http://localhost/api/data; echo ""; sleep 1; done` (`while true; do curl -s http://192.168.58.2/api/data; echo ""; sleep 1; done`) (`watch -n 1 curl -s http://192.168.58.2/api/data`) esto nos toma la consola para mostrar los resultados en vivo
	 
	 antes de borrarlo:![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803111350.png)
	 
	 luego de borrar el pod:![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803111145.png)
	 
	 Segundos después de haberlo borrado:![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803111205.png)
	 
	 
	 en otra terminal: `kubectl -n labipap get pod -w  ` esto nos toma la consola para quedar escuchando gracias al -w
	 todo el proceso de borrar, copiar y crear un nuevo pod para que siga funcionando:
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803111251.png)
	 
	 en otra terminal: `kubectl delete pod -l app=db -n labipap` se borrara un pod pero al instante volvera a crear otra (una replica) por ende la primera terminal  se cae mostrando error de conexion pero solo por 3 segundos (esto tardaria menos si no estubieramos en minikube sino en kubernetes). y se volvio a tener corriendo los 3 pod sin perder los datos de la base de  datos gracias a colocarle volumenes persistentes.
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803111223.png)
	 

3. Ultimas pruebas:
	 `kubectl apply -f pod-db_troubleshoost.yaml -n labipap` y `kubectl get po`creamos un pod  que solo tiene un pod con la imagen de alpine
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803111654.png)
	 
	 `kubectl -n labipap exec -it db-troubleshooter -- psql -h db -U postgres -d mini_commerce` dentro de ella tiramos `SELECT = FROM registris;`  nos muestra las compras que escribimos
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803223656.png)
	 
	 en otra consola escribimos `kubectl delete -f postgres-deployment.yaml -n labipap` con esto borramos todo incluido la base de datos
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803223821.png)
	 
	 volvemos a mini_commerce y volvemos a tirar `SELECT = FROM registris;` donde nos mostrara Failed
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803223936.png)
	 
	 Ahora volvemos a levantar todo con `kubectl apply -f postgres-deployment.yaml -n labipap` y nos volvemos a conectar en la otra terminal con  `kubectl -n labipap exec -it db-troubleshooter -- psql -h db -U postgres -d mini_commerce`  y dentro tiramos  `SELECT = FROM registris;`  nos muestra que los registro volvieron y que no se borraron
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803224107.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803224151.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803224228.png)
	 
	 Todo gracias por el volumen persistente, porque por mas que borremos todo luego se puede recuperar.
	 
### Finalizar

1. Parar minikube
	 `minikube stop` cerrara toda la arquitectura que creamos
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260803224359.png)
	 
 


---
# Guía del Profesor

# Laboratorio: Arquitectura Cloud con Ingress y Persistencia

  

Este laboratorio tiene como objetivo implementar una arquitectura de microservicios resiliente en Kubernetes, utilizando un **Ingress Controller** como puerta de enlace unificada y **volúmenes persistentes** para garantizar la integridad de los datos.

  

## 🎯 Objetivos del Laboratorio

Al finalizar este laboratorio, serás capaz de:

* **Gestionar el ciclo de vida de las aplicaciones**: Desplegar servicios con contenedores propios.

* **Dominar el enrutamiento**: Utilizar un `Ingress Controller` para exponer múltiples servicios bajo un mismo dominio mediante reglas de path (`/` vs `/api`).

* **Validar la alta disponibilidad**: Demostrar cómo Kubernetes auto-cura servicios mediante `ReplicaSets`.

* **Garantizar la persistencia**: Comprobar mediante `Volumes` y `Claims` que los datos de la base de datos sobreviven a la destrucción de los contenedores.

  

## 🗺️ Esquema de la Arquitectura

```text

[ CLIENTE (Navegador Local) ]

│

Puerto 80 / 443

▼

+------------------------+

| INGRESS CONTROLLER |

+------------------------+

│ │

Ruta / (Front) Ruta /api (Back)

│ │

▼ ▼

[ Serv: frontend ] [ Serv: backend ]

│ │

▼ ▼

[ Pod: Front ] [ Pod: Back ]

│

▼ DNS: db:5432

[ Serv: db ]

│

▼

[ Pod: DB ] ───> [ PersistentVolumeClaim ]

│

▼

[ PersistentVolume ]

  
```

📜 Commands

  

0- Docker build: (front-back)

1- Minikube:

minikube start

minikube addons enable ingress

2- Carga de imágenes:

minikube image load courseipap/backend:1.0.0

minikube image load courseipap/frontend:1.0.0

3- Despliegue de Infra:

k create namespace labipap

k apply -f db-storage.yml -n labipap

k apply -f db-secrets-config.yaml -n labipap

k apply -f postgres-deployment.yaml -n labipap

4- Tunelización:

minikube tunnel (en una terminal separada)

5- Configuración Ingress:

k apply -f app-ingress.yml -n lab-ipap

6- Verificación:

curl -v http://localhost

curl -v http://localhost/api/data

curl -X POST http://localhost/api/data -H "Content-Type: application/json" -d '{"nombre": "Estudiante", "clase": "Kubernetes"}'

7- Resiliencia:

kubectl delete pod -l app=db

kubectl get pods -w

8- HPA

Definir limites:

resources:

limits:

cpu: "100m"

requests:

cpu: "50m"

Ejecutar:

kubectl autoscale deployment backend --cpu-percent=20 --min=1 --max=3 -n lab-ipap

# Bucle para estresar la CPU

while true; do curl -s http://localhost/api/data > /dev/null; done

kubectl get hpa -w -n lab-ipap

9- Eliminado solucion

kubectl delete namespace lab-ipap

  

🧠 Knowledge

Enrutamiento Inteligente con Ingress

  

El Ingress actúa como un "recepcionista". En microservicios, la configuración de las rutas es crítica:

  

Ruta Raíz (/): Todo el tráfico se entrega al frontend-service. Permite acceso directo a la interfaz sin reescrituras.

  

Ruta API (/api): El tráfico se dirige al backend-service. Al usar pathType: Prefix sin rewrite-target global, garantizamos que el backend reciba la ruta completa que espera (/api/data).

  

Lección del Error: Intentar usar un rewrite-target: / global causa errores 404, ya que "limpia" el prefijo /api y el backend termina recibiendo solo /data, perdiendo su contexto de ruta.

  

Alta Disponibilidad (HA) y Replicas

  

Al escalar a múltiples réplicas, creamos un sistema tolerante a fallos:

  

Auto-curación: Si un pod falla o es eliminado, Kubernetes lanza uno nuevo para mantener el estado deseado.

  

Persistencia: Gracias al uso de PersistentVolume y PersistentVolumeClaim, los datos de la base de datos residen fuera del ciclo de vida efímero de los pods. Esto asegura que, incluso si el pod de la base de datos se destruye, la información persiste intacta tras la recuperación del servicio.


  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1WpgKOoBmjLpVmXficgmih2fLVVsdDNQf/view
