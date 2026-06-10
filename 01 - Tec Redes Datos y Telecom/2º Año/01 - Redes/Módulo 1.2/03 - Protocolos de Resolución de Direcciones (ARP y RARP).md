# Cuestionario Técnico de Taller: Capa de Enlace de Datos (AT02)

Esta nota contiene la resolución detallada y formal del cuestionario de la Actividad de Taller Nº 2.

### 1. Tamaño mínimo y máximo de la trama Ethernet
* **Tamaño Mínimo:** **64 bytes** (sin contabilizar el preámbulo ni el delimitador de inicio de trama SFD). Cualquier trama menor se descarta como *runt frame*.
* **Tamaño Máximo Estándar:** **1518 bytes** (puede extenderse a 1522 bytes si se incorpora la etiqueta de control 802.1Q de las VLANs).

### 2. Tecnologías Ethernet Históricas y Actuales
* **10Base-T (Ethernet Clásico):** Opera a 10 Mbps sobre cable de par trenzado de cobre.
* **100Base-TX (Fast Ethernet):** Opera a 100 Mbps, introduciendo mejoras de codificación sobre cobre.
* **1000Base-T (Gigabit Ethernet):** Opera a 1000 Mbps (1 Gbps) utilizando los cuatro pares del cable UTP simultáneamente.
* **Tecnologías Actuales:** En entornos de acceso LAN de usuarios se estandariza **Gigabit Ethernet (1 Gbps)**, mientras que en centros de datos, enlaces troncales y redes troncales empresariales se emplean enlaces de **10 Gbps, 40 Gbps y 100 Gbps** sobre soportes de fibra óptica o cobre especializado.

### 3. Definición de MTU (Maximum Transmission Unit)
La MTU representa la unidad máxima de transferencia. Especifica el tamaño máximo en bytes del paquete de la capa superior (datos útiles provenientes de la Capa 3) que una trama de la capa de enlace puede transportar en el canal físico sin fragmentarse. Para Ethernet estándar, el valor de la MTU es estrictamente **1500 bytes**.

### 4. Qué es una Interfaz Loopback
Es una interfaz de red puramente virtual y lógica implementada por software en el sistema operativo (asociada por defecto a la IP `127.0.0.1` en IPv4). Su propósito principal es realizar diagnósticos internos, desarrollo de software local y verificar que la pila de protocolos TCP/IP del sistema está operando correctamente de forma interna sin requerir hardware físico de red activo.

### 5. Significado de Auto-Sensing (Autonegociación)
Es una función de hardware de las placas de red (NIC) que les permite comunicarse automáticamente con el dispositivo del otro extremo del cable para negociar de mutuo acuerdo la mayor velocidad de transmisión compatible (ej. 10/100/1000 Mbps) y el modo de operación más eficiente (Half-Duplex o Full-Duplex), previniendo fallos por desajuste de velocidad.

### 6. Diferencia Estructural entre un Hub y un Switch
* El **Hub (Concentrador - Capa 1)** es un dispositivo pasivo y ciego; recibe impulsos eléctricos por un puerto y los replica hacia todos los demás puertos activos, generando constantes colisiones y saturando la red.
* El **Switch (Conmutador - Capa 2)** posee lógica de procesamiento; lee las direcciones MAC destino de las tramas y las redirige de manera inteligente y selectiva **únicamente por el puerto físico donde está conectado el destinatario real**, eliminando las colisiones mediante la microsegmentación.

### 7. Tipos de Switches Existentes y sus Diferencias
*(Ver detalles extendidos de diseño en la Nota 2 de este módulo).* Los tipos principales incluyen switches de acceso (borde), switches multicapa (con capacidades de enrutamiento de Capa 3), switches apilables (unión lógica de chasis) y switches de grado industrial (reforzados para entornos hostiles).

### 8. Definición de Dominio de Colisión y Dominio de Difusión
* **Dominio de Colisión:** Segmento físico de una red de datos donde los paquetes pueden chocar entre sí si dos o más hosts transmiten simultáneamente sobre el mismo medio conductor.
* **Dominio de Difusión (Broadcast Domain):** Área lógica de la red de datos hasta donde se propaga un mensaje enviado a la dirección física de broadcast universal (`FF:FF:FF:FF:FF:FF`).

### 9. ¿El Switch divide dominios de colisión o de difusión?
El switch **SÍ divide los dominios de colisión** debido a que cada puerto físico individual crea un canal independiente y cerrado de comunicación hacia el host final (Microsegmentación). Sin embargo, el switch estándar **NO divide dominios de difusión**; por defecto, todos sus puertos físicos integran el mismo dominio de difusión general.

### 10. ¿El Router divide dominios de colisión o de difusión?
El router **SÍ divide los dominios de difusión** debido a que las interfaces lógicas de Capa 3 bloquean de manera estricta el paso de los mensajes de broadcast, impidiendo que congestionen otras subredes externas. Adicionalmente, al aislar los segmentos físicos de red, también divide de forma implícita los dominios de colisión.

