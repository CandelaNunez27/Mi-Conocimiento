# Conmutación Ethernet y Arquitectura de Redes

## Funcionamiento básico: qué es un switch?

Los switches Ethernet enlazan dispositivos entre sí copiando tramas desde un puerto de entrada hacia un puerto de salida. A diferencia del router (que encamina paquetes analizando IPs de Capa 3), el switch se maneja en **Capa 2**, aislando el tráfico localmente y requiriendo nula configuración inicial para tareas básicas.

## Direcciones y tabla de reenvío

El switch basa sus decisiones en una tabla interna almacenada en la memoria RAM llamada **Tabla MAC o Tabla de Reenvío**. Esta tabla asocia de forma dinámica cada dirección MAC física del entorno con el número de puerto del switch donde se encuentra conectada.

## Aprendizaje de direcciones

El switch crea su tabla de forma automática mediante la inspección del tráfico entrante: cada vez que una trama ingresa por un puerto físico, el switch lee el campo de la **MAC de origen** y la anota en la tabla junto al número de puerto. De esta forma, "aprende" dónde está parado cada equipo.

## Inundación de tramas

Si una trama entra al switch buscando una MAC de destino que **no figura** todavía en la tabla de reenvío, el dispositivo realiza una copia de la trama y la **inunda (flooding)** enviándola por todos y cada uno de los puertos activos, excepto por el puerto por el cual ingresó originalmente.

## Tráfico Unicast, Broadcast y Multicast: Usos

* **Unicast:** Envío de información desde un único emisor directo hacia un único receptor.

* **Broadcast:** Dirigido a la dirección `FF:FF:FF:FF:FF:FF`. El switch está obligado a inundarlo por todos sus puertos. Se usa obligatoriamente para protocolos de descubrimiento como ARP o DHCP.

* **Multicast:** Dirigido a un grupo selecto de interfaces. El tráfico se reenvía de forma eficiente únicamente a los puertos que se hayan suscrito a dicho grupo (ej. IPTV o replicación de servidores).

## Combinando switches

En infraestructuras reales, un solo switch no basta. Los switches se pueden interconectar entre sí mediante cables de red tradicionales para expandir la cantidad de bocas disponibles, uniendo los puertos de un switch a otro (uplink).

## Spanning Tree Protocol (STP)

Al combinar múltiples switches, los administradores suelen tirar cables duplicados para tener conexiones de respaldo. Esto genera bucles físicos (bucles de red) donde las tramas de broadcast se duplican infinitamente destruyendo el rendimiento. **STP (estándar 802.1D)** es un protocolo que detecta estos bucles de forma lógica y **apaga/bloquea temporalmente los puertos redundantes**. Si el cable principal se corta, STP reactiva el puerto de respaldo automáticamente.

## Rendimiento de un switch

El rendimiento global de la red conmutada se mide por su ancho de banda interno y su velocidad para procesar millones de tramas por segundo (throughput) sin generar demoras de cola o cuellos de botella.

## Desempeño en el reenvío de tramas

Existen tres modos en los que el switch gestiona las tramas entrantes:
* **Store-and-Forward:** Almacena la trama completa, calcula el código de error CRC y si está limpia la envía. Es el más seguro pero lento.

* **Cut-Through:** Lee solo los primeros 6 bytes (MAC destino) y empieza a transmitir de inmediato. Latencia mínima, pero propaga tramas rotas.

* **Fragment-Free:** Lee los primeros 64 bytes para asegurarse de esquivar fragmentos de colisiones comunes antes de empezar a transmitir.

## Memoria en los puertos del switch

Los switches poseen buffers de memoria RAM para almacenar temporalmente las tramas cuando un puerto de salida está congestionado o saturado. Puede ser memoria compartida por todos los puertos o buffers dedicados e independientes por cada boca física.

## CPU y RAM en un switch

Los switches administrables avanzados poseen su propia arquitectura interna de computadora: una CPU dedicada a procesar funciones lógicas complejas (como STP, seguridad o telemetría) y memoria RAM para sostener el sistema operativo del switch (ej. Cisco IOS o RouterOS) y las tablas de direcciones.

## Especificaciones generales de un switch

Al evaluar un switch comercial se analizan factores críticos: la densidad de puertos (8, 24, 48 bocas), el ancho de banda del plano trasero (*backplane bandwidth*), el factor de forma (racks de 19 pulgadas) y el consumo eléctrico.

## Características básicas de un switch

Incluyen capacidades estándar de negociación automática de velocidad (Auto-sensing), detección automática de la polaridad del cable (MDI/MDIX para no requerir cables cruzados), y luces indicadoras LED de actividad/enlace por cada puerto físico.

## LAN Virtual o VLAN

