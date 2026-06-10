# Hardware de Red e Interfaces (Cisco y Mikrotik)

El hardware de red varía enormemente según su ámbito de aplicación: **SOHO** (Hogareño / Pequeña Oficina) hasta entornos **Enterprise** (Mediana y gran empresa). 

## 1. Conceptos de Hardware

* **PoE (Power over Ethernet):** Tecnología que permite enviar energía eléctrica y datos a través del mismo cable de red trenzado. Ideal para alimentar antenas WiFi, cámaras IP o teléfonos sin necesidad de un enchufe cercano.

* **Marcas de referencia:** Mikrotik (ej. RB750, hEX PoE) es muy utilizado en proveedores de internet (ISP) y pymes por su gran relación costo/beneficio operativo (RouterOS). Cisco domina el entorno Enterprise.

## 2. Interfaces y Cables en Routers Cisco
Los routers empresariales suelen ser modulares, permitiendo agregar tarjetas de expansión (**WIC** - *WAN Interface Card*) según la necesidad.

* **Conexiones Seriales (WAN):** Se utilizaban tradicionalmente para conectar el router a la red telefónica o al ISP.
    * *Tipos de cable:* V.35 DCE (Data Circuit-terminating Equipment, da la señal de reloj) y DTE (Data Terminal Equipment).
    * *Conectores físicos:* DB60, LHF60 o los más compactos "Smart Serial".
    * *Tarjetas comunes:* WIC 1T (1 puerto serial), WIC 2T (2 puertos seriales).

* **Puertos de Gestión (Out-of-band):**
    * **Consola:** Puerto dedicado (generalmente RJ45 celeste) para conectarse directamente por cable serial desde una PC y configurar el router cuando está de fábrica o sin red.
    * **AUX (Auxiliar):** Similar a la consola, históricamente usado para conectar un módem telefónico y administrar el equipo remotamente ante caídas de la red principal.