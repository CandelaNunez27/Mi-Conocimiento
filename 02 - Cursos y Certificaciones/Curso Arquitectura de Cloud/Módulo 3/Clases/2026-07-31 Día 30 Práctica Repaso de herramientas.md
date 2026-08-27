# Práctica: Despliegue de las herramientas docker, kubernetes/minikube
### Preparación primera parte en local

1. el profe muestra como borro sin querer algunas cosas y las restaura:
	 `git status` para ver el estado de los archivos, salen en estado deleted
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260807133726.png)
	 
	 para solucionarlo `git restore .` y luego `git status` nuevamente
	 ![](04%20-%20Otros/Imagenes/Pasted%20image%2020260807133902.png)
	 

2. minikube y terraform:
	 
	 Abrimos terminal en la captera llamada local, que contiene audit-k8s.yml, main.tf, providers.tf. 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826231123.png)
	 
	 Tenemos el archivo providers.tf donde teniene que llama al proveedor oficial de hashicorp (creador de terraform), luego usa la configuración local de kubernetes / minikube. 
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826231140.png)
	 
	 
	 
	 `minikube start` infraestructura local atraves de minikube
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826231656.png)
	 
	 `terraform init` para despertar a terraform
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826231750.png)
	 
	 
	 `terraform plan` para que me muestre todo lo que creara, antes de ejecutarlo. mostrara lo que creará sin crearlo. por ende, sería un comando opcional.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826231911.png)![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826231927.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826232032.png)
	 
	 `terraform apply`  muestra lo que va a crear pero también lo crea si le indicamos que yes cuando nos pregunte. entonces si queremos crear directamente usamos este comando, si queremos una vista previa antes que todo se despliegue se usa plan.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826232301.png)
	 
	 Tenemos el archivo main.tf, que crea un recurso namespace llamado name audit-lab. luego resource para un contenedor con name web-app y se asocia al ns,y luego spec que haga una replica,  un spec que tenga nginc:alpine con el puerto 80.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826232337.png)
	 
	 
	 `kubectl get all -n audit-lab` para ver que desplego terraform
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260826232428.png)
	 

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
	 
	 `cd modulos/mod3/class7/aws-II` Nos movemos a la carpeta aws-II que contiene un providers.tf, main.tf, output.tf, landa_funtion.yml. host.init, deploy-and-audit.yml `ls`
	 
	 
	 
	 Tenemos el archivo providers-tf que contiene los required_providers hasicorp/aws , hashicorp/tls y hansicor/local, la region us-east-1 y llamamos a aws_caller_identity porque hay que trabajar con cosas locales.
	 
	 Tenemos el archivo main.tf que contiene la parte de seguridad de las maquinas virtuales que crearemos y usaremos colocando recource tls_private_key generando una key con cifrado rsa 4096, luego en resource aws_key_pair le colocamos el key_name pem-lab-terraform, luego para descargarla localmente con resource local_file con permisos a ese archivo 0400. Luego la parte de redes tenemos las reglas para a conexion, donde colocamos que el puerto 22 (ssh), 80 (http nginx) y 8080 (http apache) lo abrimos para cualquiera, tambien la regla egress porque es para que lo que creemos pueda navegar. Después tenemos instancias ec2 con resource aws_instance servidor_nginx , resource aws_instance servidor_apache. Sigue un bucket con resource aws_s3_bucket bucket_ingesta y resource aws_s3_bucket_notification. Quinto tenemos las notificacines de sws a sqs con resource aws_sns_topic notificaciones_sns, resource aws_sqs_queue cola_procesamiento, resource aws_sns_topic_subcription, resource aws_sqs_queue_policy. Dentro de estas tiene andemas un name. pero la diferencia es lo que esta al lado de resource es como la variable en el código para terraform pero en aws nos mostrara el name. Y finalmente tenemos el apartado de la lambda resource aws_iam_role rol_lambda donde le indicamos que ejecute el payload.zip 
	 
	 Tenemos el archivo output.tf que contiene putput nginx_public_ip, output apache_public_ip, output s3_bucket_name y output ssh_private_key_pem. Todo esto lo mostrara cuando termine de ejecutarse el terraform apply
	 
	 Tenemos que tener logeada en la consola el aws con el acceskey
	 `terraform init` ejecuta todo lo de providers.tf
	 
	 
	 `terraform plan` nos mostrara el resumen
	 
	 
	 `terraform apply -auto-approve` y tetrraform y aws trabajaran. Aunque yo tire en el proceso de creación un ctrl + c, aws seguira creando porque ya le recibio la señal
	 
	 


