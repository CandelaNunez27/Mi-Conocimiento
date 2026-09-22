
https://github.com/pedroA37/zonda-hpc-carla2026.git

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
	
	Pero para que este bien configurado el ssh y tenga especificado el usuario exacto para cada destino y evitar de tirar un comando tan largo especificando usuario junto con ip
	En ~/.ssh/config y debe quedar de esta manera.
	```
	Host nodo-1
	  HostName 10.2.13.1
	  User zonda-hpc1
	Host nodo-2
	  HostName 10.2.13.2
	  User zonda-hpc2
	Host nodo-3
	  HostName 10.2.13.3
	  User zonda-hpc3
	
	```
	
	Autorizar y copiar la clave pública nuevamente pero de manera automatica con script
	
	`nano scripts/03-shh-nodos.sh`
	
	```
	set -e
	[ -f ~/.ssh/id_ed25519 ] || ssh-keygen -t ed25519 -N "" -f ~/.ssh/id_ed25519
	grep -qf ~/.ssh/id_ed25519.pub ~/.ssh/authorized_keys 2>/dev/null || cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
	chmod 600 ~/.ssh/authorized_keys
	grep -q "Host nodo-\*" ~/.ssh/config 2>/dev/null || printf "Host nodo-*\n\tStrictHostKeyChecking accept-new\n" >> ~/.ssh/config
	chmod 600 ~/.ssh/config
	for n in nodo-2 nodo-3; do
		ssh-copy-id $n
		scp ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub ~/.ssh/config $n:.ssh/
	done
	for a in nodo-1 nodo-2 nodo-3; do
		for b in nodo-1 nodo-2 nodo-3; do
			ssh $a "ssh $b hostname" || echo "FALLA $a -> $b"
		done
	done
		
	```
	
	- **Generación de identidad:** Crea una clave SSH segura (`ed25519`) sin contraseña en caso de no existir y se auto-autoriza agregándola al archivo local `authorized_keys`.
	- **Evasión de confirmaciones:** Inyecta la regla `StrictHostKeyChecking accept-new` en la configuración SSH para que el sistema confíe automáticamente en las identidades de los demás nodos, evitando que los procesos en segundo plano se traben esperando a que el usuario escriba "yes".
	- **Clonación de credenciales:** Distribuye la llave pública (`ssh-copy-id`), la llave privada y la configuración hacia los Nodos 2 y 3 mediante `scp`, logrando que todos compartan la misma identidad y una conexión bidireccional.
	- **Diagnóstico de matriz (3x3):** Ejecuta un bucle de validación donde cada nodo intenta contactar a todos los demás de forma cruzada, confirmando que las 9 combinaciones posibles se conectan exitosamente sin mostrar la palabra "FALLA".
	


### Nodo 1 maestro (DNS, ANSIBLE, herramientas básicas, almacenamiento compartido NFS, IndiniBand)

1. Agregar dns, lo mismo en los otros nodos
	
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
	export TERM=xterm256color
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918102450.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918102507.png)
	
	Crear el arhivo de host
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918102521.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260921215710.png)
	
	`ansible all -i inventario.ini -m ping`para comprobar
	
	

4. Herramientas necesarias
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
	
	Lo ejecutamos en cada nodo desde el nodo 1  y luego reiniciar cada nodo individualmente
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
	

