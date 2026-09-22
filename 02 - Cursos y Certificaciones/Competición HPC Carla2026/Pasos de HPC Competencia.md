
### Preparación

1. Crear cuenta en https://tailscale.com/

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001118.png)

2. Usa el siguiente enlace para agregar el host bastión a tu red de Tailscale: **[https://login.tailscale.com/admin/invite/SFneanC8udULcaAz7ymb11](https://login.tailscale.com/admin/invite/SFneanC8udULcaAz7ymb11)** 
   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001236.png)
   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001302.png)
   
   3. Descargar desde **[https://tailscale.com/download](https://tailscale.com/download)** 
	   `curl -fsSL https://tailscale.com/install.sh | sh` 
	   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001445.png)
	   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001512.png)
	   
	   iniciamos sesión en la consola
	   `sudo tailscale up
	   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001841.png)
	   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001854.png)
	   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001905.png)
	   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916001935.png)

4. Nos conectamos al bastion por ssh con su nombre de dominio completo:
	`ssh scct-2613@bastion.tail263e10.ts.net` 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916002516.png)
	

5. Puente ssh para la red del BMC:
	nodo  1 : 10.1.13.1
	nodo  2 : 10.1.13.2
	nodo  3 : 10.1.13.3
	
	Ahora creamos un "puente" a través del bastión para alcanzar la interfaz de administración (BMC) del Nodo 1, abrir nueva terminal : `ssh -L 8000:10.1.13.1:443 scct-2613@bastion.tail263e10.ts.net`
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916005243.png)
	
	Luego en el navegador buscar `https:\\localhost:8000
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916005423.png)
	
	Ingresamos con nuestras credenciales proporcionadas por los organizadores:
	- Usuario: scct-2613
	- Password: -
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916005850.png)
	
	


6.  ISO:
	En la consola donde tiramos el primer ssh descargamos la iso `wget https://mirror.hnd.cl/rockylinux/10.2/isos/x86_64/Rocky-10.2-x86_64-minimal.iso`
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916020402.png)

7. Lenvantar el servidor HTTP:
	Montar la iso descargada e instalarla. Primero tiramos el comando `python3 -m RangeHTTPServer 8013 --bind 10.7.12.102`en la primera consola, el puerto y la ip del bastión local es asignada por la organización. si sale error instalar el módulo faltante con `python3 -m pip install --user RangeHTTPServer
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916024441.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916024522.png)
	
	Ahora si, ngresando a https:\\localhost:8000 nos vamos a Remote Console & Media -> Virtual Media -> Connect CD/DVD-ROM -> virtual media URL = http://10.7.12.102:8013/Rocky-10.2-x86_64-minimal.iso -> Insert media
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916024911.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916024929.png)
	


### Acceder al Nodo 1

1. Consola remota HTML5
	Ir a Remote Console & Media -> Launch -> HTML5 Console (Abrira una nueva pastaña con el servidor apagado), logo de iLO 5 -> Power -> momentary press
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916025613.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916025802.png)
	
	Cuando aparezcan las opciones del teclado apretar F11 para ingresar a la lista de booteo. Elegir iLO Virtual CD-ROM.
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916025921.png) 
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916030234.png)
	
	Luego seleccionar del GRUB la opcion Install Rocky Linux Minimal 10.2
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916030418.png)
	

2. Completar los pasos de instalación:
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918011809.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916031226.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916031528.png)   
	
	
	Reclamar espacio
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916031538.png)
	
	
	
	Eliminar todo y reclamar espacio
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916031600.png)  
	
	contraseña de root 
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918014725.png) 
	
	
	creación de usuario
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918014826.png)
	
	red y nombre de equipo: activar la interfaz eno1np0 y colocamos el nombre nodo-1 no lo hacemos
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916032937.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918015018.png)
	
	Le damos a comenzar instalacion
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916033251.png) 
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916033950.png)
	
	al terminar mostrara la consola
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260916034330.png)
	



### Acceso a los otros nodos

1. Tunel para cada uno
	Tener tres consolas corriendo
	`ssh -L 8000:10.1.13.3:443 scct-2613@bastion.tail263e10.ts.net
	`ssh -L 8001:10.1.13.3:443 scct-2613@bastion.tail263e10.ts.net
	`ssh -L 8002:10.1.13.3:443 scct-2613@bastion.tail263e10.ts.net
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918004322.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918004338.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918004350.png)
	
	Ir al navegador y para cada una tener su ventana
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918004427.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918004437.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918004455.png)
	
	y hacemos los mismos pasos de cargarele la url de la iso, pero antes asegurarse que este corriendo
	`ssh scct-2613@bastion.tail263e10.ts.net` junto con `python3 -m RangeHTTPServer 8013 --bind 10.7.12.102`


