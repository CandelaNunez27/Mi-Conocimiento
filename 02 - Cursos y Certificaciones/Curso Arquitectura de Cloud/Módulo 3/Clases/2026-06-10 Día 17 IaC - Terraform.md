# Teoría: Terraform

# Fundamentos IaC
Aws tiene Cloudformation y las demás se enfocaron en terraform
IaC quiere dejar los clics para pasar a código, por lo tardio que es hacerlo por consola web o puede haber errores de clics equivocados. También cada área de IT trabajara con el mismo código para que haya igualdad.  No importa donde compile el código se debe desplegar lo mismo. Los errores son notificados antes de arrancar con el proceso de despliegue, al tirar el comando ``terraform apply`

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621182152.png)

# Fundamentos Paradigma
- **CloudFormations:** Una receta / Check list que se ejecuta en orden / pila de acciones. El código la hace de manera secuencial, leyendo y ejecutando.
- **Terraform:** no hace un plan de acción de despliegue, ve como despegarlos de la manera más rápida posible.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621182714.png)

# Fundamentos Terraform
Terraform domina el mercado, las otras seria cloudformation, opentofu, kurumi, etc. Creado por HashiCorp y utiliza un lenguaje específico de dominio (DSL) llamado HCL (HashiCorp Configuration Language) Además, soporta de forma nativa la sintaxis JSON.

Tiene la ventaja de que es multinube y dockers. Además es modular por lo que es especializado según la nube y la traducción de cambiar de nube es simple, se utiliza alguna IA que lo traduzca.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621182758.png)

# Terraform Ciclo de Vida
- `terraform init`: donde tengamos nuestro main.tf, crea archivos para preparar el entorno de trabajo.
- `terraform plan`: lee el código y detectara los recursos que se crearan, dando un resumen de lo que se crea, modifica y lo que se destruye. Detecta algunos errores.
- `terraform apply`: lee y los crea. (crea la lista terraform.tfstate)
- `terraform destroy`: para eliminar la estructura (queda registrado en terraform.tfstate)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621183559.png)

# Terraform Estructura de código

- **Provider**: se le indica el proveedor nos permite conectar en la API de la nube.
- **Resource**:es un tipo de bloque, el tipo de lo que quiero crear
- **"aws_instance"**: es el tipo de recurso, que elemento especifico se usara
- **"web_server"** es el nombre que le colocaremos y el que usaremos al llamarlo en otras instancias del código. No es lo mismo que el nombre que se vera en la web.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621184859.png)

# Terraform Variables y escalabilidad
Se puede desglozar el main.tf para no tener código duplicado, para tener varios archivos con variables, facilitando la escalabilidad de las distintas áreas de IT. También tiene los Outputs que son los datos que se mostraran como IP o DNS o los id como SHA.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621185327.png)

# Terraform El dueño 





# Práctica: sawkl
### hsk

1. sdssdf:
	sdsld

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1JTKA_vuQOsyeQLswCFhQT1JZxoUxO3yd/view
