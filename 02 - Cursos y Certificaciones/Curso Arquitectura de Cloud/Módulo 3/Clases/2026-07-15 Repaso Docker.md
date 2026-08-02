# Práctica: Repaso de Docker
### Preparación

Estructura del proyecto:



1. Asegurarse que el servicio docker este levantado
	 `systemctl status docker`
	
	
	
	
	

2. arrancar un minikube:
	 `minikube start`
	
	 `minikube status`
	
	 `minikube addons list ` lista de agregados / plugins que tiene minikube y que se pueden utilizar que son de terceros. De esa  lista vamos a activar el ingress que es creado por kubernetes, ingress-dns creado por minikube, istio y inspecktor-gadget creado por 3rd party
	 
	 `minikube addons enable ingress` se vera enable en la lista
	 


3. En la carpeta docker
	 La carpeta docker tiene dos carpetas, una llamada backend y otra frontend.
	 `cd backend` nos movemos para la carpeta backend
	
	 `docker build -t courseipap/fronend:1.0.0 -f Dockerfile.backend --no-cache .` se buildea la imagen,  -f es para colocarle el nombre del archivo.
	 
	 
	 
4. Cargar imagenes a minikube:
	SD


---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
