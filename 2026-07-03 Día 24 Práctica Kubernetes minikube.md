# Práctica: sawkl
### Preparación

1. Descargmos y iniciamos minikube:
	`sudo pacman -s minikube`
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722212846.png)
	
	`sudo usermod -aG docker SUPER` Para trabajar con los servicios de docker sin problema de permisos
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722215728.png)
	
	`newgrp docker` Actualiza la sesión de la terminal para que reconozca los nuevos permisos (aplicando los cambios al grupo)
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722220109.png)
	
	`minikube start --driver-docker -p minik8s` driver para que use el servicio, -p para colocarle un nombre. 
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722222128.png)
	
	se puede ver como dice que utilizara docker, que inicia un cluster de nombre minik8s como control plane, se descarga una imagen v0.0.50 creando un cluster de 2 nucleos y de 3072MB de ram, utilizando las versiones de kubernetes v1.35.1 y de docker v29.2.1, etc
	
	`minikube status -p minik8s` si no se le coloco nombre en el paso anterior no hace falta indicarle el nombre, pero en nuestro caso si con -p
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722233547.png)
	
	`docker ps`
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722233758.png)









---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
