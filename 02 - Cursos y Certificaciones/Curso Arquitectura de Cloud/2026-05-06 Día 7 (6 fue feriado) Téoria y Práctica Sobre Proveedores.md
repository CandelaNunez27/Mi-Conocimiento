**Clase Grabada**: https://drive.google.com/file/d/1YZODY4eklbJaPUicdFIWvrWA1DU-G5e6/view?usp=sharing

# Fundamentos: ¿Nube si o no?

Depende, si necesito arrancar y no tengo los dispositivos físicos, entonces si. Sino hibrida. evaluando el contexto de la empresa. El arquitecto de la nube moderno no se casa con un proveedor, se casa con la eficiencia, a resiliencia y el costo-beneficio del negocio.

# Comparativa: Proveedores
#### Los tres grandes

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260506235915.png)

#### Dominio y especialización

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507000159.png)

#### Perfiles y fortalezas

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507000419.png)

#### Infraestructura base

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507000757.png)

#### Modelos IA generativa

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507001341.png)

#### FinOps (Técnicas para ser lo más eficiente económicamente)

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507002004.png)

# Multicloud: Caso de Uso

El marketing de compras tuyo analizando tus interacciones para mostrarte otro contenido que te pueda interesar.
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507002336.png)

---
# Práctica

Se ingreso ha *aws* y se configuro un *VPC* y se vieron conceptos de la clase pasada en la web.
Viene una VPC por defecto que recomienda no borrarla. Contiene un mapa de de recursos con subredes y tablas de conexión que están totalmente abiertas al gateway, por ende no es recomendable usar esta como vpc porque esta toda expuesta.

#### Crear VPC

- Nombre: mi-vpc
- CIDR IPv4: 10.0.0.0/16
- Crear Subred Pública:
	- Nombre: public-subnet-1
	- Seleccionar zona: EEEUU
	- Bloque de CIDR de VPC IPv4: 10.0.0.0/16
	- Bloque de CIDR de la subred IPv4: 10.0.1.0/24
	- Se puede agregar tags como "ventas"
- Crear Subred Privada:
	- Nombre: private-subnet-1
	- Seleccionar zona: EEEUU
	- Bloque de CIDR de VPC IPv4: 10.0.0.0/16
	- Bloque de CIDR de la subred IPv4: 10.0.2.0/24
	- Se puede agregar tags como "data"

#### Crear Servicios Instancia EC2

- Nombre: ec2-1
- ISO: (Ubuntu, Amazon Linux, macOS, Windows, Red Hat, SUSE Linux, Debian)
- Seleccionar hardware disponible:  64 bit, CPU 2 Nucleos, 4GB RAM
- Se puede poner contraseña a la maquina
- Network Settings:  
	- Seleccionar vpc:  mi-vpc
	- Subnet: public-subnet-1
	- Auto asignacion de ip pública: activado
	- Customizar que ip o quienes pueden conectarse con la maquina
- Se puede generar el script para que se crea la maquina automáticamente (como una receta).
- Todo esto se puede hacer por consola, o se puede ejecutar ese script receta en consola. (profesor lo mostrara en la siguiente clase).
- 