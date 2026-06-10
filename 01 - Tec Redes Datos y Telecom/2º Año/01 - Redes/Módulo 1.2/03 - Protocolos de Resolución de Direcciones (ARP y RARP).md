# Análisis de Capa de Enlace (Wireshark y ARP)

## 🛠️ 1. Herramientas Utilizadas
* **Wireshark:** Analizador de protocolos. Pone la tarjeta de red en modo escucha para capturar y leer el tráfico.
* **`ip route` (o `route -n`):** Muestra por dónde sale nuestro tráfico (nuestra Puerta de Enlace / Router).
* **`ping`:** Fuerza la comunicación con otra IP enviando paquetes de prueba.
* **`arp -a`:** Muestra la tabla local donde la PC guarda las parejas de "IP = MAC Address".

---

##  2. Paso a Paso del Laboratorio

**Objetivo:** Forzar a la PC a hablar con el router para capturar e inspeccionar cómo funciona el protocolo ARP en la Capa de Enlace.

### Paso 1: Encontrar nuestro Router
Necesitamos saber a qué IP hacerle ping.
* **Comando:** 
```bash
  ip route
```

- **Qué observamos:** Buscamos la línea `default via`. En este caso, nos indicó que la IP del router era `172.22.32.1` y la interfaz usada era `eth2`.


### Paso 2: Iniciar la Captura

- Abrimos **Wireshark** (como administrador).

- Seleccionamos la interfaz descubierta (`eth2`) y comenzamos a capturar.


### Paso 3: Generar Tráfico

Obligamos a la red a generar un mensaje ARP haciendo un ping al router.

- **Comando:**
```Bash
ping 172.22.32.1
```

### Paso 4: Analizar la Trama en Wireshark

Detenemos la captura, escribimos `arp` en la barra de filtros y analizamos el paquete:

- **Cabecera Ethernet:** Vimos la MAC de nuestra PC (Origen). Como era una solicitud ARP (_Request_), la MAC de Destino era `FF:FF:FF:FF:FF:FF` (Broadcast, es decir, un grito a toda la red).

- **Campo Type:** Marcaba `0x0806`. Esto confirma que el paquete es de tipo ARP y viaja directamente en la trama Ethernet sin usar protocolo IP.


### Paso 5: Verificar el aprendizaje de la PC

Comprobamos que nuestra máquina guardó la MAC del router.

- **Comando:**
```Bash
arp -a
```

- **Qué observamos:** El sistema nos listó la IP `172.22.32.1` asociada a su MAC real (ej. `00:1a:2b...`). El ARP funcionó y la PC ya no necesita preguntar de nuevo.















# Práctica de Taller: Análisis de la Capa de Enlace con Wireshark

## 1. Procedimiento de Laboratorio

Pasos técnicos seguidos durante la actividad práctica para capturar e inspeccionar tramas reales en la red:
1. Se inició el analizador de protocolos **Wireshark** con privilegios elevados de administrador.
2. Se identificó la interfaz de red cableada activa observando el gráfico de picos de tráfico en tiempo real.
3. Se abrió la terminal de Linux y se ejecutó el comando `ip route` (o `route -n`) para localizar la dirección IP de la puerta de enlace predeterminada o Router (ejemplo: `172.22.32.1`).
4. Se inició una captura activa en Wireshark y en la terminal se procedió a disparar tráfico ICMP constante ejecutando: `ping 172.22.32.1`.
5. En la barra de Wireshark se aplicó el filtro `arp` o `icmp` para aislar el tráfico de la capa de enlace.

## 2. Inspección Detallada en Wireshark

Al abrir el desglose de una trama Ethernet capturada, se pudieron constatar físicamente los conceptos teóricos:
* **Cabecera Ethernet (Ethernet II):** Muestra con claridad los campos de la dirección MAC destino y MAC origen de 48 bits.
* **El campo Type (Tipo):** Permite ver el código que indica qué protocolo viaja adentro de la carga útil. Cuando el switch transmite un mensaje ARP, el campo tipo muestra el valor hexadecimal **`0x0806`**, confirmando que la trama encapsula un paquete ARP de forma directa sin pasar por el protocolo IP.
* **Comprobación de la Caché:** En la consola de Linux, al ejecutar `arp -a`, se listó de forma exitosa el mapa de las IPs locales y sus respectivas MAC físicas que el sistema operativo aprendió dinámicamente gracias al intercambio analizado.

## Part 2: Procedimiento Práctico (Taller de Wireshark)

Pasos seguidos en el laboratorio para capturar y analizar el tráfico de Capa de Enlace:

1. Se inició **Wireshark** con privilegios de administrador.
    
2. Se identificó la interfaz activa (ej. `eth2` o `Wi-Fi`) observando la gráfica de picos de tráfico en tiempo real.
    
3. Se inició la captura y se ejecutó en la consola del sistema operativo el comando de diagnóstico para identificar el Gateway o router: `ip route` o `route -n`.
    
4. Se procedió a realizar un `ping` hacia la IP del router resuelta (ej. `ping 172.22.32.1`).
    
5. En Wireshark, se aplicó el filtro `arp` o `icmp` para aislar los paquetes del taller. Se pudo verificar visualmente en la ventana de inspección de Wireshark cómo la trama Ethernet encapsula perfectamente los mensajes ARP utilizando el Type `0x0806` y cómo las direcciones MAC de origen y destino cambian de Broadcast a Unicast entre el Request y el Reply.