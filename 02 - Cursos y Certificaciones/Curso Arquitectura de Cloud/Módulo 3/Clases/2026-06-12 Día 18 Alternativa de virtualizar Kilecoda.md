# Práctica: cómo instalar herramientas en consola 
### Instalar docker siguiendo la guía Digital Ocean

https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04


1. `sudo apt upgrade
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205521.png)

2. `sudo apt update
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205637.png)

3. `sudo apt install ca-certificates curl gnupg
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205755.png)

sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621205940.png)

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210005.png)

sudo apt update
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210115.png)

sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210445.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260621210504.png)




---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1DU3FElrPddKHi_Kmgd3UC5vFOhSVIqIP/view?usp=sharing