Permite dividir un único switch físico en **múltiples switches lógicos e independientes**. Dispositivos en diferentes VLANs no pueden hablar entre sí directamente aunque estén conectados al mismo equipo físico, lo que aumenta drásticamente la seguridad, optimiza el rendimiento y reduce el tamaño de los dominios de difusión.

## Calidad de Servicio (QoS)

Mecanismo que permite al switch **priorizar cierto tipo de tráfico crítico** sobre otros en situaciones de congestión. Por ejemplo, se configura para que los paquetes de Voz sobre IP (VoIP) o videoconferencias pasen primero antes que las descargas de archivos pesados de datos, evitando entrecortes.

## Diseño de la red

Armar una infraestructura exige planificar meticulosamente cómo se distribuirá el tráfico para soportar el crecimiento de la empresa sin que la red colapse por malas conexiones.

## Aislación de tráfico entre clientes y servidores

Por cuestiones de rendimiento y seguridad, los servidores de producción de alta demanda (como bases de datos o servidores web corporativos) deben colocarse en segmentos físicos o VLANs dedicadas de alta velocidad, separándolos del tráfico cotidiano e impredecible de las PCs de los usuarios finales.

## Jerarquía de switches y velocidad de uplink

Para evitar cuellos de botella, los puertos que interconectan switches entre sí o switches con servidores (**Uplinks**) deben operar a una velocidad sustancialmente mayor que los puertos de acceso de los usuarios (ejemplo: usuarios a 100 Mbps o 1 Gbps, y los enlaces troncales o uplinks a 10 Gbps o más).

## Switches en el diseño de una red

El switch no se coloca al azar; actúa como el bloque constructivo modular de toda la topología cableada de la organización.

## Diseño jerárquico

Es el estándar de oro en redes corporativas. Divide la topología en tres capas lógicas bien definidas:
1.  **Capa de Acceso:** Switches donde se conectan los usuarios finales (PCs, APs).

2.  **Capa de Distribución:** Agrupa los switches de acceso, maneja políticas de seguridad, enrutamiento inter-VLAN y control de tráfico.

3.  **Capa de Núcleo (Core):** Switches de altísima velocidad encargados únicamente de conmutar paquetes de forma masiva y ultrarrápida entre las distintas zonas de la red.

## Flexibilidad de la red

Un buen diseño permite añadir nuevos switches, servidores o mudar puestos de trabajo completos sin necesidad de reestructurar el cableado principal ni detener la operación del resto de la red corporativa.

## Switches de propósito específico

Según el entorno físico donde operen, se dividen en categorías especializadas: 
- Switches Multicapa (con capacidades de ruteo de Capa 3)
- Switches de borde
- Switches Apilables (*Stackables*, se unen con cables especiales de alta velocidad para gestionarse como una sola unidad)
- Switches Industriales (diseñados para resistir polvo, humedad, vibraciones y temperaturas extremas en fábricas).

## Características avanzadas de un switch

Los switches Enterprise modernos incorporan herramientas sofisticadas de auditoría y potencia: soporte avanzado para **PoE** (para alimentar antenas y cámaras remotas) y protocolos de telemetría como **sFlow, Netflow e IPFIX** (estándar internacional de la IETF), los cuales capturan y analizan los flujos de tráfico para identificar cuellos de botella y detectar ataques informáticos o anomalías de seguridad en tiempo real.













# Switches Ethernet y Conmutación de Capa 2

## 1. Naturaleza y Propósito del Switch
Los switches (conmutadores) Ethernet enlazan físicamente dispositivos de red entre sí, copiando y retransmitiendo tramas de un puerto a otro basándose estrictamente en las direcciones MAC de destino.
* **Estándar IEEE 802.1D:** Define las especificaciones técnicas iniciales de los switches transparentes, asegurando la interoperabilidad entre equipamiento de diferentes fabricantes.
* **Diferencia Crítica con los Routers:**
	* El **Switch** conmuta tramas basándose en direcciones MAC (Capa 2), opera de manera transparente y requiere mínima o nula configuración básica inicial para operar (Plug & Play).
	* El **Router** encamina paquetes basándose en direccionamiento lógico IP (Capa 3) y requiere que cada una de sus interfaces de red conectadas esté explícitamente configurada en una subred.

## 2. Las Cuatro Tareas Lógicas de la Tabla de Reenvío (MAC Table)
El switch mantiene una tabla dinámica en memoria RAM que asocia direcciones MAC con sus respectivos puertos físicos de salida. Al procesar una trama, realiza cuatro acciones automáticas:

