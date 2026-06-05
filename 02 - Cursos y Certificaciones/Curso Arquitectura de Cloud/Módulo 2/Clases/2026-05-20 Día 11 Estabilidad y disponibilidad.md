# Fundamento Estabilidad
**La magia de la nube:** de servidores estáticos a ecosistemas inteligentes que respiran y crecen/decrecen según el ritmo de tu negocio.
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260605180824.png)

# Escalabilidad (vertical) vs Elasticidad (horizontal)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260605181115.png)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260605182546.png)

# Fundamento Objetivo Disponibilidad
**Uptime Garantizado:** Sistemas accesibles y confiables cerca del 100% del tiempo (99.9%)

# Métodos para volver a la disponibilidad

**High availability (99.9%):** mitigar fallos o estar uptime lo mayor de tiempo con dos servidores con un balanceador de carga que se configura como quiero que reparten las consultas en ambos servidores.

**Disaster Recovery (99.95%):** se busca lo rápido, tener una región preparada para hacer una transferencia hacia otro servidor para tener ya configurada.

**Fault Tolerance (100%):** en cambio de la anterior, esta las dos regiones están activas. Soy dos totalmente operativos.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260605182812.png)

# Administración tráfico Balanceadores de carga

**Application Load Balancer (ALB):** maneja el tráfico a nivel de aplicación (7),  maneja el tráfico web y se le indica que responda a la URL del balanceador en base a métodos y base a esos métodos elegís a que servidor enviarle la petición. Ej: miservidor.com/api va aun servidor y miservidor.com/web va al otro.

**Network Load Balancer (NLB):** maneja el tráfico a nivel de transporte (4), maneja todo el tráfico de red como TCP/UDP,  incluye el trafico de capa 7 para no tener tantos puertos abiertos, generando mejor rendimiento y sin latencia.

**Gateway/Classic Load Balancer:** maneja tráfico en capa de red, con una mezcla de transporte y aplicación (3, 4 y 7). Gateway es la administración a nivel de red con Firewalls (fortinet, ...)  y gateway inicial de capas más altas como Cloufer. Classic se puede poner varios balanceadores con sus gateways.

*Nota: estos nombres de los balanceadores son los nombres de los servicios de AWS*

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260605184153.png)




---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1FLVxqjMMr6-Ek0ZPO-ydB5j-z4-WavTJ/view
