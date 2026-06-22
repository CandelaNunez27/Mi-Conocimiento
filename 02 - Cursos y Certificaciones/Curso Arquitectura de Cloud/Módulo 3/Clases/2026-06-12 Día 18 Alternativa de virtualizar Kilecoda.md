# Práctica: cómo instalar herramientas en consola 
### Instalar docker siguiendo la guía Digital Ocean

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04


1. `sudo apt upgrade
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205521.png)

2. `sudo apt update
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205637.png)

3. `sudo apt install ca-certificates curl gnupg
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205755.png)

4. 
```
   sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205940.png)

5. 
```
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210005.png)

6. `sudo apt update`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210115.png)

7. `sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210445.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210504.png)

### Instalar terraform

siguiendo guia de hashCoro Developer
https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

1. `sudo apt update && sudo apt install -y gnupg software-properties-common curl`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621211349.png)

2. `wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621211424.png)


3.  `echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621211504.png)

4.  `sudo apt update && sudo apt install terraform`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621211556.png)

5. `terraform -version`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621211633.png)

### Clonamos el github del profesor

1. `git clone https://github.com/juliangigena/course_ing_cloud.git`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621212207.png)

2. nos movemos a la carpeta de terraform
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621212506.png)

3. `systemctl status docker`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621212633.png)


### Instalar ansible

https://docs.ansible.com/projects/ansible/latest/installation_guide/installation_distros.html

1. `sudo apt update`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621213053.png)

2. `sudo apt install -y software-properties-common`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621213210.png)

3. `sudo add-apt-repository --yes --update ppa:ansible/ansible`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621213311.png)


4. `sudo apt install -y ansible`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621213516.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621213458.png)

5. `ansible --version`
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621213550.png)

### Instalar minikube

https://minikube.sigs.k8s.io/docs/start/?arch=%2Flinux%2Fx86-64%2Fstable%2Fbinary+download

1. 
```shell
curl -LO https://github.com/kubernetes/minikube/releases/latest/download/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube && rm minikube-linux-amd64
```
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621214530.png)

2. 
```shell
minikube start
```

Fin de muestra de preparación de entorno en killercode.

---

# Práctica: Despliegue de terreform  con docker, aws y import

### Preparación

1. tener instalado docker, terraform, minikube

2. Tener:
	Carpeta terraform-docker con un main.tf , outputs.tf , providers.tf , variables.tf
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621221309.png)

3. Abrir terminal en esa ubicación y ejecutar `terraform init`, que nos creara algunos archivos. 
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621221253.png)

4.  nos salio un error al darle `terraform plan` por ello tiramos `sudo chmod 666 /var/run/docker.sock`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621222035.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621222140.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621222216.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621222232.png)
	Por ende nos mostrara el id del container y una url de acceso.

5. `terraform apply -auto-approve` lo creara y ademas creara el terraform.tfstate
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621222737.png)
	
	Vemos el `docker ps` y ingresamos a la url desde un navegador
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621223012.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621223113.png)
	


### Qué pasa si se modifica el puerto

1. Nos vamos al archivo variables.tf y modificamos el puerto a 8081 -> 8082
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621223513.png)
	

2. `terraform plan` veamos que muestra y que cambio
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621223729.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621223750.png)
	Nos muestra que va a destruir para modificar

3. `terraform apply -auto-approve` `
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224040.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224122.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224151.png)
	

### Borrar

1. Mostramos como terraform.tfstate esta antes y despues de tirar `terrafrom destroy -auto-approve`
	terraform.tfstate cuando esta todo desplegado
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224525.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224558.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224630.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224715.png)
	
	terraform.tfstate despues de destroy
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224859.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621224913.png)
	

# Práctica: Despliegue de terreform  con aws

### Despliegue en terraform aws

1. nos movemos a la carpeta terraforms-aws




# Práctica: Despliegue de terreform  con import






---
# Guía del Profesor
# Terraform

Cuando trabajamos con Terraform de manera profesional en la industria, no escribimos todo en un único archivo gigante. En su lugar, dividimos el código en archivos especializados para maximizar la legibilidad, mantenibilidad y modularidad:

  

## providers.tf

Configura los requerimientos de la versión de Terraform y declara los proveedores (plugins) necesarios para comunicarse con las APIs del exterior (AWS, GCP, Docker, etc.). Separa el cómo nos conectamos de la infraestructura en sí.

  

## variables.tf

Declara las variables de entrada que el proyecto aceptará. Funciona como el "plano estructural" y los parámetros de configuración parametrizables, evitando escribir valores fijos (hardcoded) en el código.

  

## terraform.tfvars

Contiene las asignaciones de valores reales para las variables definidas en variables.tf. Nunca se debe subir a Git si contiene secretos o claves de acceso.

  

## main.tf

Es el núcleo operativo de nuestro despliegue. Aquí se declaran los recursos reales (máquinas virtuales, firewalls, redes, contenedores) que se van a construir.

  

## outputs.tf

Define la información que Terraform imprimirá en pantalla al terminar con éxito el aprovisionamiento de recursos. Se usa para extraer IPs públicas, URIs de bases de datos o IDs de recursos útiles para el usuario o para canalizaciones de CI/CD.


# Terraform-docker

docker-infra/

├── providers.tf

├── variables.tf

├── main.tf

└── outputs.tf

  

### 1. Crear y acceder a la carpeta del proyecto

mkdir docker-infra && cd docker-infra

  

### 2. Crear los 4 archivos descritos en el Canvas (providers.tf, variables.tf, main.tf, outputs.tf) con sus respectivos códigos

  

### 3. Inicializar el proveedor de Docker local

terraform init

  

### 4. Ver los recursos que se van a crear

terraform plan

  

# 5. Desplegar el contenedor de Nginx

terraform apply -auto-approve

  

# 6. Probar en tu navegador ingresando a http://localhost:8081

  

# 7. Destruir el contenedor y limpiar tu máquina local al finalizar la clase

terraform destroy -auto-approve


  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1DU3FElrPddKHi_Kmgd3UC5vFOhSVIqIP/view?usp=sharing