5. Creamos el almacenamiento compartido NFS para que nodo 2 y 3 lo vean como local
	`nano scripts/02-nfs.sh` para crear el script que comparta la carpeta `/sharedy` le colocamos lo siguiente. Evita tener que compilar HPL tres veces o copiar los binarios a mano nodo por nodo
	
	```
		#!/bin/bash
	set -e
	if [ "$(hostname -s)" = "nodo-1" ]; then
		sudo mkdir -p /shared
		sudo chown $USER: /shared
		echo "/shared 10.2.13.0/24(rw,sync)" | sudo tee /etc/exports
		sudo systemctl enable --now nfs-server
		sudo exportfs -ra
	else
		sudo mkdir -p /shared
		grep -q "nodo-1:/shared" /etc/fstab || echo "nodo-1:/shared /shared nfs defaults,_netdev 0 0" | sudo tee -a /etc/fstab
		sudo mount -a
	fi
	mkdir -p /shared/registros /shared/hpl-run /shared/src
		
		
	
	```
	
	**Condicional `if [ "$(hostname -s)" = "nodo-1" ];`:** El script verifica el nombre de la máquina. Si detecta que está corriendo en el `nodo-1`, actúa como el **Servidor NFS**. 
	* Crea la carpeta `/shared` y le asigna los permisos de tu usuario (`chown`).
	* Escribe en `/etc/exports` la orden de compartir esa carpeta exclusivamente con la subred del clúster (`10.2.13.0/24`). 
	* Inicia el servicio NFS (`systemctl enable --now nfs-server`) y aplica la configuración (`exportfs -ra`).
	
	**Sección `else`:** Si el script se ejecuta en los Nodos 2 o 3, actúan como **Clientes NFS**.
	 * Crean su propia carpeta `/shared` vacía. 
	 * Agregan una línea al archivo `/etc/fstab` indicando que deben montar la carpeta remota del Nodo 1 cada vez que arranquen (`nodo-1:/shared`).
	 * Ejecutan `mount -a` para conectar la carpeta inmediatamente
	 
	 **Carpetas finales:** Finalmente, crea tres subcarpetas dentro de `/shared` (`registros`, `hpl-run`, `src`) para organizar el código fuente y las pruebas.
	
	
	Lo ejecutamos en cada nodo desde el nodo 1
	`ssh nodo-1 'bash -s' < scripts/02-nfs.sh
	`ssh nodo-2 'bash -s' < scripts/02-nfs.sh
	`ssh nodo-3 'bash -s' < scripts/02-nfs.sh
	
	
	
	


6. Validación de la red InfiniBand 
	Para usar InfiniBand se necesita RDMA yUCX para que OpenMPI pueda enrutar el cálculo matemático por esta red.
	
	`nano scripts/04-ib.sh
	
	```
	#!/bin/bash
	set -e
	sudo dnf -y install rdma-core infiniband-diags perftest libibverbs-utils ucx ucx-ib
	ibstat
	ibv_devinfo | grep -E "hca_id|state|active_mtu"
	
	```
	
	Lo ejecutamos en cada nodo desde el nodo 1
	`ssh nodo-1 'bash -s' < scripts/04-ib.sh 
	`ssh nodo-2 'bash -s' < scripts/04-ib.sh
	`ssh nodo-3 'bash -s' < scripts/04-ib.sh
	
	Verificar que nos muestre: El puerto InfiniBand (`mlx5_0`) debe mostrar `State: Active` y `Physical state: LinkUp`. Si dice `Initializing`, hay un problema con la red de la organización y debes detenerte.
	

7. MKL () y MPI ()
	- **MKL (Intel oneMKL):** Es la **librería matemática** (una implementación de BLAS). En supercomputación, el benchmark HPL no hace las multiplicaciones de matrices por sí solo, sino que "llama" a esta librería para que las haga. Utilizar Intel oneMKL es una decisión de diseño crítica de tu equipo porque está hiperoptimizada para exprimir las instrucciones avanzadas **AVX-512** de los procesadores Intel Xeon Skylake de sus nodos, lo que disparará los GFLOPS. 
	
	* **MPI (Message Passing Interface):** Es el **estándar de comunicación**. Mientras MKL calcula rápido dentro de un solo nodo, MPI es el director de orquesta que divide la gran matriz inicial y envía los pedazos a través de la red hacia los Nodos 2 y 3 para que todos trabajen en paralelo. Decidimos usar **OpenMPI** configurado con la capa de transporte **UCX**, lo que obliga a MPI a enrutar todos esos pedazos matemáticos por los cables de altísima velocidad de **InfiniBand** (kernel bypass) en lugar de usar la red Ethernet lenta.
	
	`nano scripts/05-mkl-mpi.sh
	
	
	```
	
	#!/bin/bash
	set -e
	sudo tee /etc/yum.repos.d/oneAPI.repo >/dev/null <<EOF
	[oneAPI]
	name=Intel oneAPI repository
	baseurl=https://yum.repos.intel.com/oneapi
	enabled=1
	gpgcheck=1
	repo_gpgcheck=1
	gpgkey=https://yum.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB
	EOF
	
	sudo dnf -y install intel-oneapi-mkl-devel libfabric
	sudo dnf -y install openmpi openmpi-devel
	
	sudo tee /etc/profile.d/hpc.sh >/dev/null <<'EOF'
	export MKLROOT=/opt/intel/oneapi/mkl/latest
	export PATH=/usr/lib64/openmpi/bin:$PATH
	export LD_LIBRARY_PATH=/usr/lib64/openmpi/lib:$MKLROOT/lib:$LD_LIBRARY_PATH
	EOF
	
	```

	
	- **Repositorio Intel (`tee /etc/yum.repos.d/...`):** Le enseña al gestor de paquetes (`dnf`) de Rocky Linux dónde encontrar los servidores oficiales de Intel para poder descargar herramientas que no vienen por defecto en Linux.
	* **Instalación (`dnf install...`):** Descarga el paquete de desarrollo matemático (`intel-oneapi-mkl-devel`), la herramienta de comunicación (`openmpi`) y, de forma crucial, la dependencia de red `libfabric` que  faltaba en OpenMPI 5.0.9 para que funcionara correctamente
	* **Variables de Entorno (`/etc/profile.d/hpc.sh`):** Este es el paso más importante para que el clúster funcione. Exporta las rutas (`$PATH` y `$LD_LIBRARY_PATH`) donde se instalaron estas herramientas a nivel global
		 * *¿Por qué en `profile.d`?* Porque cuando OpenMPI lance procesos a los otros nodos de forma automática y transparente (sesiones no interactivas), esos procesos deben saber exactamente en qué carpeta de la computadora buscar la librería matemática MKL para poder hacer los cálculos. Si estuviera en un archivo local como `.bashrc`, la conexión remota podría fallar al no encontrar las herramientas.
	
	
	Lo ejecutamos en cada nodo desde el nodo 1
	`ssh nodo-1 'bash -s' < scripts/05-mkl-mpi.sh 
	`ssh nodo-2 'bash -s' < scripts/05-mkl-mpi.sh
	`ssh nodo-3 'bash -s' < scripts/05-mkl-mpi.sh
	
	Verificar que se haya instalado bien las librerías Inter oneMKL, lo ejecutamos en cada nodo desde el nodo 1
	`ssh nodo-1 'source /etc/profile.d/hpc.sh && ls -l $MKLROOT/lib/libmkl_core.so'
	`ssh nodo-2 'source /etc/profile.d/hpc.sh && ls -l $MKLROOT/lib/libmkl_core.so'
	`ssh nodo-3 'source /etc/profile.d/hpc.sh && ls -l $MKLROOT/lib/libmkl_core.so'
	
	Verificar que openMPI enrute el tráfico a través del puente InfiniBand (`mlx5_0`) y no por ethernet
	`source /etc/profile.d/hpc.sh
	`ompi_info --param pml ucx | grep -i ucx
	`mpirun -np 3 --host nodo-1,nodo-2,nodo-3 hostname
	`mpirun -np 2 --host nodo-1,nodo-2 --mca pml ucx -x UCX_NET_DEVICES=mlx5_0:1 -x UCX_TLS=rc,sm,self hostname
	
	_Si aparece el mensaje `plm:ssh: Warning: setpgid failed... Permission denied`, es un artefacto normal de las sesiones anidadas y no afecta la validez de la prueba.
	
	

