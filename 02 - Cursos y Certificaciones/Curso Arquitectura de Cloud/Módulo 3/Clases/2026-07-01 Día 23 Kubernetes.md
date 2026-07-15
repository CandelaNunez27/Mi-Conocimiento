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

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714230659.png)

- Work node: Funcionan como los musculos, ellos levanta, administran, alojan a los pods, los crean, los administran. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260714230804.png)






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
