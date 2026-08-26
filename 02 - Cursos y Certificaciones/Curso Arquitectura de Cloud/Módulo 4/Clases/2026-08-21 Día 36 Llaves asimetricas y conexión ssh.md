
# Práctica: Llave ssh y docker
### Preparación

1. Almacenamiento de contraseña:
	Creamos un dockerfile: FROM ubuntu:22.04, RUN apt-get update && apt-get insatall -y openssh-server sudo, RUN mkdir /var/run/sshd, RUN useradd -rm -d /home/admin -s /bin/bash -g root -G sudo adminlab, RUN echo 'adminlab:password_temporal_blanqueada' | chpassws, RUN mkdir -p /home/adminlab/.ss && chmod 700 /home/adminlab/.ssh, COPY id_demo_ssh.pub /home/adminlab/.ssh/authorized_keys, RUN chmod 600 /home/adminlab/.ssh/autorized_keys && chown -R adminlab:root /home/adminlab/.ssh, EXPONSE 22, CMD ["/usr/sbin/sshd","-D"]
	
	`cd` nos vamos a ~ (no hacer)
	`ssh-keygen -t ed25519 -C "demo-alumno@lab-cumplimiento" -f ~/.ssh/id_demo_ssh -N ""` para generar las doble claves privadas y publicas
	`ls -la` buscamos la carpeta .ssh `ls -ls .ssh/` veremos las llaves
	
	`cat .ssh/id_demo_ssh` y `cat .ssh/id_demo_ssh.pub`
	

2. Docker:
	
	Volvemos a la carpeta clase 2 DockerFile `docker build -t servidor-ssh-demo . --no-cahe`  ,`docker image ls` buildiamos la imagen
	
	`docker run -d --name contenedor_seguro -p 2222:22 servidor-ssh-demo` corremos la imagen y le abrimos el puerto 22 para poder conectarnos por ssh
	
	`docker ps` lista los docker activos
	
	`ssh -i ~/.ssh/id_demo_ssh -p 2222 adminlab@localhost` para conectarnos le damos yes y nos pedirá contraseña
	
	


3. Salio mal porque pedia contraseña
	Se copio un nuevo dockerfile y un archivo entrypoint.sh, se le dio permisos `chmod +x entrypoint.sh` , `ls -la` nos dara que tiene permisos de escritura.
	
	Ahora paramos y borramos el anterior docker `docker stop contenedor_seguro`, `docker ps`, `docker container prune`
	
	Ahora si corremos el que si anda, `docker build --no-cache -t servidor-ssh-demo .` , `docker run -d --name contenedor_seguro -p 2222:22 \ -e SSH_PUBLIC_KEY="${cat ~.ssh/id_demo_ssh.pub}" \ servidor-ssh-demo`
	
	Nos conectamos `ssh-keygen -R "[localhost]:2222" ` y `ssh -i ~/.ssh/id_demo_ssh -p 2222 adminlab@localhost`, Nos pregunrara si queremos conectarnos y le colocamos que yes y no nos pedirá contraseña
	


### Conectados:

1. ssh
	Dentro de la consola conectada podemos tirar `ls`, `pwd` y `exit` para salir
	Y no es lo mismo que conectarse por `docker exec -it contenedor_seguro bash` por que al ingresar tiramos `pwd` y veremos que el usuario es root. y dijimos queno se recomeinda usar el root. `exit`
	
	por ende volvemos a adminlab, dentro nos dejara crear por ejemplo `mkdir cande` y tendremos los permisos para hacerlo




---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1yE0C5jjxJ4NrJFoJpCutdfspo1p5KN9o/view