8. Compilar HPL
	
	HPL (High-Performance Linpack) es el programa de benchmarking oficial de la competencia CARLA 2026 (y del Top500 global). Su única función es generar un sistema de ecuaciones lineales gigantesco y resolverlo, midiendo el rendimiento final en operaciones de punto flotante por segundo (GFLOPS). HPL no realiza los cálculos matemáticos pesados por sí mismo; actúa como un "director" que le entrega las piezas del rompecabezas a MPI para que las distribuya por la red y a la librería BLAS (en nuestro caso, Intel oneMKL) para que haga las multiplicaciones de matrices a máxima velocidad.
	
	`nano scripts/06-build-hpl.sh
	
	```
	#!/bin/bash
	set -e
	source /etc/profile.d/hpc.sh
	cd /shared/src
	
	# Descargar y extraer el código fuente
	[ -f hpl-2.3.tar.gz ] || wget https://www.netlib.org/benchmark/hpl/hpl-2.3.tar.gz
	rm -rf hpl-2.3
	tar xzf hpl-2.3.tar.gz
	cd hpl-2.3
	
	# Configurar la compilación para Intel Skylake AVX-512 y OpenMP
	./configure CC=mpicc \
	  CFLAGS="-O3 -march=skylake-avx512 -fopenmp" \
	  LDFLAGS="-L$MKLROOT/lib -Wl,--no-as-needed -fopenmp" \
	  LIBS="-lmkl_intel_lp64 -lmkl_gnu_thread -lmkl_core -lgomp -lpthread -lm -ldl" \
	  --prefix=/shared/opt/hpl
	  
	# Compilar en paralelo usando los 36 núcleos del nodo
	make -j 36
	make install
	
	# Verificación de librerías enlazadas
	ldd /shared/opt/hpl/bin/xhpl | grep -i mkl
	
	# Copiar el binario localmente a todos los nodos (Plan B por si falla el NFS)
	for n in nodo-1 nodo-2 nodo-3; do
	  ssh $n "sudo mkdir -p /opt/hpl/bin && sudo cp /shared/opt/hpl/bin/xhpl /opt/hpl/bin/"
	done
	
	```
	
	* **Preparación (`source...`):** Carga las variables de entorno configuradas previamente (rutas de OpenMPI y MKL) y se sitúa en la carpeta compartida (`/shared/src`) para evitar compilar tres veces
	* **Descarga:** Obtiene y extrae el código fuente oficial de HPL 2.3 desde la web de netlib.
	* **Configuración Avanzada (`./configure`):** * Usa el compilador de MPI (`CC=mpicc`).
		* Añade banderas de optimización extrema (`CFLAGS="-O3 -march=skylake-avx512 -fopenmp"`) para instruir al compilador a generar instrucciones específicas que exprimen el hardware Intel Xeon Skylake de los nodos.
		* Enlaza el benchmark contra la librería Intel oneMKL en modo multihilo (`LIBS="-lmkl_intel_lp64... -lgomp..."`), delegando las multiplicaciones de matrices pesadas a este motor matemático.
	* **Compilación Paralela:** Ejecuta `make -j 36` para utilizar todos los núcleos físicos del nodo-1 simultáneamente, agilizando la construcción, y `make install` para colocar el binario resultante (`xhpl`) en la carpeta compartida.
	* **Verificación de Cumplimiento:** Ejecuta `ldd` sobre el binario `xhpl` y filtra por "mkl" para auditar y confirmar que el programa quedó enlazado a las librerías dinámicas correctas del fabricante.
	* **Respaldo Local (Plan B):** El bucle final copia el ejecutable desde la carpeta de red (`/shared`) hacia el disco local de cada uno de los tres nodos (`/opt/hpl/bin`). Esto garantiza que, si el servidor NFS falla el día de la competencia, el clúster pueda seguir ejecutando el benchmark.
	

9. Scripts de corrida
	
	nos ubicamos en `/shared/hpl-run/` para crear los dos script
	
	`nano gen_dat.sh` Este script recibe los parámetros por consola (tamaño de matriz $N$, tamaño de bloque $NB$, cuadrícula $P$ y $Q$) y construye dinámicamente el archivo `HPL.dat` que el binario necesita leer antes de iniciar.
	
	```
	#!/bin/bash
	# uso: ./gen_dat.sh N "NBs" P Q "BCASTs" "DEPTHs" > archivo.dat
	N=$1; NB=$2; P=$3; Q=$4; BC=${5:-1}; DE=${6:-1}
	cat <<EOF
	HPLinpack benchmark input file
	Zonda-HPC
	HPL.out      output file name (if any)
	6            device out (6=stdout,7=stderr,file)
	1            # of problems sizes (N)
	$N           Ns
	$(echo $NB | wc -w)            # of NBs
	$NB          NBs
	0            PMAP process mapping (0=Row-,1=Column-major)
	1            # of process grids (P x Q)
	$P           Ps
	$Q           Qs
	16.0         threshold
	1            # of panel fact
	2            PFACTs (0=left, 1=Crout, 2=Right)
	1            # of recursive stopping criterium
	4            NBMINs (>= 1)
	1            # of panels in recursion
	2            NDIVs
	1            # of recursive panel fact.
	1            RFACTs (0=left, 1=Crout, 2=Right)
	$(echo $BC | wc -w)            # of broadcast
	$BC          BCASTs (0=1rg,1=1rM,2=2rg,3=2rM,4=Lng,5=LnM)
	$(echo $DE | wc -w)            # of lookahead depth
	$DE          DEPTHs (>=0)
	2            SWAP (0=bin-exch,1=long,2=mix)
	64           swapping threshold
	0            L1 in (0=transposed,1=no-transposed) form
	0            U  in (0=transposed,1=no-transposed) form
	1            Equilibration (0=no,1=yes)
	8            memory alignment in double (> 0)
	EOF
	
	```
	
	- **Inyección de parámetros:** Recibe variables matemáticas críticas por consola (tamaño de matriz $N$, tamaño de bloque $NB$ y la cuadrícula de procesos $P$ y $Q$) y las inserta directamente en el formato estricto que exige Linpack.
	- **Ejecución de pruebas múltiples:** Permite recibir listas de valores para los parámetros de ajuste fino ($NB$, BCAST y DEPTH). Utiliza el comando `wc -w` para contar dinámicamente cuántas opciones ingresaste y estructura el archivo para que HPL evalúe todas esas combinaciones de forma secuencial en una sola corrida, ahorrando tiempo durante la fase de tuning.
	
	`chmod +x gen_dat.sh` dar perimsos de ejecución
	
	luego el otro script también debe estar en `/shared/hpl-run/ ` 
	
	`nano run.sh` Este script lanza OpenMPI, limpia la memoria caché de los nodos antes de cada corrida para asegurar mediciones justas, fuerza el tráfico por la capa UCX/InfiniBand, y extrae los GFLOPS resultantes a un archivo `resultados.csv`
	
	```
	
	#!/bin/bash
	# uso: BIOS=fabrica ./run.sh <archivo.dat> <nodos> <procesos_por_nodo> <hilos_por_proceso> [local]
	# ej:  BIOS=fabrica ./run.sh prueba.dat nodo-1,nodo-2,nodo-3 2 18
	set -e
	IBDEV=mlx5_0
	DAT=$1; NODOS=$2; PPN=$3; HILOS=$4; MODO=${5:-shared}
	BIOS=${BIOS:-sin-dato}
	SELLO=$(date +%m%d-%H%M%S)
	NNODOS=$(echo $NODOS | tr ',' '\n' | wc -l)
	NP=$((NNODOS * PPN))
	HOSTS=$(echo $NODOS | sed "s/\([^,]*\)/\1:$PPN/g")
	if [ "$MODO" = "local" ]; then
		XHPL=/opt/hpl/bin/xhpl; RAIZ=$HOME/hpl-run
	else
		XHPL=/shared/opt/hpl/bin/xhpl; RAIZ=/shared/hpl-run
	fi
	DIR=$RAIZ/corridas/$SELLO
	mkdir -p $DIR
	cp $DAT $DIR/HPL.dat
	cp $(readlink -f $0) $DIR/run.sh
	echo "BIOS=$BIOS $0 $@" > $DIR/comando.txt
	for n in $(echo $NODOS | tr ',' ' '); do
		ssh $n "mkdir -p $DIR; sync; echo 3 | sudo tee /proc/sys/vm/drop_caches >/dev/null; echo 1 | sudo tee /proc/sys/vm/compact_memory >/dev/null"
	done
	cd $DIR
	mpirun -np $NP --host $HOSTS \
		--map-by ppr:$((PPN / 2)):package:PE=$HILOS --bind-to core --report-bindings \
		--mca pml ucx -x UCX_NET_DEVICES=$IBDEV:1 \
		-x OMP_NUM_THREADS=$HILOS -x MKL_NUM_THREADS=$HILOS -x MKL_DYNAMIC=false \
		-x OMP_PROC_BIND=close -x OMP_PLACES=cores -x LD_LIBRARY_PATH \
		$XHPL 2> bindings.txt | tee salida.txt
	PASO=$(grep -c PASSED salida.txt || true)
	awk -v s=$SELLO -v b=$BIOS -v p=$PPN -v h=$HILOS -v ok=$PASO \
		'/^WR/ {print s","b","p","h","$2","$3","$4","$5","$6","$7","ok}' salida.txt >> $RAIZ/resultados.csv
	grep -E "^WR|PASSED|FAILED" salida.txt
		
		
		
	
	```
	
	
	- **Configuración y Directorios:** Recibe los parámetros de entrada (archivo `.dat`, nodos, procesos por nodo e hilos) y crea una carpeta única basada en la fecha y hora (`corridas/<sello>`) para guardar de forma ordenada los archivos de cada ejecución.
	- **Preparación del Hardware:** Se conecta por SSH a cada nodo involucrado para limpiar la caché del sistema (`drop_caches`) y compactar la memoria RAM (`compact_memory`) antes de arrancar, asegurando que cada prueba comience en igualdad de condiciones.
	- **Lanzamiento Paralelo (OpenMPI):** Ejecuta el binario `xhpl` usando `mpirun`, forzando el tráfico de red a través de la interfaz InfiniBand (`mlx5_0`) mediante la capa UCX y aplicando una asignación estricta de procesos e hilos a los núcleos físicos (`--bind-to core`).
	- **Registro de Métricas:** Analiza la salida de la ejecución, verifica si superó la prueba de validación (`PASSED`) y extrae automáticamente los datos de rendimiento (como los GFLOPS y el tiempo) para añadirlos a un archivo acumulativo (`resultados.csv`).
	
	
	darle permisos de ejecución `chmod +x run.sh`
	
	Luego para que no nos salte el error del buffer RDMA por falta de memoria, tirar
	
	`for n in nodo-1 nodo-2 nodo-3; do
	  `ssh $n "echo -e '* soft memlock unlimited\n* hard memlock unlimited' | sudo tee /etc/security/limits.d/99-hpc-memlock.conf"
	`done
	

