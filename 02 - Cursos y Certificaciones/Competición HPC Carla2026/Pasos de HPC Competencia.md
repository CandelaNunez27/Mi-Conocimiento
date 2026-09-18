
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
	
	Volvemos a conectarnos al bastión y desde ahí nos conectaremos a los nodos
	`ssh scct-2613@bastion.tail263e10.ts.net` junto con `ssh zonda-hpc1@10.2.13.1
	
	Nodo-2:
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918024850.png)
	
	Nodo-3:
	![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260918025213.png)
	



`