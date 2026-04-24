Un **Bus** es un conjunto de líneas eléctricas compartidas que conectan los distintos componentes del sistema. Existen líneas de Direcciones, Datos y Control.

## El Cuello de Botella del Bus Único
Cuando conectamos demasiados dispositivos a un mismo bus principal, ocurren problemas graves:
1. **Retardo de propagación:** El bus debe ser físicamente más largo, tardando más la señal.
2. **Cuello de botella:** Si la demanda de transferencia es mayor a la capacidad del bus, los dispositivos se encolan y esperan.
3. **Incompatibilidad de velocidades:** Un dispositivo muy lento frena al bus, impidiendo que los dispositivos rápidos transfieran miles de datos en ese mismo tiempo.

## Jerarquía y Estándares de Buses
Para solucionar esto, las computadoras modernas usan una jerarquía de múltiples buses (buses locales rápidos para la CPU/Memoria y buses de expansión más lentos para periféricos).

Algunos estándares históricos y actuales:
* **ISA / EISA / VESA:** Antiguos y lentos.
* **AGP:** Puerto exclusivo que se usaba solo para tarjetas gráficas (Aceleradora de Gráficos).
* **PCI / PCI Express (PCIe):** El estándar moderno interno. PCIe alcanza altísimas velocidades (decenas de GB/s) mediante carriles (lanes) seriales.
* **USB (Universal Serial Bus) / Firewire:** Estándares externos para conectar periféricos de forma universal.