10. Primeras pruebas 
	primera prueba con solo un nodo:
	
	situarnos en la carpeta compartida `cd /share/hpl-run/` y tirar
	`./gen_dat.sh 40320 384 1 2 > n1.dat 
	
	`BIOS=fabrica ./run.sh n1.dat nodo-1 2 18
	
	verificar que la salida diga **PASSED** indicando un residuo seguro por debajo del umbral. (Debería dar alrededor de **120.07 GFLOPS**). 
	
	segunda prueba con los tres nodos:
	`./gen_dat.sh 40320 384 2 3 > n3.dat
	`BIOS=fabrica ./run.sh n3.dat nodo-1,nodo-2,nodo-3 2 18
	
	verificar que la salida diga **PASSED** y aproximadamente **338.02 GFLOPS**. Esto demuestra un ~93.8% de eficiencia de escalado contra el nodo individual, lo que certifica que la interconexión RDMA/UCX funciona sin cuellos de botella.
	
	
	

11. Tunnig y Corrida de rendimiento (fases a a f)
	
	la Fase A (Línea base formal con el BIOS de fábrica o de HPC con el tamaño de problema grande N=80640) y la Fase B, C, D, E, F (Tuning y Corrida Grande). El objetivo de este paso es llevar el clúster al límite de su rendimiento midiendo el impacto de los parámetros de HPL y la distribución de hilos/procesos.
	
	#### 1. Fase A: Línea base formal ($N = 80640$)
	
	Se ejecutan dos configuraciones extremas para tener una referencia inicial con el tamaño de matriz grande (~85% de la RAM del nodo).
	
	  

