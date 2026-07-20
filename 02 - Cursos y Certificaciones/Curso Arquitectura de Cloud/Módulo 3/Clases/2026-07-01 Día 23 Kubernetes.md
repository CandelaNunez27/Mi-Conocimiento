# Teoría: Kubernetes

# Evolución Orquestación containers K8s

Orquestación: automatización las tareas degetión de contenedores, puede ser un balanceador de carga, crear toda la estructura de red atravez de servicios, crear recursos perce.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714223234.png)

# Docker Lo que tenemos

El conteiner nos facilitaba que las cosas andaran en cualquier equipo, etc, pero empezaron a surguir limitaciones de los contenedores aislados. 
Cuando ya tenes miles de contenedores divididos que tienes que gestionar, docker se volvia tedioso tener que ir uno por uno viendo que andaran bien, problema de que si queria dos servicios en el mismo puerto no podía, o si necesitaba hacer crecer o decrecer tenia que ser de manera manual
Ojo Docker y docker compose no se ha dejado de utilizar, de hecho se utiliza en estructuras no muy grandes donde no es necesario muchos conteiners.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714224239.png)

# Kubernetes Lo nuevo

Cuando una arquitectura es grande si es necesario un orquestador. Cuando quiero que andes muchos contenedores tambien tengo que tener en cuenta mi capacidad de recursos fisicos porque tendre que agregar fisicamente uno al lado, y entre los dos servidores tienen que tener la posibilidad de trabajar en equipo. 
Para que esta comunicación entre ellos sea posible es necesario clusterizar que esto hará que simulen que esten en un solo servidor grande. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714224937.png)

# Historia Kubernetes

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714225200.png)

# Fundamentos Ciclo de vida k8s (Resiliencia)

1. Kubernete puede crear contenedores
2. Nos permite con comandos modificar en caliente
3. Facilita la configuraación de red
4. Monta volumenes de forma dinamica
5. Puede ser un balanceador de carga si se necesita
6. Se le comunica la minima y la maxima permitida y él ajusta los recursos
7. Con metricas sabe cuando tiene que reiniciar o retirar contenedores inactivos.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714225349.png)

# Fundamentos El Cluster de k8s

La instalación on-prime no es facil, se necesita de minima dos servidores (pueden ser virtuales), uno llamado Plano de control y otro llamado Nodos de Trabajo

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714230527.png)

- Control Plane: Es el que administra y hace toda la magia a nivel de arquitectura, computo y toma de decisiones. Siendo el cerebro. 
	- Kube-apiserver sería la puerta donde tirariamos los comandos siendo el traductor de comandos entre la computadora y el control plane, debemos ser administradores para tirar comandos.
	- Kube-scheduler es el que adiministra las tareas y programa/calendariza todo lo que debe hacer (hoja de ruta). 
	- etcd es la memoria de datos siendo una base de datos no estructurada, guardando todo lo que teiene que saber para a futuro entender todo lo que esta haciendo el control plane, es critico po lo que se debe casi no tocar. 
	- En on-prime es Kube-controller-manager y en nube es cloud-controller-manager, en on-prime es el que controla que los Work node este haciendo las cosas bien y el cloud es el que enlaza con la nube que se administra solo.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714230659.png)

- Work node: Funcionan como los músculos, ellos levanta, administran, alojan a los pods, los crean, los administran. 
	- Kubelet de la capa de administración, le dice a cada contenedor que hacer.
	- kube-proxy de la capa de administración, es quien se encarga de la comunicación entrada y salida por red.
	- POD en la capa de acción tenemos todos los contenedores corriendo.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714230804.png)

# Fundamentos Jerarquía K8s

El clúster es el work node. Luego el nodo es uno de los servidores que puede tener el clúster, es lugar donde se almacena fisicamente. POD es la unidad  minima que puede gestionar a nivel de computo kubernetes. Dentro estaran los contenedores, pueden ir uno o dos, cuando se colocan dos es porque se quiere que entre ellos casi no tengan latencia. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719020802.png)

El contenedor es la aplicación dockerizada. EL deployment es la receta .yml siendo las directivas para el pod de como lo administre. POD unidad mínima que puede puede administrar kubernetes, ya que si tiene que eliminar kubernetes eliminaria el pod no el contenedor en sí. Service es el recurso que nos sirve para que le de conectividad a red o otros servicios.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719020831.png)

# Fundamentos Imperativo vs Declarativo

Es Imperactivo: cuando le digo a kubernetes "quiero x cosa"  y comparando sus metricas con lo que tiene realiza las modificaciones que se le pidio. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719022513.png)

# Fundamentos K8s YAML

El inicio del yaml es como esto:
	`Kind`:  nos define lo que quiero hacer, qué tipo es.
	`metadata`: simplemente es el nombre
	`spec: replicas`: es por si quiero hacer replicas.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719022837.png)

# Fundamentos HPA - Volúmenes

HPA: Horizontal POD Autoscaler es la función que tiene kubernetes que esta constantemente monitoreando. lo que  se observa en la imagen son las métricas que con dos pod se le indico a hpa que si la carga del cpu supera el 70% duplica mas pod para bajar esta carga.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719023305.png)

Volúmenes: el pod tendrá datos efímeros para ello se le tiene que asignar un volumen como en docker, pero la diferencia con docker es que previamente se debe declarar un volumen un PV (Persistent Volume), que es una parte de un disco que debe estar reservada para varios PVs.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719023322.png)

*Nota: ya para infraestructuras más avanzadas y para optimizar tu clúster de forma integral, se usan Karpenter. Es una excelente herramienta para aprovisionar nodos al clúster bajo demanda. Sin embargo, para un flujo de autoescalado completo, se complementa con otras herramientas que manejan los Pods: KEDA (Kubernetes Event-driven Autoscaling),Kubernetes HPA (Horizontal Pod Autoscaler), Kubernetes VPA (Vertical Pod Autoscaler) .*
# Resumen Kubernetes

Kubernetes no es un ejecutor de comandos. Kubernetes es un automatización que lee archivos yaml y también el estado actual del clúster, haciendo modificaciones decreciendo o creciendo según lo que compara con la realidad.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719024505.png)

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/18djocO3rKPTP8RTXEbiBWlTH8aCMJfaW/view 
