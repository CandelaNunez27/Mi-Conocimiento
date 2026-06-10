# Capa de Enlace de Datos: Ethernet, MAC, ARP y RARP

## 1. Preguntas Introductorias de la Capa de Enlace

* **¿Cómo se comunican las terminales y los equipos de red entre ellos?** La comunicación se realiza de terminal a terminal de forma local a través de enlaces individuales.

* **¿Cómo se encapsulan los datagramas?** Los datagramas de la capa de red (Capa 3) se encapsulan dentro del campo de datos de las **tramas (frames)** correspondientes a la capa de enlace (Capa 2) para su transporte físico.

* **¿Proporcionan los protocolos una transferencia de datos fiable router a router?** Depende del protocolo de enlace utilizado. Algunos proporcionan entrega fiable mediante confirmaciones y retransmisiones (común en enlaces inalámbricos propensos a fallos), mientras que otros (como Ethernet cableado) no lo hacen para evitar sobrecarga, delegando la fiabilidad a capas superiores (TCP).

* **¿Pueden utilizarse diferentes protocolos en una misma ruta?** Sí. Un paquete IP puede viajar a través de múltiples enlaces físicos distintos, utilizando un protocolo de enlace diferente en cada uno (por ejemplo, Wi-Fi en el primer salto, Ethernet en el núcleo y PPP en el enlace WAN).

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609235058.png)

## 2. Clasificación Fundamental de Canales de Comunicación

* **Canales de Difusión (Broadcast Channels):** Presentes en redes de área local (LAN), LAN inalámbricas (Wi-Fi), redes satelitales y redes de acceso híbridas de fibra y cable coaxial (HFC). Al compartir un único medio físico entre múltiples hosts, es indispensable usar un **protocolo de acceso al medio (MAC)** para coordinar las transmisiones y prevenir colisiones de datos.

* **Canales Punto a Punto (Point-to-Point):** Conexión exclusiva entre dos dispositivos conectados de forma directa (por ejemplo, el enlace serie entre dos routers o la conexión de un módem residencial hacia el router del ISP). Al no compartirse el soporte físico, no existen colisiones de tramas.

## 3. Servicios Principales de la Capa de Enlace

Dependiendo del protocolo utilizado, la capa de enlace puede ofrecer:

* **Entramado (Framing):** Encapsulación de cada datagrama de red añadiendo una cabecera (*header*) y una cola (*trailer*) que delimitan el inicio y fin de la trama.

* **Acceso al Enlace:** Regulación y control del uso del canal en redes de difusión (protocolos MAC).

* **Entrega Fiable:** Garantía de que los datos crucen el enlace sin errores. (reconocimientos ACK)

* **Control de Flujo:** Mecanismo para evitar que un emisor rápido sature la capacidad de recepción de un host más lento.

* **Detección de Errores:** Identificación de bits alterados por ruido o atenuación mediante el uso de bits de paridad, sumas de comprobación o códigos de redundancia cíclica (CRC).

* **Corrección de Errores:** Capacidad de identificar y reparar errores de bits directamente en el receptor sin requerir una retransmisión de la trama.

## 4. Implementación de la Capa de Enlace

A diferencia de los protocolos de capas superiores que corren puramente en software dentro del Sistema Operativo, la capa de enlace se implementa principalmente en el **hardware** del dispositivo, específicamente en el **Adaptador de Red (NIC - Network Interface Card)**. Este adaptador se conecta al bus del sistema y combina componentes de hardware, firmware y software (drivers).
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260610003312.png)

## Introducción a Ethernet

Ethernet es la tecnología por cable dominante en el mundo LAN. Evolucionó desde un medio compartido primitivo hasta las conexiones conmutadas actuales de alta velocidad (Gigabit y superiores), estandarizadas por la IEEE.

## Acceso a un medio compartido

Originalmente, Ethernet utilizaba un único cable coaxial donde todos transmitían. Para gestionar el caos de que dos equipos hablasen a la vez, se diseñó el protocolo **CSMA/CD (Acceso Múltiple por Detección de Portadora y Detección de Colisiones)**:
1. Escuchar el canal antes de transmitir. 
2. Si está libre, transmitir.
3. Si ocurre una colisión (dos transmiten a la vez), se detecta el choque eléctrico, se detiene la transmisión, se envía una señal de atasco y se espera un tiempo aleatorio antes de reintentar.
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260610012833.png)


## Funcionamiento de Ethernet

Ethernet es un protocolo **no orientado a la conexión y no fiable**. No realiza un "saludo de manos" previo antes de enviar tramas, y si una trama llega corrupta a destino, la placa de red simplemente la descarta sin avisar; la responsabilidad de recuperar ese dato se delega a capas superiores (como TCP en Capa 4).

## Tipos de redes Ethernet

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260610013037.png)
* **1000Base-T (Gigabit Ethernet):** 1000 Mbps, el estándar actual en la mayoría de los dispositivos locales. 

## Power Over Ethernet (PoE)

Estándar que permite enviar **corriente eléctrica continua (DC)** junto con los datos a través de los mismos hilos de cobre del cable de red de par trenzado. Esto elimina la necesidad de fuentes de alimentación externas para dispositivos como cámaras IP o teléfonos VoIP. 

## Direcciones MAC

* Es la dirección física de la Capa 2. 

* Tiene un tamaño de **48 bits** (6 bytes) expresados habitualmente en formato hexadecimal (ej. `AA:BB:CC:11:22:33`). 

* Viene grabada de fábrica de forma permanente en la ROM de la placa de red, garantizando que no existan dos tarjetas con la misma MAC en todo el mundo. 

## ARP (Address Resolution Protocol)

Protocolo crítico para el funcionamiento de la red local. Su único propósito es **traducir una dirección IP conocida a su correspondiente dirección MAC física**. 
* Si un equipo quiere enviar un paquete a una IP pero no conoce su MAC, envía un mensaje **ARP Request en modo Broadcast** (a todos).

* El dueño de esa IP responde con un **ARP Reply en modo Unicast** enviando su MAC física. Esta relación se guarda temporalmente en la tabla *ARP Cache*. 

## RARP (Protocolo de Resolución de Dirección Inversa)

Hace exactamente el proceso opuesto a ARP: permite que un dispositivo que conoce su dirección física MAC pueda consultar y averiguar qué dirección IP se le ha asignado en la red. Era usado históricamente por terminales viejas que no tenían disco duro para arrancar. 

## Switches vs Routers

* **Switches:** Equipos de **Capa 2**. Interconectan dispositivos dentro de una misma red local, analizan e interconectan tramas basándose en **direcciones MAC** y operan de forma automática (Plug and Play). 

* **Routers:** Equipos de **Capa 3**. Interconectan redes completamente diferentes, analizan paquetes basándose en **direcciones IP** y requieren una configuración manual explícita de sus interfaces y tablas de ruteo.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260610014234.png)