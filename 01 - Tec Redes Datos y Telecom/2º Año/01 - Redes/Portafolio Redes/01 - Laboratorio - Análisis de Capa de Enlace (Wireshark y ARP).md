# Herramientas de Diagnóstico y Análisis de Tráfico

Para comprender el comportamiento real de las redes más allá de los modelos teóricos, se requiere el uso de software de inspección y comandos de diagnóstico del sistema operativo. Estos permiten auditar cómo se construyen y viajan las tramas en la Capa de Enlace.

## 1. Utilidades y Conceptos de Diagnóstico

Durante el análisis de redes se emplean herramientas específicas que interactúan con la pila de protocolos TCP/IP del sistema:

* **Wireshark (Analizador de Protocolos):** Es un software de inspección profunda de red (sniffer). Su función es capturar los paquetes que entran y salen de una interfaz de red en tiempo real. Para lograrlo, suele configurar la placa de red en "modo promiscuo", capturando incluso el tráfico que no va dirigido directamente a esa máquina. Permite desensamblar visualmente una trama y observar campo por campo sus cabeceras OSI.
* **Puerta de Enlace (Default Gateway):** Es la dirección IP del router local. Representa la "puerta de salida" que usa una computadora cuando necesita enviar datos a una red externa (como Internet).
* **Tabla de Enrutamiento Local (`ip route` / `route -n`):** Comandos de consola que leen la configuración interna del sistema operativo para mostrar por cuál interfaz de red física y hacia qué Puerta de Enlace se enviará el tráfico.
* **Comando `ping` (Protocolo ICMP):** Es una utilidad para verificar la conectividad de red a nivel de Capa 3. Envía mensajes de "solicitud de eco" a una IP destino. Si el destino responde, confirma que la ruta de red está operativa y calcula el tiempo de ida y vuelta (latencia).
* **Tabla Caché ARP (`arp -a`):** Es un espacio en la memoria RAM donde el sistema operativo guarda temporalmente el mapa de resoluciones descubiertas (qué dirección MAC física le corresponde a qué dirección IP lógica). Esto evita tener que inundar la red con preguntas ARP cada vez que se quiere enviar un dato.



---

## 2. Análisis Teórico de un Proceso de Comunicación

Al estudiar el tráfico de una red local, se puede observar cómo la teoría de la Capa de Enlace se aplica a una comunicación real entre una computadora y su router (Puerta de Enlace). El proceso analítico se desarrolla de la siguiente manera:

### Generación de la Necesidad de Comunicación
Para que exista tráfico analizable en la Capa de Enlace, un equipo debe intentar comunicarse con otro nodo (por ejemplo, enviando paquetes `ping` a la IP del router). Como el equipo origen solo conoce la dirección IP destino, se ve obligado a utilizar el protocolo **ARP** para descubrir la dirección MAC del router y poder construir la trama Ethernet.

### Inspección de la Trama y Encapsulamiento
Al capturar este momento con un analizador como Wireshark, la estructura de la trama Ethernet revela detalles fundamentales:
* **Direccionamiento Físico:** En la cabecera Ethernet (Ethernet II), se observa la MAC de la computadora origen. Si se trata de la pregunta (ARP Request), la MAC destino se registra como `FF:FF:FF:FF:FF:FF`, demostrando el concepto de **Broadcast** (difusión a todos los nodos del segmento).
* **El Campo Tipo (Type):** Es el indicador clave del encapsulamiento. Al inspeccionar una solicitud ARP, este campo muestra el valor hexadecimal **`0x0806`**. Este valor es la prueba empírica de que el protocolo ARP **no utiliza una cabecera IP**; se encapsula de forma directa e inmediata dentro del campo de datos de la trama Ethernet.

### Resolución y Actualización del Sistema
Una vez que el router contesta enviando su dirección MAC real (ARP Reply en modo Unicast), la comunicación a nivel de enlace se establece con éxito. Como resultado de este proceso, el sistema operativo de la computadora actualiza de forma silenciosa su tabla interna. Si un administrador audita el sistema (mediante comandos como `arp -a`), podrá comprobar que la dirección IP del router ahora está firmemente vinculada a su MAC de hardware, optimizando las futuras transmisiones.


# Laboratorio: Análisis de la Capa de Enlace con Wireshark

