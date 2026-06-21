# Teoría: La era serverless & MLOps

# Fundamentos El código como base
No se utiliza los clics en interfaz web (peligro con los clics erróneos) sino por código. Definimos servidores,redes, bases de datos, roles y todo servicio, mediante archivos de texto plano que pueden ser versionados, revisados y automatizados. El crear la receta mayor se hará una única vez (dedicar tiempo en el desarrollo) y ya se puede cuantas veces querramos.

Se usa terrafor, con lenguaje compilado? se puede utilizar con docker.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260619235908.png)

# Fundamentos Infraestructura como código (IaC)
Se busca que la estructura sea escrita, se puede versionar para usar en github para que varios trabajadores trabajen en conjunto, aprovisionar con códigos para que cloud pueda implementar la arquitectura.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620000217.png)


# Fundamentos Paradigma IaC

- **Imperativo:** La forma como se va a ejecutar, tiene un orden que lee de arriba hacia abajo.
- **Declarativo:** Se le indica lo que uno quiere y no importa en que orden lo ejecute, simplemente que lo realice.

- **Mutable:** Si podemos modificar las cosas existentes con parches en caliente, como cambiar nombre de algo. Puede generar inconsistencia.
- **Inmutable:** Se debe borrar y subir ahora con las modificaciones. Garantiza coherencia absoluta. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620003425.png)

# Fundamentos Ahorro extremo
El MLOps aparecion con los distintos modelos (machine learning, ...). machine learning usa mucho el servicio serverless. El MLOps era una tarea de full stack developer (saber de front y back), pero no remplaza  a los que trabajan en cloud. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620004307.png)

# Fundamentos Básicos de IaC
Aparece Terraform que nos sirve para tener una arquitectura modificable. Si el desarrollo esta en aws y se quiere pasar a azure se debe cambiar algunos nombres nada más, por ende es facil el traspaso.  
Para que funcionen los comandos de terraform se debe tener un archivo.tf, para descargarse los plugins, librerias y demas para instalarse.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620004449.png)

# Práctica: Muestra de opciones Serverless. Ver si un archivo se puede exportar según lo que pese con Lambda


### Preparación de Cloudformation

1. Tener:
	Tener una carpera llamada cloudformation con un archivo s3-sns-sqs-lambda.yaml, que tiene un bloque de recursos (resources) y un Outputs (opcional). Resources contiene la creacion del topico de SNS, la creacion del SQS, creacion de subscripcion SNS y SQS (con bloque properties) , creación de Politica de SQS, creación de bucket s3, creación de las politicas de SNS, Creación de rol de IAM para lambda, creación y inyeccion del codigo para la funcion lambda, Mapeo de eventos conectando SQS con la lambda.

### Ejecución de Cloudformation

1. Abrir Terminal en la carperta cloudformation:
	```
	aws cloudformation create-stack \
      --stack-name Lab-FormaTEC-Infra \
      --template-body file://s3-sns-sqs-lambda.yml \
      --capabilities CAPABILITY_IAM
	```
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620231637.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620232002.png)


### Preparación de Terraform

1. Tener:
	Instalado docker y terraform.
	Tener una carpeta llamada terraform con un archivo lambda_funtion_payload.zip y un archivo main.tf, que contiene la configuración de proveedor (colocar que usarmos aws y qué region), creacion del topico de SNS, la creacion del SQS, creacion de subscripcion SNS y SQS (con bloque properties) , creación de Politica de SQS, creación de bucket s3,crear notificacion de backet a sns, creación de las politicas de SNS para entrada desde s3, Creación de rol de IAM para lambda, creación y inyeccion del .zip para la funcion lambda, Mapeo de eventos conectando SQS con la lambda.

### Ejecución de Terraform

1. Abrir Terminal en la carpeta  terraform:
	`terraform init` 
		
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620234905.png)
	`terraform plan` para que muestre lo que va a crear (verde es crear, amarrillo es modificar y rojo eliminar)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621020813.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621020933.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621021018.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621021053.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621021129.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621021201.png)
	``terraform apply -auto-approve`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621022051.png)
	Esto tarda mucho menos que cloudformation que puede tardar 10 min y este lo hizo en 1 min.

# Prueba de subir archivo
1. en interfaz web:
	s3 > 
	lambd

---
# Guía del Profesor

  

💻 Automatización Opción A: AWS CloudFormation (IaC Nativa)

  

Esta plantilla de CloudFormation (s3-sns-sqs-lambda.yaml) despliega el flujo completo de forma 100% automatizada e incluye las políticas de permisos necesarias para la interconexión segura.

  

Ejecutar comando: aws cloudformation create-stack....

  

Subir archivos .csv al bucket

  

Ejecutar comando: aws cloudformation delete-stack

  

📦 Automatización Opción B: Terraform (IaC Agnóstica)

  

Esta es la configuración de Terraform (main.tf) equivalente para el mismo aprovisionamiento. Permite explicarles a los alumnos la diferencia entre el enfoque declarativo puro de CloudFormation (JSON/YAML) frente al lenguaje HCL estructurado y modular de HashiCorp.

  

correr estos comandos:

terraform init

  

terraform plan

  

terraform apply

  

Subir archivos .csv al bucket

  

terraform destroy


---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1vMSbi1o2G3Lvbl50E0jDVKwOe_LDtBkD/view?usp=sharing
