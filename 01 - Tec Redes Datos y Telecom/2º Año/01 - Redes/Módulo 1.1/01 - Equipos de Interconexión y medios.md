# Equipos de Interconexión de Redes

Para que los dispositivos puedan comunicarse, existen diferentes equipos de interconexión que operan en distintas capas del modelo OSI.

## 1. Equipos de Capa Física y Enlace (Red Local)
* **Repetidor (Repeater - Capa 1):** Dispositivo electrónico que amplifica y retransmite la señal para extender la longitud máxima de la red (que en cables de cobre suele ser de 100 metros). Los *Hubs* hacían esto pero con múltiples puertos (hoy están obsoletos).
* **Switch (Conmutador - Capa 2):** Conecta dispositivos en una misma red local (LAN). Actúa como un filtro inteligente: lee la **Dirección MAC** de las tramas de datos y las envía únicamente al puerto donde está conectado el destinatario.
    * *No administrables:* Plug & play, básicos.
    * *Administrables:* Permiten configuraciones avanzadas, seguridad y creación de **VLANs** (Redes de área local virtuales).
* **Access Point (AP o Punto de Acceso WiFi):** Permite a los usuarios inalámbricos conectarse a la red cableada (LAN) mediante radiofrecuencia.



## 2. Equipos de Capa de Red (Interconexión Global)
* **Router (Encaminador - Capa 3):** Es el dispositivo encargado de interconectar *diferentes* redes (por ejemplo, tu red local con Internet). Utiliza **Direcciones IP** para enviar los paquetes de datos a través de la mejor ruta posible leyendo sus tablas de enrutamiento.

## 3. Medios Físicos de Transmisión
* **Cobre:** Cable de par trenzado (el clásico cable de red) y cable coaxial.
* **Fibra Óptica:** Transmisión mediante pulsos de luz (mayor velocidad e inmunidad al ruido).
* **Inalámbrico:** Canales de radio terrestres (WiFi, telefonía móvil) y satelitales.