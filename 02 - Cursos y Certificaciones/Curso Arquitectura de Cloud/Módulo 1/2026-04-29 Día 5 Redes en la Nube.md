**Clase Grabada**: https://drive.google.com/file/d/15Ck5ZFR4TvNEgqXuhTc0Vh2UQ4SfeUXl/view?usp=sharing 

**Páginas para virtualizar:**
https://killercoda.com/ terminal con laboratorios (Linux, grafana, ... ).
https://labex.io/ terminal con interfaz con laboratorios (Linux, cybersecurity, ....) dura una 1 hs y se va renovando.

# Fundamentos: VPN (Virtual Private Network)

Blindaje de Conexión: Crea un túnel cifrado entre tu dispositivo y un servidor remoto.
- Proteger Datos: Cifrado de información sensible.
- Trabajo Remoto: Acceso seguro a recursos internos.
- Evitar Rastreo: Oculta la Actividad e IP del ISP (proveedor).

# Fundamentos: Principios de la Nube

- Múlticuenta en un Tenant (empresas).
- Múltiples regiones en una cuenta para elegir virtualizar, cada una con distinta disposición de hardware.
- Múltiples zonas (datacenters) en una región, estarán entre ellas interconectadas para evitar que si un datacenter se prende fuego no se perderá los datos.

# Fundamentos: Red Virtual (Virtual Network Nube)

Se deben separar para mayor organización como departamentos en un edificio (*VPC Isolated Cloud Resources*) y se empezara a trabajar en el apartado de Red.
- Sección aislada de la nube donde tienes el control total del entorno.
- Control total sobre IPs, subredes y tablas de ruteo.

# Arquitectura: Pilares de Redes Cloud

Elementos vitales para que la infraestructura sea operativa.
- **CIDR**: Rango de direcciones IP.
- **Subnets**: Segmentación lógica.
- **Route Tables**: El "GPS" del tráfico.
- **Gateways**: Puertas de entrada y salida.

# Seguridad: Segmentación Crítica

Se debe separar lo público de lo privado, y tráfico interno controlado como vpn o cable para la comunicación entre ellas.
- Pública: Tráfico directo desde Internet, aloja lo que puede ser visible (Balancadores (distribuye el trafico de los varios servidores)y Servers Web).
- Privida: Accesible únicamente desde el interior de la red, aloja recursos críticos (Bases de datos RDS/SQL y Microservicios).

# Seguridad: Defensa en Profundidad

La seguridad se gestiona en capas concéntricas:
- **IAM**: Identidad como perímetro.
- **NACL**: Firewall a nivel Subred (Stateless).
- **Security Groups**: Firewall a nivel Instancia (Stateful)
![](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260506232858.png)

# Ejemplo de Lab Arquitectura en 2 capas

![](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260506233233.png)

