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

## 4. Direccionamiento Físico frente a Direccionamiento Lógico
* **Dirección MAC (Physical Address):** Identificador físico y permanente de 48 bits, grabado de fábrica en la ROM de la tarjeta de interfaz de red (NIC). Se expresa en formato hexadecimal y se utiliza para direccionar tramas localmente dentro del mismo segmento de red (Capa 2).
* **Dirección IP (Logical Address):** Dirección lógica de red asignada dinámicamente por software o manualmente. Permite el encaminamiento global de paquetes entre diferentes redes interconectadas del mundo (Capa 3).

## 5. Anatomía de la Trama Ethernet Estándar
La trama es la estructura de datos que circula por el cableado LAN. Sus campos obligatorios son:
1. **Preámbulo y SFD (7 + 1 Bytes):** Patrón de bits que permite la sincronización del reloj del receptor antes de que lleguen los datos.
2. **Dirección MAC Destino (6 Bytes):** Dirección física del adaptador de red que debe recibir la trama.
3. **Dirección MAC Origen (6 Bytes):** Dirección física del adaptador de red que emite la trama.
4. **Tipo / Longitud (2 Bytes):** Indica el protocolo de capa superior encapsulado (ej. `0x0800` para IPv4, `0x0806` para mensajes ARP).
5. **Datos / Carga útil (Payload):** El datagrama de red encapsulado. Posee un tamaño mínimo de 46 bytes y un máximo de 1500 bytes (MTU estándar).
6. **FCS / CRC (4 Bytes):** Secuencia de verificación de trama basada en un código de redundancia cíclica para descartar tramas corruptas.



* **Restricción de Tamaño Mínimo (64 Bytes):** Si una trama mide menos de 64 bytes (excluyendo el preámbulo), se detecta como un fragmento de colisión (*runt frame*) y el hardware la elimina inmediatamente.

## 6. Modos de Distribución del Tráfico
* **Unicast:** Tráfico direccionado estrictamente desde un emisor hacia un único receptor identificado por su dirección MAC.
* **Multicast:** Envío eficiente de datos desde un origen hacia un grupo específico de hosts que se han suscrito a una dirección especial.
* **Broadcast:** Difusión masiva de datos dirigida a **todos** los dispositivos del segmento de red local. Utiliza la dirección física destino universal `FF:FF:FF:FF:FF:FF`.

## 7. Protocolos de Resolución de Direcciones: ARP y RARP
* **ARP (Address Resolution Protocol):** Traduce o mapea una dirección lógica conocida (IP) a una dirección física de hardware (MAC) dentro de la misma LAN.
	* *Funcionamiento:* El host emisor envía un mensaje **ARP Request** en modo **Broadcast** preguntando por una IP específica. Todos lo reciben, pero solo el host con esa IP configurada responde con un **ARP Reply** en modo **Unicast** directo al emisor, revelando su dirección MAC.
	* *ARP Cache:* Tabla dinámica en memoria RAM que almacena los mapeos IP-MAC descubiertos temporalmente para no inundar la red con solicitudes constantes.
* **RARP (Reverse Address Resolution Protocol):** Realiza la función matemática inversa de ARP; permite a una máquina cliente averiguar su propia dirección IP a partir de su dirección física MAC conocida (usado históricamente en estaciones de trabajo sin disco duro).