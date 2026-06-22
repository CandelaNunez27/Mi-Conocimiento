# Teoría: sawkp

# Fundamentos sdjaksl



# Práctica: sawkl
### Preparación

1. sdssdf:
	sdsld

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

