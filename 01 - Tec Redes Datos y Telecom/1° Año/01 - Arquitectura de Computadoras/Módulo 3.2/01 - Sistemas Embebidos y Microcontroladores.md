La computación ubicua (o inteligencia ambiental) busca integrar la informática en nuestro entorno hasta volverla invisible. El motor de esto son los **Sistemas Embebidos (SE)**.

## 1. Características Principales
A diferencia de una PC de propósito general, un Sistema Embebido está diseñado para realizar **una o unas pocas funciones dedicadas**, a menudo con restricciones de tiempo real.
* **Recursos Limitados:** Tienen memoria y capacidad de procesamiento ajustadas a su tarea para reducir costos y tamaño.
* **Bajo Consumo:** Diseñados para funcionar con baterías o energía limitada.
* **Flexibilidad:** Al no estar ligados a una arquitectura genérica rígida, se pueden adaptar interfaces específicas (ASIC, PLD).

## 2. Arquitectura de Hardware
* **CPU / Microcontrolador:** El "cerebro". Un microcontrolador integra en un solo chip la CPU, memoria (RAM/ROM) y periféricos de E/S.
* **Reloj de Tiempo Real (RTC) y Watchdog:** El Watchdog es un temporizador de seguridad que reinicia el sistema si el software se cuelga.
* **Puertos de Comunicación:** UART, SPI, I2C, y módulos inalámbricos como XBee/ZigBee (2.4 GHz, topología de malla para sensores).

## 3. Software y Sistemas Operativos
* **Firmware:** Es el software de más bajo nivel que interactúa directamente con el hardware (ej. BIOS, UEFI).
* **Sistemas Operativos Embebidos:** A veces no hay SO y el código se ejecuta "bare-metal" (directamente en el chip). Para sistemas más complejos se usan:
    * *RTOS (Real Time Operating System):* Garantizan tiempos de respuesta estrictos (ej. FreeRTOS).
    * *SO Adaptados:* Windows IoT, Raspbian, Firefox OS, TinyOS.