- **Lanzar la prueba híbrida (2 procesos por nodo, 18 hilos cada uno):**

    
    `./gen_dat.sh 80640 384 2 3 > base-2x18.dat
    `BIOS=tuneado ./run.sh base-2x18.dat nodo-1,nodo-2,nodo-3 2 18
    
    
- **Lanzar la prueba plana (36 procesos por nodo, 1 hilo cada uno):**
    
    _Nota: Como esta corrida toma varios minutos, se recomienda desacoplarla de la sesión SSH usando `nohup` y `setsid` para evitar que se interrumpa si se cierra la terminal._
    
    `setsid nohup ./run.sh base-36x1.dat nodo-1,nodo-2,nodo-3 36 1 > base-36x1.out 2>&1 &
    
    _Verificación:_ Una vez finalizada, revisa que el archivo `resultados.csv` contenga las líneas correspondientes y que los puntajes muestren el estado **PASSED**. Guarda una copia de respaldo del archivo de datos ganador como `HPL-fabrica.dat` en `/shared/hpl-run/`.
    
	#### 2. Fase B: Verificación y Respaldo del BIOS
	
	Los nodos HPE iLO permiten guardar y restaurar la configuración de hardware (como la desactivación del Hyperthreading para evitar pérdida de ciclos en AVX-512).
	
	  

- **Verificar el estado actual del BIOS desde el bastión:**
    
    ```
    ilorest login 10.1.13.1 -u scct-2613 -p '<PASS_BMC>'
    ilorest select Bios.
    ilorest get WorkloadProfile ProcHyperthreading PowerRegulator SubNumaClustering
    ```
    
- **Realizar el respaldo (Backup) de los 3 nodos:**

    ```
    for i in 1 2 3; do
      ilorest login 10.1.13.$i -u scct-2613 -p '<PASS_BMC>'
      ilorest save --selector Bios. -f bios-nodo-$i.json
      ilorest logout
    done
    ```
    
    _Verificación:_ Comprueba que se hayan generado los archivos `bios-nodo-1.json`, `bios-nodo-2.json` y `bios-nodo-3.json`.
	
	
	#### 3. Fase C: Tuning de Procesos por Nodo vs. Hilos
	
	Consiste en barrer diferentes combinaciones de paralelismo para encontrar el punto óptimo donde la factorización del panel no deje núcleos esperando.

- **Generar y ejecutar la grilla ganadora de 36 procesos por nodo con 1 hilo ($P=9, Q=12$):**
    
    ```
    ./gen_dat.sh 80640 384 9 12 > c-36x1.dat
    BIOS=tuneado ./run.sh c-36x1.dat nodo-1,nodo-2,nodo-3 36 1
    ```
    
    _Verificación:_ Abre el archivo `bindings.txt` dentro de la carpeta de la corrida en `corridas/<sello>/` para confirmar que los procesos MPI estén correctamente distribuidos y anclados a los núcleos físicos sin solaparse.
	
	#### 4. Fase D y E: Ajuste de Bloque ($NB$) y Broadcast ($BCAST$)
	
- **Barrido de tamaños de bloque ($NB$) con la configuración ganadora:**
   
    ```
    ./gen_dat.sh 80640 "192 256 336 384" 9 12 > d-nb.dat
    BIOS=tuneado ./run.sh d-nb.dat nodo-1,nodo-2,nodo-3 36 1
    ```
    
    _Verificación:_ Analiza los GFLOPS resultantes en el archivo `resultados.csv` para identificar qué tamaño de bloque (por lo general $NB=192$ o $256$) exprime mejor la caché y las instrucciones vectoriales.
    
	#### 5. Fase F: Corrida Grande Final
	
	Con todos los parámetros optimizados ($N$ escalado, $NB$ ideal, grilla $P \times Q$ y procesos de 1 hilo), se ejecuta la prueba de alta carga que simula la entrega final.
	
- **Lanzar la corrida de gran escala (ej. $N=161280$):**
    
    
    ```
    ./gen_dat.sh 161280 192 9 12 > f-final.dat
    BIOS=tuneado ./run.sh f-final.dat nodo-1,nodo-2,nodo-3 36 1
    ```
    
- **Monitorear el rendimiento de la CPU y la frecuencia real en otra terminal:**
    
    ```
    ssh nodo-2 sudo turbostat --quiet --show Busy%,Bzy_MHz --interval 30
    ```
    
    _Verificación:_ El resultado final de la corrida debe indicar **PASSED**, registrando un puntaje competitivo en GFLOPS (por encima de los 2100 GFLOPS en este hardware) y una eficiencia lógica adecuada frente al $R_{peak}$ teórico del clúster.
	
	

12. Reinicio
	El objetivo de este paso es comprobar que el clúster es totalmente autónomo y que, tras un reinicio completo de las tres máquinas simultáneamente, todos los servicios críticos (red, NFS, InfiniBand y el entorno de HPL) se levantan solos y sin intervención manual.
	
	Configurar para que el sistema sea persistente
	`nano scripts/07-sistema.sh`
	
	```
	
	#!/bin/bash
	# Paso 11 del plan - sistema persistente (correr en cada nodo, requiere reinicio después).
	set -e
	sudo systemctl enable --now tuned
	sudo tuned-adm profile throughput-performance
	sudo grubby --update-kernel=ALL --args="transparent_hugepage=always"
	echo "Falta: sudo reboot para que transparent_hugepage=always tome efecto."
	
	
	```
	
	- **`tuned` y perfil de rendimiento:** Habilita el demonio gestor de energía y rendimiento del sistema operativo, fijando el perfil `throughput-performance` para forzar al procesador a mantener un rendimiento elevado.
	- **`grubby` (_Transparent Hugepages_):** Actualiza los argumentos de arranque del kernel para habilitar `transparent_hugepage=always`, lo cual mejora la eficiencia en el manejo de bloques grandes de memoria RAM utilizados por el benchmark.
	
	
	
	Ejecutar en los 3 nodos desde nodo-1
	`chmod +x scripts/07-sistema.sh
	
	`for n in nodo-1 nodo-2 nodo-3; do
	 ` ssh $n 'bash -s' < scripts/07-sistema.sh
	`done
	
	
	reinicio limpio en los nodos
	`for n in nodo-1 nodo-2 nodo-3; do ssh $n "sudo systemd-run --on-active=1 --unit=hpc-reboot-final reboot" & done; wait
	
	
	`nano scripts/check.sh`Para comprobar de forma rápida que todos los componentes críticos del clúster volvieron a subir por sí solos, se utiliza el script de chequeo.
	
	```
	
	#!/bin/bash
	# Paso 11 del plan - chequeo post-reinicio. Correr desde nodo-1.
	for n in nodo-1 nodo-2 nodo-3; do
	    echo "== $n"
	    ssh $n 'ip -4 -br a show eno1np0; df -h /shared | tail -1; ls /opt/hpl/bin/xhpl; ibstat | grep -E "State|Rate"; systemctl is-active chronyd tuned; tuned-adm active; cat /sys/kernel/mm/transparent_hugepage/enabled; nproc'
	done
	ssh nodo-1 'systemctl is-active nfs-server'
	
	
	
	```
	
	- **Red y NFS:** Verifica que la interfaz Ethernet `eno1np0` tenga IP asignada, que el recurso compartido `/shared` esté montado correctamente como cliente NFS en los nodos 2 y 3, y que el servidor NFS esté activo en el nodo 1.
    - **Binarios y Respaldo:** Confirma la presencia del binario local `xhpl` en `/opt/hpl/bin/` en cada máquina como medida de contingencia.
    - **InfiniBand:** Ejecuta `ibstat` para validar que el dispositivo `mlx5_0` se encuentra en estado `Active` con un _Rate_ de 100 Gb/s.
    - **Servicios del Sistema:** Comprueba que `chronyd` y `tuned` estén activos, que el perfil de rendimiento esté aplicado, que las páginas de memoria transparentes estén habilitadas y que el sistema detecte los 36 núcleos físicos (_Hyperthreading_ desactivado).
	
	
	Otorgar permisos `chmod +x scripts/check.sh
	
	Ejecutar comprobación
	`/scripts/check.sh
	
	
	Última confirmación de una corrida cn el parámetro ganador
	`cd /shared/hpl-run/
	`./gen_dat.sh 40320 384 1 2 > confirmacion.dat
	`BIOS=tuneado ./run.sh confirmacion.dat nodo-1,nodo-2,nodo-3 2 18
	
	**Resultado esperado:** La ejecución debe finalizar indicando **PASSED** en aproximadamente 13 segundos, lo que confirma de manera definitiva que el clúster se recupera de un reinicio completo sin pérdida de estabilidad ni rendimiento
	
	