1. **Aprendizaje (Learning):** El switch inspecciona la **MAC de origen** de cada trama entrante. Si no está en su tabla, la añade junto con el número de puerto físico de entrada. Si ya existía, refresca su temporizador de caducidad (*aging time*).
2. **Filtrado (Filtering):** Si la MAC de destino ya está registrada en la tabla y está ubicada en el *mismo puerto físico* por el cual ingresó la trama, el switch la elimina (la filtra) para evitar que se duplique innecesariamente en ese medio físico.
3. **Reenvío (Forwarding):** Si la MAC de destino está registrada en la tabla en un puerto físico diferente, el switch retransmite la trama de forma selectiva y única a través de ese puerto de salida concreto.
4. **Inundación (Flooding):** Si la dirección MAC de destino es de **Broadcast**, **Multicast** o es una dirección **Unicast desconocida** (no registrada aún en la tabla), el switch duplica la trama y la inunda por todos los puertos activos del equipo, excepto por aquel por donde ingresó.

## 3. Métodos de Conmutación de Tramas (Switching Modes)
Define el nivel de inspección que realiza el switch antes de reenviar los datos por el puerto de salida:
* **Store-and-Forward (Almacenamiento y Reenvío):** El switch recibe la trama **completa** en sus buffers internos, calcula el valor de verificación **CRC/FCS** para validar que no tenga errores y, si está íntegra, la reenvía. Ofrece máxima seguridad (no propaga errores), pero tiene la latencia más alta.
* **Cut-Through (Corte Directo):** El switch lee únicamente los primeros **6 bytes** de la trama (la MAC de destino) e inmediatamente empieza a transmitirla al puerto de salida, sin esperar el resto de los datos ni verificar errores. Latencia extremadamente baja, pero propaga tramas corruptas o dañadas.
* **Fragment-Free (Libre de Fragmentos):** Una variante optimizada de Cut-Through. El switch almacena y lee los primeros **64 bytes** de la trama antes de iniciar el reenvío. Elige este tamaño exacto porque la teoría de redes demuestra que la inmensa mayoría de las colisiones y fragmentos corruptos ocurren dentro de los primeros 64 bytes de la transmisión.



## 4. Segmentación: Dominios de Colisión frente a Dominios de Difusión
* **Dominio de Colisión:** Segmento físico de la red donde los paquetes de datos pueden chocar si dos dispositivos transmiten a la vez.
	* *Acción del Switch:* **Divide los dominios de colisión.** Cada puerto individual del switch constituye un dominio de colisión único e independiente (**Microsegmentación**). En configuraciones Full-Duplex, las colisiones se eliminan por completo. (El antiguo *Hub* mantenía un único dominio de colisión para todos sus puertos).
* **Dominio de Difusión (Broadcast Domain):** Alcance lógico máximo de la red hasta donde se propaga una trama de broadcast (`FF:FF:FF:FF:FF:FF`).
	* *Acción del Switch:* **NO divide dominios de difusión.** Por defecto, todas las interfaces físicas de un switch estándar pertenecen al mismo dominio de difusión.
	* *Acción del Router:* **SÍ divide dominios de difusión.** Las tramas de broadcast se detienen en la interfaz del router; este componente de Capa 3 nunca reenvía broadcasts hacia otras redes.

## 5. Clasificación de Switches y Características Avanzadas
* **Switches Multicapa (Layer 3 Switches):** Equipos híbridos que operan con la conmutación rápida de Capa 2 y añaden funciones avanzadas de enrutamiento lógico de Capa 3.
* **Switches de Acceso o de Borde:** Equipos diseñados específicamente para conectar de forma directa las terminales de los usuarios finales a la infraestructura de red.
* **Switches Apilables (Stackable):** Diseñados con puertos traseros especiales para interconectar físicamente varios chasis mediante un bus de alta velocidad, permitiendo administrarlos a todos de forma lógica como si fuesen un único gran switch.
* **Ethernet Industriales:** Equipos diseñados para entornos hostiles; vienen sellados contra polvo/humedad, no poseen ventiladores mecánicos, resisten altas vibraciones y temperaturas extremas, y usan conectores reforzados.
* **Switches Access-Point Wireless:** Conmutadores cableados convencionales que integran antenas y soporte directo para gestionar redes inalámbricas.
* **Protocolos Netflow, sFlow e IPFIX:** Tecnologías de auditoría que recopilan información analítica sobre los flujos de tráfico que atraviesan los puertos del switch. Netflow es propietario de Cisco y sirvió de base para el estándar internacional **IPFIX** de la IETF. Se utilizan en seguridad informática para mapear patrones de tráfico e identificar ciberataques (como ataques de denegación de servicio).
* **PoE (Power over Ethernet):** Estándar técnico que permite suministrar energía eléctrica continua (DC) a través de los mismos pares de cobre trenzados del cable Ethernet. Esto permite energizar componentes remotos (teléfonos IP, cámaras de videovigilancia, antenas Wi-Fi) sin requerir fuentes de alimentación ni enchufes eléctricos locales en las paredes.