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
	 


### Despliegue de arquitectura

1. Creamos el namespace:
	 Volvemos a la carpeta repaso que es la que contiene todo la actividad `cd ..`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802204328.png)
	 
	 `kubectl create namespace labipap` lo crearemos desde la consola ya que crear el archivo yaml como la clase pasada no es tan necesario ya que son muy poquitas lineas. `kubectl get ns`
	 
	 Tenemos el archivo  postgres_deployment.yaml que tiene apiversion, kind Deployment, name postgres-db, spec containers volieMounts, secretkey que apunta al otro archivo db-secret-config.yaml. etc, con su servicio. luego un backend con su servicio, y por ultimo un frontend con su servicio
	 
	 Tenemos el archivo db-secret-config.yaml que tiene apiversion, kind Secret, name db-credentials, data usarname y passwoed en codificacion en bash64. Tambien tiene un Kind ConfigMap, name db-config, data db_name "mini_commerce"
	 

1. Deployment:
	 Ahora si empezamos a desplegarlo en nuestro namespace
	 `kubectl apply -n lapipap -f db-storage.yaml` y `kubectl apply -n lapipap -f db-secret-config.yaml`
	 
	 `kubectl get all` o `kubectl get all -n labipap`no va a mostrar lo que creamos porque get all muestra más que nada servicios basicos, pods, etc
	 
	 
	 `kubectl get secret -n labipap` aca si se mostrara el db-credentials
	 
	 
	 `kubectl get cm -n labipap` mostrara el db-config y kube-root-ca.crt
	 
	 
	 `kubectl get pv -n labipap` mostrara los volumenes presistentes
	 
	 
	 Ahora seguimos desplegando con `kubectl -n labipap apply -f postgres-deployment.yaml`
	 
	 y ahora como ya lo desplego todo el deployment lo veremos en `kubectl get all -n labipap` aunque nos aparece el pod de backend ready 0, puede ser un problema de la imagen pero para mas info tiramos `kubectl -n labipap describe pod backend-casdasdasd` buscamos el bloque de eventos, nos muestra el error con la imagen courseipap/backend:1.0.4. esa linea esta en el postgres-deployment.yaml en la parte del backend por ende lo cambiamos a courseipap/backend:1.0.0. Pero si tiramos `kubectl get pods -n labipap` nos sigue saliendo en ready 0. para eso se tiene que volver a ejecutar `kubectl -n labipap -f postgres-deployment.yaml` . Todo esto es para ver como se soluciona un error y siempre se suguiere que se haga un reinicio desde la mamusca mas grande en nuestro caso el deployment
	 
	 ahora estara todo bien en `kubectl get all -n labipap` y en `kubectl -n labipap describe pod backend-sdajsdjalksdja`
	
	 
	 

### Generamos la rutas de conectividad segun el grafico de la aquitectura
 
 1. Probamos desde nuestra pc
	 `curl -v localhost` no nos muestra nada porque aun nos falta el ingress controler para que direccione todo.

2. Ingress (recurso de kubernetes):
	Tenemos el archivo app-ingress.yaml donde tenemos 
	 
	 `kubectl -n labipap apply -f app-ingress.yaml` para que se cree. y nuevamente `kubectl get all -n labipap ` no lo va a mostrar porque no es un recurso basico. para verlo usamos `kubectl get ingress -n labipap`  con eso ya tendriamos las rutas de comunicacion.
	 
	 tiramos nuevamente `curl -v localhost` pero falla nuevamente por estar usando minikube. para eso hacemos como la clase anterior un tunel en una nueva terminal.
	 
	 `minikube tunnel` creara el tunel luego de pedirnos la contraseña de nuestra pc y nos quedara tomada la terminal.
	 
	 
	 nuevamente volvemos a `curl localhost` y probamos en el navegador `http://localhost`y. Ahora si nos anda los dos. 
	 
	 
	 También probamos `curl localhost/api` nos sale un error pero medio engañoso, el api es un recurso que esta en nuestro ingress controler pero es algo de nuestro index.js que esta en nnuestra carpeta de docker > backend. si revisamoes ese index.js tiene atributos api/data por ende lo probamos, `curl localhos/api/data` este no nos devuelve nada.
	 
	 
	 Este error no es un error de kubernetes si no es un error un de la configuracion. lo encontramos en el app-ingress.yaml en annotations. un rewrite-target es para las consultas localhost/.... a kubernetes no le interesa lo que se coloque despues del / . para ello se cambia el archivo app-ingress.yaml a por el archivo app-ingress.yml donde se le saca el rewrite. En este nuevo si les coloca las posibilidades que hay si se le coloca cosas distintas luego de la /.  Esto es bueno para generar estos dos caminos que vemos en el grafico de la arquitectura.
	 
	 
	 Entonces para que funcione colocamos `kubectl -n labipap apply -f app-ingress.yml` y revisamos que siga corriendo el tunel
	 

### Compra del cliente y resiliencia

1. Escribir en la base de datos (compra ecomers)
	 Actualmente la base de datos esta vacia por ende con este comando le colocaremos una "compra" `curl -X POST http://localhost/api/data -H "Content-Type: application/json" -d ´{"nombre": "Estudiante", "clase": "Kubernetes"}´ ` para ver que se guardo con exito ejecutamos curl localhost/api/data y nos sale.
	 

2.  
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 


---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
