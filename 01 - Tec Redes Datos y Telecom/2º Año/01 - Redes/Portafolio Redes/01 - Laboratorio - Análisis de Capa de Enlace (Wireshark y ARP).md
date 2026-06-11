# primera versión
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







---
# segunda versión


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
