# Práctica: Primeros pasos con minikube
### Preparación

1. Descargamos y permisos necesarios:
	`sudo pacman -S minikube`
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722212846.png)
	
	`sudo pacman -S kubectl`	
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722235456.png)
	
	`sudo usermod -aG docker SUPER` Para trabajar con los servicios de docker sin problema de permisos
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722215728.png)
	
	`newgrp docker` Actualiza la sesión de la terminal para que reconozca los nuevos permisos (aplicando los cambios al grupo)
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722220109.png)

2. Arrancamos un minikube:
	`minikube start --driver-docker -p minik8s` driver para que use el servicio, -p para colocarle un nombre. 
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722222128.png) 
	
	se puede ver como dice que utilizara docker, que inicia un cluster de nombre minik8s como control plane, se descarga una imagen v0.0.50 creando un cluster de 2 nucleos y de 3072MB de ram, utilizando las versiones de kubernetes v1.35.1 y de docker v29.2.1, etc
	
	`minikube status -p minik8s` si no se le coloco nombre en el paso anterior no hace falta indicarle el nombre, pero en nuestro caso si con -p
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722233547.png)
	
	`docker ps`
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722233758.png)


### Empezar a ver comandos de Kubernetes (kubectl)

1. Utilizar Kubectl (es la linea de comunicacion punto a punto con el kubernetes):
	`kubectl config current-context` nos devuelve a que cluster estoy conectado
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260722235555.png)
	
	`kubectl get namespace` o `kubectl get ns` get = obtener lo que tengo desplegado, ns  lista todos los espacios de nombre disponibles en el cluster, nos permite agrupar logicamente cosas como Pods, deployments y servicios de forma aislada.
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260723000309.png)

2. Arrancamos con pod:
	`kubectl run nginx-test --image=nginx:alpine` creamos un pod con la imagen de alpine
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724002830.png)
	
	`kubectl get pods` listado de pod creados
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724002912.png)
	
	`kubectl logs nginx-test` y `kubectl logs nginx-test --follow` nos mustra los log y --follow para verlos en vivo
	así trabaja un travel suting (resuelve problemas)
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003007.png)
	
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003039.png)
	
	
	
	`kubectl exec -it nginx-test -- sh` para entrar dentro del nginx o sea el bash del pod y mostramos lo que tiene con `ls` , donde estamos parados con `pwd`  y para salir `exit`
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003305.png)
	
	`kubectl delete pod nginx-test` para borrar este pod de prueba
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003416.png)
	

3. Manifiesto (equipos de trabajo):
	kubernetes no es un traductor de comandos. Se puede trabajar en grupo para ello se crean equipos (manifiestos). Para ello se crea un archivo pod1.yml (apiversion, kind: pod, metadatos con el nombre y etiqueta, spec: declara el conteiner y el poder de computo colocandole nombre, imagen, y puerto del contenedor: 80)
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003511.png)
	 
	 
	 `kubectl appy -f pod1.yml` para crearlo, hay que estar parados en la ruta expecifica
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003622.png)
	 
	 `kubectl get pod` lista los pods o para más información `kubectl describe pod pod-demo-red` es distinto al de logs `kubectl logs pod-demo-red` porque este comado muestra los logs del contenedor y comando anterior mustra los logs del pod
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003653.png)
	 
	![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003755.png)
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003813.png)
	 
	 `kubectl get pod -o yaml ` cuando uno de nuestro equipo creo un pod que no conocemos podemos utilizar este comando para ver informacion. si tengo un solo pod funciona si tengo mas le expecifico el nombre, tambien muestra informacion 
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003901.png)
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003922.png)
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724003950.png)
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724004011.png)
	 
	 `kubectl get pod -o yaml > export_pod1.yaml` también podemos exportar toda esa información, una copia donde podemos modificar y crear uno nuevo mejorado.
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724004144.png)
	 
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260724004308.png)



---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
