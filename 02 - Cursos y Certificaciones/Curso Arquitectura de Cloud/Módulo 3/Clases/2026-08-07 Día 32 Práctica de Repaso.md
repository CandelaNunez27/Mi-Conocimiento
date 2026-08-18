
# Práctica: Repaso 3
### Preparación

1. terraform:
	`touch main.tf` creamos el main pero las buenas prácticas que minimamente separemos los proveedores en otro archivo, `touch providers.tf` y opcionalmente creamos el output  `touch outputs.tf`
	
	En providers.tf le indicamos que necesitamos tener instalado terraform >= 1.0.0, otra instancia que le indicamos a aws la versión ~> 5.0, y archive la versión ~> 2.4, luego que el proveedor aws la región var.aws_region y en un archivo de variables `touch variables.tf` colocamos una variable que aws_region por default sea us-easte-1. `teraform validate` para ver si no nos equivocamos codiando y nos dira que nos faltan cosas.
	
	
	`terraform init ` y `terraform validate`
	
	En main.tf colocamos data aws_caller_identity. creamos el recurso aws_s3_bucket para data. creamos el rol IAM aws_aim_role para que asume el rol en jsonencode donde permitira a la lambda tener permisos. creamos los permisos para log CloudWatch aws_iam_pole_policy_attachment para que el rol anterior sea adjuntado a la policy arn que ya tiene aws. le colocamos el código en python de como empaquetar. creamos la lambda aws_lambda_function para asignarle el rol de antes junto con el handler app.handler que le indica que cuando aparezca app.handler arranque el proceso y que empaquete en un zip la data, y el runtime python3.11, por último debajo unas variables.  
	
	En output.tf escribimos que nos muestre el nombre del s3_bucket_auditoria, luego que nos muestre el nombre de la ARN de lambda y la función de la lambda.
	
	`terraform validate` para volver a validar si escribimos todo bien, y corregimos si tenemos algun error. y luego `terraform plan` para ver el resumen de lo que crearemos
	

### Despliegue

1. Terraform:
	Por último solo nos queda aplicarlo todo lo que preparamos con `terraform apply`




---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1Md_AsCqCZ2hRO01w5EnfY6LF-2GaWt-m/view
