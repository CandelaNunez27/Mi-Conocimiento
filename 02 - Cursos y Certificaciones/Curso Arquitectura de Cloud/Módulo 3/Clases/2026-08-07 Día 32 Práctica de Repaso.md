
# Práctica: Repaso 3
### Preparación

1. terraform:
	`touch main.tf` creamos el main pero las buenas prácticas que minimamente separemos los proveedores en otro archivo, `touch providers.tf` y opcionalmente creamos el output  `touch outputs.tf`
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831232528.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831232558.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831232621.png)
	
	
	En providers.tf le indicamos que necesitamos tener instalado terraform >= 1.0.0, otra instancia que le indicamos a aws la versión ~> 5.0, y archive la versión ~> 2.4, luego que el proveedor aws la región var.aws_region y en un archivo de variables `touch variables.tf` colocamos una variable que aws_region por default sea us-easte-1. 
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831232740.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831232811.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831232851.png)
	
	
	
	`teraform validate` para ver si no nos equivocamos codiando y nos dira que nos faltan cosas. 
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233045.png)
	
	
	
	`terraform init ` y `terraform validate`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233559.png)
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233631.png)
	
	En main.tf colocamos data aws_caller_identity. creamos el recurso aws_s3_bucket para data. creamos el rol IAM aws_aim_role para que asume el rol en jsonencode donde permitira a la lambda tener permisos. creamos los permisos para log CloudWatch aws_iam_pole_policy_attachment para que el rol anterior sea adjuntado a la policy arn que ya tiene aws. le colocamos el código en python de como empaquetar. creamos la lambda aws_lambda_function para asignarle el rol de antes junto con el handler app.handler que le indica que cuando aparezca app.handler arranque el proceso y que empaquete en un zip la data, y el runtime python3.11, por último debajo unas variables.    
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233251.png) 
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233306.png)
	
	En output.tf escribimos que nos muestre el nombre del s3_bucket_auditoria, luego que nos muestre el nombre de la ARN de lambda y la función de la lambda.    
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233333.png) 
	
	`terraform validate` para volver a validar si escribimos todo bien, y corregimos si tenemos algun error. y luego `terraform plan` para ver el resumen de lo que crearemos  
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233732.png)
	
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233829.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233858.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233919.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831233943.png)

### Despliegue

1. Terraform:
	Por último solo nos queda aplicarlo todo lo que preparamos con `terraform apply` 
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260831234053.png)

2. AWS:
	Ahora ingresamos a nuestra cuenta de aws para ver que se ccreo lo anterior.
	Revisamos el s3, la lambda con su ClowdWatch

### Borrar todo

1. Terraform:
	borramos todo con `terraform destroy` y nos mostrara un plan también donde nos indica todo lo que borrara, le indicamos `yes`. Y ya en aws no estará nada de lo que creamos con terraform


---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1Md_AsCqCZ2hRO01w5EnfY6LF-2GaWt-m/view