1. Los mismos pasos de configuracion:
	Se sigue los mismos pasos que el nodo 1
	nodo2:
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918012107.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918012526.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918012704.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918012719.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918013916.png)
	
	nodo 3:
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918020722.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918020523.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918020623.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918022328.png)
	
	
	

### Establecer comunicación sin contraseñas entre nodos

1. Colocarles las IP a los Nodos 
	
	Nodo-1:
	En la interfaz web una vez dentro de nodo-1 usamos `sudo nmtui
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918024009.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918023425.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918023518.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918023919.png)
	
	Reiniciamos el servicio
	`sudo systemctl restart NetworkManager`
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918024222.png)
	
	o en la consola evitando que se borre la ip 
	`sudo nmcli connection modify eno1np0 ipv4.method manual ipv4.addresses 10.2.13.1/24 ipv4.gateway 10.2.13.254 connection.autoconnect yes
	`sudo nmcli connection up eno1np0
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918033452.png)
	
	
	Aunque le forzamos que levante la  interfaz 
	`sudo nmcli connection up eno1np0
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918030134.png)
	
	Volvemos a conectarnos al bastión y desde ahí nos conectaremos a los nodos
	`ssh scct-2613@bastion.tail263e10.ts.net` junto con `ssh zonda-hpc1@10.2.13.1
	
	Nodo-2:
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918024850.png)
	
	o en la consola evitando que se borre la ip 
	`sudo nmcli connection modify eno1np0 ipv4.method manual ipv4.addresses 10.2.13.2/24 ipv4.gateway 10.2.13.254 connection.autoconnect yes
	`sudo nmcli connection up eno1np0
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918032659.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918032717.png)
	
	
	
	
	Nodo-3:
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918025213.png)
	
	
	o en la consola evitando que se borre la ip 
	`sudo nmcli connection modify eno1np0 ipv4.method manual ipv4.addresses 10.2.13.3/24 ipv4.gateway 10.2.13.254 connection.autoconnect yes
	`sudo nmcli connection up eno1np0
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918034036.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918034051.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918030851.png)
	
	Volvemos a conectarnos al bastión y desde ahí nos conectaremos a los nodos
	`ssh scct-2613@bastion.tail263e10.ts.net` junto con `ssh zonda-hpc1@10.2.13.1 , ssh zonda-hpc2@10.2.13.2  . ssh zonda-hpc3@10.2.13.3
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918034126.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918033010.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918034231.png)
	


2. Generar ssh para que se comuniquen sin contraseñas entre los nodos
	Nodo-1 (maestro)
	`ssh-keygen -t ed25519`
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918034640.png)
	
	Se las copiamos a los otros nodos desde el Nodo-1
	`ssh-copy-id zonda-hpc2@10.2.13.2
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918034949.png)
	
	
	`ssh-copy-id zonda-hpc3@10.2.13.3
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918035026.png)
	
	Para comprobar `ssh zonda-hpc2@10.2.13.2` y  `ssh zonda-hpc3@10.2.13.3` estando dentro del Nodo 1. Deberías entrar instantáneamente al Nodo 2 sin contraseña.
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918035256.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918035409.png)
	


### Nodo 1 maestro (DNS, ANSIBLE, )

1. Agregar dns
	
	`sudo nmcli connection modify eno1np0 ipv4.dns 8.8.8.8 
	`sudo nmcli connection up eno1np0
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918095645.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918095802.png)
	

2. Descargar e instalar ansible
	`sudo dnf install epel-release -y
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918095905.png)
	
	refrescamos el repositorio por tirar error `sudo dnf makecache`y tiramos `sudo dnf install ansible-core -y`
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918100344.png)
	`ansible --version
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918100458.png)
	

3. Ansible
	descargar nano y saltar error
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918102450.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918102507.png)
	
	Crear el arhivo de host
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918102521.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260921215710.png)
	
	`ansible all -i inventario.ini -m ping`para comprobar
	
	

