La Unidad de Entrada/Salida (E/S) tiene la misión fundamental de conectar los módulos internos de la computadora (UCP y Memoria) con los dispositivos externos, denominados **periféricos**.

## El problema de las velocidades (El Módulo de E/S)
La velocidad de los periféricos mecánicos o externos es muchísimo menor que la del procesador electrónico. Además, los formatos de datos y las señales suelen ser incompatibles. Por esto, la UCP nunca se conecta directamente a un periférico; siempre lo hace a través de un **Módulo o Controlador de E/S**.

Este módulo actúa como un "amortiguador" (buffer) e incluye:
* **Señales de Estado:** Indican cómo está el dispositivo (Listo, Ocupado, Desconectado).
* **Señales de Control:** Determinan la función a realizar (Leer, Escribir, Recibir).
* **Lógica de Control:** Gobierna al dispositivo según las órdenes de la UCP.
* **Transductor:** Convierte los datos a la energía/formato que necesita el periférico, almacenándolos temporalmente en un buffer.

## Tipos de Transferencia
* **Transferencia Elemental:** Se envía o recibe una cantidad muy pequeña de datos (ej. 1 byte a la vez), típico de teclados o ratones.
* **Transferencia de Bloque:** Se envían grandes paquetes de datos enteros de una sola vez, típico de discos duros o tarjetas de red.