## 1. Herramientas y Conceptos Prácticos
Antes de analizar el tráfico, es fundamental entender las herramientas de diagnóstico utilizadas por el sistema operativo y el administrador de red.

* **Wireshark:** Es un analizador de protocolos de red (un *sniffer* o rastreador de paquetes). 
    * *¿Para qué sirve?* Permite capturar y ver microscópicamente todo el tráfico que entra y sale de una placa de red en tiempo real. 
    * *¿Cómo funciona?* Pone la tarjeta de red en "modo promiscuo", obligándola a capturar y registrar todas las tramas que viajan por el cable, incluso aquellas que no van dirigidas a nuestra PC. Luego decodifica esos ceros y unos para mostrarlos en un formato legible por humanos (separando las cabeceras MAC, IP, etc.).

* **Comandos de Ruteo (`route -n` o `ip route`):** Comandos de la terminal de Linux que muestran la tabla de enrutamiento interna de la PC. Se utilizan para descubrir cuál es la "Puerta de enlace predeterminada" (Default Gateway), es decir, la dirección IP del router que nos da salida a Internet.

* **Comando `ping`:** Utilidad de diagnóstico que envía paquetes de solicitud de eco (protocolo ICMP) a una dirección IP específica. Sirve para comprobar si hay conectividad a nivel de red con ese equipo y medir el tiempo que tarda en responder (latencia).

* **Comando `arp -a`:** Muestra la tabla caché ARP local del sistema operativo, permitiendo ver qué direcciones IP ya han sido asociadas a sus respectivas direcciones MAC físicas.

---

## 2. Desarrollo de la Actividad (Paso a Paso)

El objetivo del laboratorio fue forzar a nuestra PC a comunicarse con el router para poder capturar e inspeccionar la trama Ethernet y el mensaje ARP en tiempo real.

### Paso 1: Identificación de la Puerta de Enlace
Primero, necesitamos saber a qué IP hacerle ping. Abrimos la terminal de Linux y ejecutamos el comando para ver la tabla de rutas.
* **Comando ejecutado:**
```bash
$ ip route
```

- **Salida obtenida:**
```Plaintext
 default via 172.22.32.1 dev eth2 proto dhcp src 172.22.3X.XXX
```
  
- _Explicación:_ El sistema nos indica que nuestra puerta de enlace por defecto es la IP `172.22.32.1` y que el tráfico sale por la interfaz de red llamada `eth2`.

### Paso 2: Preparación de la Captura

1. Abrimos **Wireshark** con permisos de administrador.

2. En la pantalla inicial, seleccionamos la interfaz de red activa descubierta en el paso anterior (en este caso, `eth2`).

3. Iniciamos la captura de tráfico.


### Paso 3: Generación de Tráfico

Para que Wireshark tenga algo que analizar, forzamos una comunicación con el router enviando paquetes de prueba.

- **Comando ejecutado:**
```bash
$ ping 172.22.32.1
```

- **Salida obtenida:**
```Plaintext
PING 172.22.32.1 (172.22.32.1) 56(84) bytes of data.
64 bytes from 172.22.32.1: icmp_seq=1 ttl=64 time=3.83 ms
```

### Paso 4: Análisis e Inspección en Wireshark

Al detener la captura en Wireshark y filtrar la búsqueda con la palabra `arp`, inspeccionamos el paquete capturado:

- **Cabecera Ethernet (Ethernet II):** Pudimos observar físicamente las direcciones MAC de origen (nuestra PC) y de destino. Cuando el paquete era un "ARP Request", la MAC de destino era `FF:FF:FF:FF:FF:FF` (Broadcast).

- **Campo Type:** Vimos que el campo que indica el protocolo encapsulado tenía el valor hexadecimal **`0x0806`**, lo que corrobora la teoría de que un mensaje ARP viaja directamente dentro de la trama Ethernet sin usar protocolo IP.


### Paso 5: Verificación de la Caché Local

Finalmente, comprobamos que el sistema operativo aprendió la MAC del router y la guardó en su memoria para no tener que preguntar de nuevo.

- **Comando ejecutado:**
```bash
 $ arp -a
```

- **Salida obtenida:**
```Plaintext
? (172.22.32.1) at 00:1a:2b:3c:4d:5e [ether] on eth2
```
 
