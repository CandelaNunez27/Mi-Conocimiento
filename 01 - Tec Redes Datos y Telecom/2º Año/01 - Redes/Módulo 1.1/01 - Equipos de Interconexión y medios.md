# Equipos de Interconexión de Redes y Medios de Transmisión

Para construir una infraestructura de telecomunicaciones, es necesario interconectar los dispositivos finales utilizando diferentes componentes de hardware que operan en distintas capas del modelo OSI, adaptándose a las necesidades de la topología.

## 1. Clasificación General de Equipos de Interconexión

El material de la cátedra clasifica los dispositivos fundamentales en cinco categorías históricas y actuales:
1. **Repetidor (Repeater)** - Capa 1
2. **Concentrador (Hub)** - Capa 1 (En desuso)
3. **Puente (Bridge)** - Capa 2 (En desuso)
4. **Conmutador (Switch)** - Capa 2
5. **Encaminador (Router)** - Capa 3

---

## 2. Análisis de Dispositivos de Capa 1 (Capa Física)

### A. Repetidor (Repeater)
* **Función básica:** Es un dispositivo electrónico que conecta dos segmentos de una misma red, transfiriendo y amplificando el tráfico de un extremo a otro (ya sea mediante soporte cableado o inalámbrico).
* **Restricción de los 100 metros:** Los segmentos de red de cobre tienen una longitud máxima limitada (generalmente **no superan los 100 metros**). Esto ocurre debido a dos factores críticos del medio físico:
	1. **Pérdida de señal (Atenuación):** La degradación de la energía de la señal a lo largo de la distancia.
	2. **Generación de ruido:** Interferencias electromagnéticas que alteran los bits.
* **Aplicación moderna:** Se han vuelto sumamente populares en redes inalámbricas (**Wi-Fi**), donde actúan amplificando la señal de la red LAN desde el router hacia las computadoras u ordenadores que están fuera del alcance original.

### B. Concentrador (Hub)
* **Nota técnica de la cátedra:** Actualmente **no se utilizan**.
* **Funcionamiento:** Recibe los impulsos eléctricos por un puerto y los replica ciegamente hacia todos los demás puertos del equipo, sin discriminar el destino, lo que satura el medio físico con colisiones de datos.

---

## 3. Análisis de Dispositivos de Capa 2 (Capa de Enlace de Datos)

### A. Conmutador (Switch)
* **Función básica:** Interconecta dos o más segmentos de red, pasando la información de un segmento a otro de manera selectiva y eficiente.
* **Mecanismo de Aprendizaje Inteligente:** Al ser activado, el Switch empieza a **reconocer y registrar las Direcciones MAC** (Control de Acceso al Medio) de todos los dispositivos que envían datos.
* **Filtrado:** Actúa como un filtro inteligente. En lugar de inundar la red (como hacía el Hub), lee la MAC de destino de la trama y la envía **únicamente por el puerto específico** donde se encuentra el destinatario real.

### B. Puente (Bridge)
* **Nota técnica de la cátedra:** Actualmente **no se utilizan**.
* **Diferencia fundamental con el Switch:** Las funciones lógicas de un Bridge son exactamente iguales a las de un Switch (filtrar por dirección MAC en la Capa 2). Sin embargo, el puente está limitado tecnológicamente a interconectar **únicamente dos segmentos de red**, mientras que el Switch evolucionó para manejar múltiples puertos y segmentos a la vez.

### C. Punto de Acceso Inalámbrico (Access Point o AP)
* **Función básica:** Es el puente que permite a los usuarios inalámbricos transmitir y recibir paquetes hacia una red Internet o LAN cableada.
* **Restricciones de Cobertura:**
	* En una **LAN inalámbrica (Wi-Fi)**, los usuarios deben encontrarse a una distancia corta del dispositivo, usualmente a **unas pocas decenas de metros** del punto de acceso.
	* En las **redes inalámbricas de área extensa (WAN)**, la transmisión se realiza a distancias masivas conectándose a una **estación base** utilizando la misma infraestructura de celdas de la telefonía móvil.

---

## 4. Análisis de Dispositivos de Capa 3 (Capa de Red)

### Encaminador (Router)
* **Función básica:** Es el encargado de interconectar redes lógicamente independientes (por ejemplo, conectar la LAN privada de una institución universitaria con el Proveedor de Servicios de Internet - ISP).
* **Enrutamiento Inteligente:** Trabaja en la Capa 3 del modelo OSI utilizando **Direcciones IP**. Lee el encabezado del paquete de datos, consulta sus tablas de enrutamiento internas y determina de forma dinámica cuál es la **mejor ruta o camino óptimo** para enviar la información hacia su destino final a través de la red global.

---

## 5. Direccionamiento Esencial en Redes

Cualquier nodo final o dispositivo intermedio de la red maneja obligatoriamente dos tipos de direcciones lógicas y físicas para asegurar que los datos no se pierdan:

1. **Dirección MAC (Physical Address):** Identificador físico único de 48 bits grabado de fábrica en la placa de red (NIC). Es la dirección utilizada por la **Capa 2** (Switches) para mover la información localmente dentro de una misma LAN.
2. **Dirección IP (Logical Address):** Dirección lógica asignada por software (de forma manual o por DHCP). Identifica el dispositivo dentro de una red global y es utilizada por la **Capa 3** (Routers) para encaminar datos entre diferentes redes del mundo.

*Capas del Modelo OSI: Router y Switch*
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609153452.png)

---

## 6. Arquitectura Cliente-Servidor

* **Definición de Servidor (Server):** En el ámbito de las redes informáticas, un servidor es un nodo o sistema (compuesto por hardware y software dedicados) encargado de **centralizar y proveer recursos, datos o servicios específicos** a otros equipos de la red que actúan como sus "clientes" (por ejemplo, un *Web Server* aloja archivos HTML y "sirve" las páginas web ante las peticiones de los navegadores de los usuarios).

---

## 7. Clasificación de Medios Físicos de Transmisión

La capa física requiere un soporte material para guiar las señales. El programa los divide en tres grandes familias:

* **Medios de Cobre:**
	* *Cable de par trenzado:* El cable LAN estándar (limitado a 100 metros por atenuación).
	* *Cable coaxial:* Conductor central de cobre rodeado por blindaje (usado en televisión por cable e instalaciones tradicionales de banda ancha).
* **Medios de Fibra Óptica:** Filamentos de vidrio o plástico que transmiten datos mediante pulsos de luz. Ofrecen anchos de banda masivos y distancias kilométricas sin interferencias eléctricas.
* **Medios Inalámbricos (Radiofrecuencia):**
	* *Canales de radio terrestres:* Conexiones de corto y medio alcance como Wi-Fi, enlaces de microondas e infraestructura de telefonía móvil.
	* *Canales de radio vía satélite:* Enlaces de comunicación utilizando repetidores en órbita (baja o geoestacionaria) para dar cobertura a zonas remotas de la tierra.

*Símbolos comunes de las redes de datos*
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609153725.png)
