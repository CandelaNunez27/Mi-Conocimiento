# Capa de Enlace de Datos y Protocolo Ethernet

La capa de enlace de datos se encarga de la transferencia fiable de información a través de un canal físico de comunicación. Su función principal es tomar los datagramas de la capa de red y encapsularlos en unidades llamadas **tramas (frames)**.

## 1. Tipos de Canales en la Capa de Enlace

El diseño de los protocolos varía según el tipo de medio físico utilizado:

* **Canales de Difusión (Broadcast Channels):** Son comunes en redes locales (LAN), Wi-Fi, redes satelitales y accesos híbridos de fibra y coaxial (HFC). Al haber muchos hosts conectados al mismo medio, requieren un **protocolo de acceso al medio (MAC)** para coordinar las transmisiones y evitar que las tramas colisionen.

* **Canales Punto a Punto (Point-to-Point):** Conexión directa y exclusiva entre dos dispositivos, como el enlace entre dos routers o entre un módem residencial y el router del ISP. No sufren colisiones de datos.

## 2. Parámetros Técnicos de Ethernet

* **Tamaño de la Trama Ethernet:** * **Mínimo:** **64 bytes**. Si una trama mide menos, se considera un fragmento de colisión (*runt frame*) y se descarta.
    * **Máximo estándar:** **1518 bytes** (puede llegar a 1522 bytes si incluye etiquetas de VLAN 802.1Q).

* **MTU (Maximum Transmission Unit):** Es la unidad máxima de transferencia. Define el tamaño máximo del paquete de la capa de red (datos útiles) que puede ser transportado en una sola trama sin fragmentarse. Para Ethernet estándar, la MTU es de **1500 bytes**.

* **Jumbo Frames:** Son tramas Ethernet que transportan una carga útil (MTU) superior al estándar de 1500 bytes, llegando habitualmente hasta los **9000 bytes**. Se utilizan exclusivamente en redes de almacenamiento (SAN) o centros de datos para optimizar transferencias de gran volumen, ya que reducen drásticamente la carga de procesamiento (CPU) al generar menos cabeceras de red.

## 3. Modos de Transmisión del Tráfico

1.  **Unicast:** Envío de información desde un único emisor hacia un único receptor específico.

2.  **Multicast:** Distribución eficiente del tráfico desde un emisor hacia un grupo de receptores interesados (uno a muchos).

3.  **Broadcast:** Transmisión de datos que serán recibidos y procesados por **todos** los dispositivos que pertenezcan a la misma red local.

## 4. Conceptos Avanzados de Hardware

* **Interfaz Loopback:** Es una interfaz de red puramente virtual (habitualmente asociada a la IP `127.0.0.1` en IPv4). Se utiliza para pruebas locales de diagnóstico, desarrollo de software y verificación de que la pila de protocolos de red del sistema operativo funciona correctamente sin depender de hardware físico.

* **Auto-Sensing (Autonegociación):** Función que permite a dos interfaces de red conectadas negociar automáticamente la velocidad de transmisión más alta compatible (ej. 10/100/1000 Mbps) y el modo de comunicación (Half-Duplex o Full-Duplex) para evitar desajustes de configuración.