### 11. ¿Qué es una colisión en Ethernet y qué ocurre cuando se produce una?
Una colisión es la superposición física de dos o más señales electromagnéticas en un medio de transmisión compartido, provocando la corrupción de los bits y volviendo la información ilegible. Cuando ocurre en entornos Ethernet tradicionales (Half-Duplex), las tarjetas de red detectan el pico de voltaje anómalo mediante el protocolo **CSMA/CD**, detienen la transmisión de datos, emiten una señal de atasco (*jam signal*), esperan un intervalo de tiempo aleatorio basado en un algoritmo de postergación y reintentan la transmisión.

### 12. Qué es un Jumbo Frame y en qué casos conviene usarlo
Son tramas Ethernet modificadas diseñadas para transportar una carga útil (MTU) muy superior al estándar de 1500 bytes, alcanzando habitualmente valores de hasta **9000 bytes**. 
* *Aplicación:* Conviene utilizarlos exclusivamente en redes de almacenamiento masivo (SAN), clústeres de cómputo o datacenters. Al encapsular más datos por trama, se generan menos cabeceras de red por gigabyte transmitido, lo cual reduce drásticamente el uso y la sobrecarga de la CPU de los servidores en transferencias de gran volumen.

### 13. Definición de Unicast, Multicast y Broadcast
* **Unicast:** Transmisión de datos dirigida desde un único emisor hacia un único receptor identificado de forma unívoca en la red.
* **Multicast:** Distribución eficiente de tráfico desde un origen común hacia un grupo selecto de receptores configurados para escuchar una dirección específica (uno a muchos).
* **Broadcast:** Difusión masiva de un mensaje de datos emitido desde un origen hacia **todos** los dispositivos que integran el mismo segmento o dominio de red local.

### 14. Propósito de ARP y RARP y su Funcionamiento
* **ARP (Address Resolution Protocol):** Traduce una dirección lógica conocida (IP) a la dirección física de hardware (MAC) del adaptador destino para poder encapsular la trama localmente. Funciona mediante solicitudes ARP Request (Broadcast) y respuestas ARP Reply (Unicast).
* **RARP (Reverse Address Resolution Protocol):** Realiza la función inversa de ARP. Permite que un host consulte y obtenga su dirección IP en la red a partir de su dirección física MAC conocida (común en el arranque de terminales sin disco duro).



### 15. ¿En qué capa del modelo TCP/IP se ubica el protocolo ARP?
En el modelo conceptual de capas TCP/IP, el protocolo ARP se clasifica formalmente dentro de la **Capa de Internet (Red)**, debido a que trabaja directamente con las estructuras y direcciones lógicas de Capa 3, aunque actúa como interfaz operativa interactuando de forma estrecha con la Capa de Acceso a Red (Enlace).

### 16. Encapsulación y Formato del Mensaje ARP
Los mensajes ARP no se transportan dentro de un paquete IP. Se encapsulan **directamente dentro del campo de datos de una trama Ethernet estándar**. Para indicar que la carga útil contiene información de resolución de direcciones, se coloca el valor hexadecimal **`0x0806`** en el campo *Type* de la cabecera Ethernet.

### 17. Tipos de Operaciones posibles en un Mensaje ARP
El propósito del mensaje ARP se determina mediante el campo de código de operación (*Opcode*) en su cabecera. Los dos tipos esenciales son:
* **Opcode 1 (ARP Request / Solicitud):** Mensaje de consulta enviado en modo broadcast por el host origen.
* **Opcode 2 (ARP Reply / Respuesta):** Mensaje de respuesta enviado en modo unicast por el host destino dueño de la IP consultada.

### 18. Ejemplo del comando `arp -a` en Linux
Al ejecutar el comando en la consola de comandos de Linux, el sistema operativo despliega la tabla interna en memoria de las direcciones físicas aprendidas:

```bash
$ arp -a
? (192.168.1.1) at 00:1a:2b:3c:4d:5e [ether] on eth0
? (192.168.1.50) at a4:b2:c3:d4:e5:f6 [ether] on eth0
```

Muestra las direcciones IP de la LAN mapeadas con sus respectivas MAC físicas asignadas y el nombre de la interfaz de red por la cual se comunicaron.

## Part 2: Procedimiento Práctico (Taller de Wireshark)

Pasos seguidos en el laboratorio para capturar y analizar el tráfico de Capa de Enlace:

1. Se inició **Wireshark** con privilegios de administrador.
    
2. Se identificó la interfaz activa (ej. `eth2` o `Wi-Fi`) observando la gráfica de picos de tráfico en tiempo real.
    
3. Se inició la captura y se ejecutó en la consola del sistema operativo el comando de diagnóstico para identificar el Gateway o router: `ip route` o `route -n`.
    
4. Se procedió a realizar un `ping` hacia la IP del router resuelta (ej. `ping 172.22.32.1`).
    
5. En Wireshark, se aplicó el filtro `arp` o `icmp` para aislar los paquetes del taller. Se pudo verificar visualmente en la ventana de inspección de Wireshark cómo la trama Ethernet encapsula perfectamente los mensajes ARP utilizando el Type `0x0806` y cómo las direcciones MAC de origen y destino cambian de Broadcast a Unicast entre el Request y el Reply.