3. Herramientas necesarias
	 Crearemos un script donde nos descargara lo necesario para la seguridad, red y dependencias para compilar y ejecutar software HPC
	 - **Validación y Actualización:** Verifica la conexión a internet con `curl`, actualiza el sistema base y descarga compiladores (como GCC) requeridos para compilar HPL desde cero.
	- **Dependencias Críticas:** Instala `numactl` para el manejo de memoria NUMA, `environment-modules` para controlar versiones de software y `nfs-utils` para permitir el almacenamiento en red.
	- **Red y Sincronización:** Mapea las IPs locales en `/etc/hosts` para la comunicación de OpenMPI, unifica los relojes de los nodos con `chronyd` y abre el cortafuegos exclusivamente para el tráfico de la subred interna.
	- **Seguridad:** Bloquea el acceso remoto (SSH) al superusuario root.
	- **Parche InfiniBand:** Fija el parámetro `memlock` como ilimitado para que la red de alta velocidad (UCX/RDMA) pueda mover grandes bloques de memoria sin abortar los procesos.
	- **Aplicación de Cambios:** Ejecuta un reinicio (`reboot`) para garantizar que el servidor arranque utilizando el nuevo kernel instalado en el primer paso.
	
	`nano scripts/01-base.sh
	
	```
		#!/bin/bash
	# Paso 4 del plan - base comun. Correr en cada nodo:
	#   ssh nodo-N 'bash -s' < scripts/01-base.sh
	set -e
	curl -sI https://dl.rockylinux.org | head -1
	sudo dnf -y update
	sudo dnf -y groupinstall "Development Tools"
	sudo dnf -y install wget git tar rsync numactl numactl-devel hwloc pciutils environment-modules chrony nfs-utils tuned kernel-tools python3
	for h in "10.2.13.1 nodo-1" "10.2.13.2 nodo-2" "10.2.13.3 nodo-3"; do
		grep -q "$h" /etc/hosts || echo "$h" | sudo tee -a /etc/hosts
	done
	echo "PermitRootLogin no" | sudo tee /etc/ssh/sshd_config.d/10-noroot.conf
	sudo systemctl restart sshd
	sudo systemctl enable --now chronyd
	sudo firewall-cmd --permanent --zone=trusted --add-source=10.2.13.0/24 || true
	sudo firewall-cmd --reload
	# memlock para RDMA/UCX (encontrado en la practica el 18/09, no estaba en la receta original)
	printf "* soft memlock unlimited\n* hard memlock unlimited\n" | sudo tee /etc/security/limits.d/99-hpc-memlock.conf
	echo "Falta: sudo reboot (kernel nuevo de dnf update)."
	```
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260921230254.png)
	
	Ejecutarlo en todos los nodos y luego reiniciar
	``ssh nodo-1 'bash -s' < scripts/01-base.sh``
	`ssh nodo-2 'bash -s' < scripts/01-base.sh
	`ssh nodo-3 'bash -s' < scripts/01-base.sh
	
	`sudo systemd-run --on-active=1 --unit=hpc-reboot reboot`en cada nodo para reiniciar y que la sesión ssh actual se cierre limpiamente.
	
	Luego para verigicar que todo haya salido bien se tira este comando en todos los nodos
	`lscpu; numactl -H; free -g; grep MemTotal /proc/meminfo; lspci | grep -i -E "mellanox|infiniband"` 
	
	- **`lscpu`**: Verifica que el sistema detecte los 36 núcleos físicos, la presencia de las instrucciones avanzadas `avx512f`, y permite confirmar si el Hyperthreading está desactivado (si estuviera activo, mostraría 72 CPUs).
	- **`numactl -H`**: Comprueba la topología de la memoria para asegurar que el sistema operativo identifica correctamente los 2 nodos NUMA de los procesadores.
	- **`free -g` y `grep MemTotal /proc/meminfo`**: Validan que la memoria RAM total detectada ronde los 192 GB esperados para cada nodo.
	- **`lspci | grep -i -E "mellanox|infiniband"`**: Confirma que el bus PCI del servidor reconozca físicamente la tarjeta de red de alta velocidad (Mellanox/InfiniBand) necesaria para la interconexión del clúster.
	
	




