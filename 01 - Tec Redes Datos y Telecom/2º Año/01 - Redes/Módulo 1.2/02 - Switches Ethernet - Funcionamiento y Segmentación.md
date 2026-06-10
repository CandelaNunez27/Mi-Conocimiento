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