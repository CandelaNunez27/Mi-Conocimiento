
# Práctica: Terraform + Ansible en AWS
### Preparación

1. Tener:
	carpeta con archivo host.ini (el incentario dirección IP del ec2), main.tf (la estructura desplegada por terraform), deploy.yml (tareas y configuraciones que le indicaremos con ansible).
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622201953.png)
	

### Terraform

1.  Desplegar terraform
	Abrimos terminal en esa carpeta y ejecutamos`terraform init`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622215711.png)

2. Nos fijamos el resumen de lo que crearemos `terraform plan`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622220600.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622220638.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622220701.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622220740.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622220803.png)

3. Lo desplegamos con `terraform apply -auto-approve`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622222452.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622223605.png)
	
	Nos genera un archivo pem-lab-terraform.pem con la clave privada RSA.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622223057.png)

### Conexión ssm de aws

1. le damos a connectar con ssm a la ec2 creada
	Modificamos el rol de IAM por el que creamos en practicas anteriores, esperamos unos minutos a que se actualice.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622224024.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622224237.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622230236.png)
	
	Comprobamos que no tiene docker
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622231759.png)
	


### Ansible

1. En el paso anterior nos dio el output la ip publica y la key que la colocaremos en el archivo host.ini
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622223345.png)
	

2. Ejecutamos ansible con `ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i host.ini deploy.yml`
	El `ANSIBLE_HOST_KEY_CHECKING=False` es porque al hacer ssh hay una pregunta de yes/no y le colocamos este argumento para que se lo salte
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622231059.png)
	

3. Revisamos si se coloco la configuración de nginx y instalo docker
	Ahí vemos que a diferencia de antes si esta instalado docker 
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622231722.png)
	
	vemos si nos levanto el contonedor nginx
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622231954.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622232133.png)
	


### Borrar todo

1. `terraform detroy -auto-approve`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260622234424.png)



















---
# Guía del Profesor
# Laboratorio Integrado: Terraform + Ansible en AWS

## Módulo 3 - Clase 1: Despliegue de Infraestructura y Configuración Automatizada

  

### 🎯 Objetivo del Laboratorio

El alumno aprenderá a encadenar las dos herramientas fundamentales del ecosistema DevOps:

1. **Terraform (Aprovisionamiento):** Creará de forma declarativa una instancia EC2 en AWS con sus respectivas reglas de red.

2. **Ansible (Configuración):** Se conectará a la máquina creada por Terraform para instalar Docker y desplegar un contenedor de Nginx.

  

---

  

### 🗺️ Arquitectura del Flujo de Trabajo

[ Código .tf ] ──> ( Terraform Apply ) ──> Crea Instancia EC2 ──> Entrega IP Pública

│

▼

[ Código .yml ] <── ( Ansible Playbook ) <── [ hosts.ini ] <─────────────┘

  

---

  

### 📁 Estructura del Proyecto

Pídeles a los alumnos que creen la siguiente estructura de archivos en su carpeta de trabajo `ansible-docker-aws`:

```text

ansible-docker-aws/

├── main.tf # Código de Terraform para AWS

├── hosts.ini # Inventario de Ansible (IP destino)

└── deploy.yml # Playbook de Ansible
```

  # Paso a paso

  

## Ejecutar el terraform

  

## Reemplazar la IP publica (output del terraform) al archivo host.ini

  

## Aplicar el deploy de Ansible

  

ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i host.ini deploy.yml

  

## Verficar el correcto despliegue entrando en un navegador web a la ip publica

  

## Destruir toda la infraestructura con terraform









  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1y9Cwy3F8Jh41HV8sZbYVlvk-oFj0ROpM/view