### Ansible instalar cosas en la nube

1. teniendo las ip
	 Aun no podemos ir al navegador ara ver que tenemos en esas ip porque aun no corremos el archivo deploy-and-audit.yml
	 
	 Tenemos el archivo deploy-and-audit.yml donde tenemos varios tasks donde 1 actualizaremos cache de api, 2 instalar dependencias, 3 instalar docker, 4 asegurar que docker este activo y corriendo, 5 agregar el usuario para docker y darle permisos para que haga acciones, 6  desplegar nginx dockerizado por puerto 80, 7 desplegar apache dockerizado por el puerto 8080,  8 validación final con respuesta en http local.
	 
	 para indicarle a ansible donde tiene que apuntar creamos un archivo llamado hosts.ini donde adentro le colocamos las ip generadas. En ese archivo comentamos con ; por un momento el apartado servidores_web:vars
	 `ansible-playbook -i hosts.ini deploy-and-audit.yml` que nos da error que es esa linea que comentamos. prque si lo descomentamos si funciona.
	 Es para comparar con el comando que usábamos antes `ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts.ini deply.yml` y veamos sus diferencias, porque si ejecutamos `ssh -i pem-lab-terraform.pem ubuntu@34.224.25.64` nos estamos conectando a la ec2 de nginx que esta en aws pero al conectarnos nos pregunra esta seguro de querer conectarse y le damos yes, bueno ese yes no lo puede colocar ansible por ende se utiliza esa linea donde se le indica que no haga esos chequeos y pase directo.
	 

2. Revisamos si se ejecuto bien
	 
	 Ingresamos a nuestra cuenta de aws y chequeamos que se alla creado la landa (home > lambda > procesadorReportesAuditoria-tf), el bucket (home > s3 > formatec-auditoria-tf-99998980989898),  las EC2s (home > ec2) la queue(home > simple queue service> ColaProcesamietoAuditoria-tf) y la sns (home > simple notification service > topic > notificacionesAuditoria-tf) 
	 
	 

### Subimos un archivo de prueba

1. Probamos si anda como el ejercicio que usamos hace varias clases cando vimos lambda
	En S3 > Buckets > formatec-auditoria-tf-90909989 > upload > Seleccionamos el reporte.txt que creamos en local y lo subimos
	
	Luego en la lambda > funtions >procesadorReportesAuditoria.tf > monitor > hace menos de 1 hs > vemos los grafico que nos muestra > tambien vemos los logs con view cloudwhatch logs > ultimo log > y veremos todos los pasos del codigo de la lambda


### Revisamos conexión

1. Navegador:
	Ahora si tiramos http://34.224.25.64:80 que es el nginx y el apache en  http://3.93.68.144:8080 


### Borrar todo

1. Borrar todo con terraform:
	`terraform destroy -auto-approve`




---
# Guía del Profesor
## Ej local

Steps

### 1

Iniciar Minikube

### 2

Ejecutar terraform local

### 3

Ejecutar el ansible

ansible-playbook audit-k8s.yml

### 4

Leer el archivo generado

  

# AWS

### 1

activar las credenciales

### 2

Ejecutar terrafom

### 3

Ageragar el host al archivo

### 4

Ejecutar ansible

ansible-playbook -i hosts.ini deploy-and-audit.yml


  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1Ph5XmKpvVkGMKvMJjy7A-nPai72_WxlL/view
