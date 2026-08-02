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

1. Creamos los pod:
	 Volvemos a la carpeta repaso que es la que contiene todo la actividad `cd ..`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802204114.png)
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 


---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
