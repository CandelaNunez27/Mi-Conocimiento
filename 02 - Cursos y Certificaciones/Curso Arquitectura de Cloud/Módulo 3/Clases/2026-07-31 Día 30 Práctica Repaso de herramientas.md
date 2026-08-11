# Práctica: Despliegue de las herramientas docker, kubernetes/minikube
### Preparación primera parte en local

1. el profe muestra como borro sin querer algunas cosas y las restaura:
	 `git status` para ver el estado de los archivos, salen en estado deleted
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260807133726.png)
	 
	 para solucionarlo `git restore .` y luego `git status` nuevamente
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260807133902.png)
	 

2. minikube y terraform:
	 
	 Abrimos terminal en la captera llamada local, que contiene audit-k8s.yml, main.tf, providers.tf. 
	 Tenemos el archivo providers.tf donde teniene que llama al proveedor oficial de hashicorp (creador de terraform), luego usa la configuración local de kubernetes / minikube. 
	 
	 `minikube start` infraestructura local atraves de minikube
	 
	 `terraform init` para despertar a terraform
	 
	 `terraform plan` para que me muestre todo lo que creara, antes de ejecutarlo. mostrara lo que creará sin crearlo. por ende, sería un comando opcional.
	 
	 `terraform apply`  muestra lo que va a crear pero también lo crea si le indicamos que yes cuando nos pregunte. entonces si queremos crear directamente usamos este comando, si queremos una vista previa antes que todo se despliegue se usa plan.
	 
	 Tenemos el archivo main.tf, que crea un recurso namespace llamado name audit-lab. luego resource para un contenedor con name web-app y se asocia al ns,y luego spec que haga una replica,  un spec que tenga nginc:alpine con el puerto 80.
	 
	 `kubectl get all -n audit-lab` para ver que desplego terraform
	 
	 

### Ansible, primeras preguntas de la auditoria

1. Cuantos servidores tenemos?
	 Ansible nos da una pequeña auditoria / relevamiento.
	 Tenemos el archivo audit-k8s.yml que en primer lugar se coloca un name, y donde se tiene que conectar con hosts: localhost, con conexión local, creara dos variables internas en ansible. Su primera tarea tasks es obtener informacion de los pods del ns indicando kind pod namespace audit-lab que es una variable de arriba. 2do valida las politicas de seguridad en los pods con un código. 3ero generar el reporte estructura escrita con todas las variables donde guadaba los datos. 4to mostrar en consola que la auditoria se realizado  con exito.
	 
	 
	 `ansible-playbook audit-k8s.yml` nos mostrara los pasos que hizo.
	 
	 En la carpeta que estabamos parados se genera un reporte-auditoria-k8s.txt 
 
### Borrar todo

1. Borrar todo con terraform:
	`terraform destroy -auto-approve `
 
### Preparación segunda parte en aws
 
1. AWS
	 Nos movemos a 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 
	 

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1Ph5XmKpvVkGMKvMJjy7A-nPai72_WxlL/view
