
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

**Clase Grabada:** 

