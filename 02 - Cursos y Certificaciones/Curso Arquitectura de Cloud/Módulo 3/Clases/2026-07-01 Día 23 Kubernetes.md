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

El clúster es el work node. Luego el nodo es uno de los servidores que puede tener el clúster, es lugar donde se almacena fisicamente. POD esta dentro de cada nodo

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719020802.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260719020831.png)




# Práctica: sawkl
### Preparación

1. sdssdf:
	sdsld

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
