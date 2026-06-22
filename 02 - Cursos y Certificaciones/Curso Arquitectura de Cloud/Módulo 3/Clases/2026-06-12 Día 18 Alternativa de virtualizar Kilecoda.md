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


---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1DU3FElrPddKHi_Kmgd3UC5vFOhSVIqIP/view?usp=sharing
