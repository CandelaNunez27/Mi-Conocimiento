### Preparación de Virtualización en hipervisor

1. Paquetes necesarios
	`sudo pacman -Syu qemu-full virt-manager virt-viewer dnsmasq openbsd-netcat swtpm iptables-nft`
	![](data:image/png;base64,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)

2. Activar los servicios necesarios:
	Una vez que termine la instalación, activar el motor de las máquinas virtuales
	`sudo systemctl enable --now libvirtd`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260902023808.png)

3. Permisos de usuario
	Agrega tu usuario al grupo `libvirt` para que no tengas que usar la contraseña de root cada vez que abras el programa 
	
	`sudo usermod -aG libvirt,libvirt-host $USER`
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260902024859.png)
	
	Luego cerrar sesión o reiniciar PC para que se apliquen los cambios.
	

3. ISO y Gestor de Máquinas Virtuales
	Antes de seguir descargamos Rocky Linux 9 (Minimal ISO) desde https://rockylinux.org/download (activar vpn en ee.uu para una descarga rápida)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260903230535.png)

4. Gestor de Máquinas Virtuales
	Luego del reinicio, en las Apps nos saldra una llamada Gestor de Máquinas Virtuales (virt-manager) la cual abriremos
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904013234.png)
	
	
	**nodo-master (Servicios, Ansible y Compilación Base)**: Le damos a crear nueva maquina virtual > Medio de instalación local > siguiente > seleccionamos la iso que descargamos > siguiente > memoria 3815 MiB y 2 nucleos de CPU > siguiente> dejar marcaado "habilitar almacenamiento para la mv" y asignar 20 GiB > siguente  > marcamos personalizar configuración antes de instalar > en red le colocamos  
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904013405.png) 
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904013706.png) 
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904014548.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904014909.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904015622.png)
	
	
	Como nos salia la nat inactiva la activamos con este comando `sudo virsh net-start default` y `sudo virsh net-autostart default` para que arranque cada vez que prenda la computadora.
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904015422.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904015552.png)
	
	Para que deje de salir inactiva una vez ya acticada cancele todo y volve a realizar los pasos.
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904015811.png) 
	Luego nos sale un menu de configuración avanzada. Donde nos nos vamos a CPU > y nos aseguramos que este marcada la opción Copiar configuración de la CPU del anfitrión (host-passthrough) > iniciar la instalación
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904020310.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904020339.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904021026.png)
	
	Creamos las otras maquinas virtuales con el mismo hardware y el mismo proceso. Por ende nos quedara las tres maquinas virtuales listas para usar (nodo-master, nodo-calculo1, node-calculo2) 

5. Instalación de Rocky linux minimal 9.8
	Arrancamos la maquina node-master y nos saldra con interfaz gráfica la instalación.
	Seleccionamos idioma Español (Argentina) > seleccionamos teclado > creación de usuario > hpc-user , LocalHPC-1234, marcamos Hacer de este usuario un administrador > Luego en contraseña de root le cole que la misma > selecionamos el disco de 20 y que quede en las particionado automatico > en red le colocamos el nombre del equipo nodo-master y la red > configurar...> ajustes de IPv4 > manual, añadir , direccion: 192.168.122.10, mascara: 255.255.255.0 , puerta de enlace: 192.168.122.1, DNS: 8.8.8.8 > guardar y conectar. Volvemos al menu del resumen de instalación y le damos a Comenzar la instalación.
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904022215.png)
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904022503.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904022318.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904022939.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904023418.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904023649.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904024851.png) 
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904024449.png)  
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904025019.png)
	
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260904025238.png)
	
	
	
	
	