# IaC - Terraform

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

# Terraform El dueño del estado terraform.tfstate
Todos los archivos .tf son todas las solucitudes que le pido a la nube, lo que deseo que este en aws. 
terraform.tfstate lo que hace es ser el intermediario entre lo que deseamos con la realidad, detalla lo que tenemos realmente y sus id. No se toque los terraform.tfstate por eso se modifica los parametros directamente desde el main.tf.  y cuidado con modificar desde la consola web porque tambien puede causar error ya que terraform.tfstate no tendria la realizad.
Al realizar destroit se crea un terraform.tfstate.backup por si fue un error. quedando terraform.tfstate en blanco o minimamente.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621191522.png)

# Terraform Evolución y adopción
En la práctica anterior teníamos un gran main.tf pero como vimos en el punto Terraform Variables y escalabilidad se puede estructurar. Para eso se generan varios archivos .tf, si necesito hacer algún cambio voy directo al archivo y área especifica.

También existe los tres pasos que se ven en la imagen para pasar una nube ya creada a terraform
1. Definir la carcasa: Escribir un bloque vació en el archivo .tf
	`resource "aws_instance" "server_web" {}

2. Captura vincular el nombre con el ID real de la nube (se coloca la secuencia de caracteres en id)
	`terraform import aws_instance.server_web "id"`

3. Extracción de ADN: leer el estado capturado para extraer los valores reales y rellenar el archivo HCL. Terraform es ahora el dueño.
	`terraform state show aws_instance.server_web`

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621192008.png)


---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1JTKA_vuQOsyeQLswCFhQT1JZxoUxO3yd/view
