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

### Levantar servicios con .yml

1. Servicio 1:
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731003351.png)
	
	 Tenemos el archivo svc_clusterid.yml donde hay apiVersion, kind:  Service, de nombre servicio-interno,  con el tipo ClusterIP, el puerto y la app que sera el pod (colocando su nombre), utilizando el selector para comunicarnos. Que este pod lo tenemos configurado en el archivo pod1.yml. Lo que hace este servicio es que si alguien consulta por el puerto 80 llevalo a ese puerto 80 de ese pod.
	 
	 `kubectl apply -f svc_clusterid.yml` para crear el servicio. `kubectl get service`. ya tendriamos el servicio creado. 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731215527.png)

2. Servicio 2 (Pod utilizado por el profesor para hacer travel suting donde trabaja):
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731215619.png)
	 
	
	 Tenemos el archivo my_curl_pod.yml, que contiene apiVersion, kind: pod, metadata de nombre network-debugger y el nombre de la labels app igual. spec indicandole el conteiner a crear, con nombre networl-debugger-container, su imagen que es una imagen publica que descarga de aws, los comandos para que pueda descargarlo,  "-c" es para que entienda que es un comando lo de acontinuazcion.
	 
	 `kubectl apply -f my_curl_pod.yml` y `kubectl get pod`, tarda un poquito porque esta descargando la imagen, pero una vez listo nos permitira ingresar a ella
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731221502.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731221650.png)
	 
	 `kubectl exec -it network-debugger -- sh ` ingresaremos al conteiner con la imagen. donde podremos tirar comandos como `curl http://servicio-interno` donde descubrira nuestro otro servicio, gracias a nuestro servicio-interno estoy pudiendo llegar a nuestro pod pod-demo-red. Para salir usamos `exit`
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731222116.png)
	 
	 Ahora nos conectaremos a nuestro pod, `kubectl exec -it pod-demo-red -- sh` donde tiramos `curl localhost`, y debería de responder exactamente lo mismo.
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731222351.png)
	 
	 Pero si ejecutamos desde nuestra consola `curl http://servicio-interno`, no nos debería de dejar acceder porque no esta expuesto el puerto. Para ello el tercer servicio.
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731222720.png)
	 

3. Servicio 3: 
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731225832.png)
	 
	 Tenemos el archivo svc_nodeport.yaml donde hay apiVersion, kind:  Service, de nombre servicio-externo-nodo,  con el tipo, el puerto tambien 80 pero con nodePort 31080 que esto fuerza al servicio utilizar este puerto. y la app que sera el pod del archivo pod1.yml. Lo que hace este servicio es que le decimos que al 80 mandalo al 31080 del cluster, quedando expuesto para nuestro kubernetes
	 
	 `kubectl apply -f svc_nodeport.yaml` y `kubectl get service` creamos el tercer servicio que nos permite la comunicación entre nuestro equipos
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731230204.png)
	 
	 `minikube -p minik8s ip` o `minikube profile list`para ver nuestra ip de nuestro contenedor que corre minikube, aunque todavia no se creo ninguna ip externa a la api. pero con esta ip nos permite a conectarnos desde nuetra pc. 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731230640.png)
	 
	 
	 `curl http://192.168.49.2:31080` y en el navegador
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731230945.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731231126.png)
	 
	 Aunque, aveces hay problemas al exponerlo por un tema de estar usando minikube con docker, ya que hay que indicarle a minikube que abra el puerto y su servicio docker tambien. Para ello se utiliza el siguiente servicio. 
	 
	 
	 
	 
	 

4. Servicio 4:
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260731235421.png)
	 
	 Tenemos el archivo svc_loadBalancer.yml donde hay apiVersion, kind:  Service, de nombre servicio-balanceador,  con el tipo loadBalancer, el puerto 80 y la app que sera el pod del archivo pod1.yml. Lo que hace este servicio es que nos soluciona el problema de no llegar desde nuestra pc, trayendo una ip externa a por ejemplo aws.
	 
	 `kubectl apply -f svc_loadBalancer.yml` y `kubectl get service` para crear el servicio y ver lo que ya tenemos en runing
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260801000246.png)
	 
	 
	 En  otra terminal dejar corriendo:  `minikube tunnel -p minik8s` nos crea el tunel que se quedara escuchando
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260801003354.png)
	 
	 Volviendo a la terminal anterior realizamos `kubectl get service` o `kubectl get svc` que es lo mismo
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260801003032.png)
	 
	 Paso de estar pendiente a ya tener una asignada, en un caso donde no haya funcionado lo del servicio anterior tendria que salir 127.0.0.1 como a mi profesor
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260801003717.png)
	 
	 Probamos la conexion `curl http://127.0.0.1` mi profesor y yo `curl http://10.102.163.11`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260801004036.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260801004311.png)
	 
	 La logica es que kaint lo conecta un puerto extra. Y no es buena practica exponer los nodepot porque nos estariamos pegando siempre al mismo servicio, para ello se hacen varios servicios que corren atras con servicios tipo clusterApi. ClusterApi es como si le fijaramos una ip con un puerto de manera privado. con nodeport estamos exponiendo pero tendria que ir uno a uno por ende es más tedioso.
	 


### Levantar divicion logica de Nodespace  con .yml

1. Namespace:
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802011216.png)
	 Tenemos el archivo namespace.yaml con appiVersion, kind Namespace, metadata name formatec-apps. Este namespace es una division logica que nos permite realizar las mamuscas que se hablo en la teoria.
	 
	 `kubectl apply -f namespace.yaml` para crear el namespace
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802012256.png)

2. Deploy base de datos (una mamusca):
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802012329.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802012432.png)
	 
	 Tenemos el archivo deploy_db.yaml con kind Deployement, name postgres-db, namespace fomatec-apps (para que se coloque por debajo del namespace, encapsulado), label app db-backend, tiene dos spec donde el primero tiene replicas: 1, selector app postgres-pod, y template app postgres-pod, el segundo spec tiene que cree un contenedor, con sus datos.
	 Luego de ese mismo archivo se encuentra dividido por unos --- donde arranca a codificar un servicio, apiversion, kind Service, Name postgres-db namespace formatec-apps, spec type ClusterIP, port 5432, selector app postgres-pod 
	 
	 `kubectl apply -f deploy_db.yaml` y `kubectl get pod` para crear el deploy. En la lista de pod no se tendria que ver el pod que crea el deploy_db.yaml porque presisamente esta encapsulado en namespace
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802012636.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802012745.png)
	 
	 
	 Para verlo se utiliza `kubectl get ns` o `kubectl get namespace` entonce una vez visto el nombre utilizamos `kubectl get pod -n formatec-apps` o `kubectl -n formatec-apps get po ` o `kubectl -n formatec-apps get all`
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802012900.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802013021.png)
	 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802013110.png)
	 
	 
	 
	 Entonces se puede ver que la mamusca esta creada con esta esttructura:
	 - Deployment_apps
		 - replicaset_apps
			 - pod
	 y por otro lado el servicio que levantamos al final del archivo
	 
	 `kubectl delete -f deploy_db.yaml`para eliminarlo
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802013150.png)
	 
	 

### Borrar todo lo que quedo

1. `minikube stop -p minik8s` se para y se borra todo
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260802013318.png)


---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1qLWL5ZERM9CWPJYqHx_0EctjJnsUESjh/view
