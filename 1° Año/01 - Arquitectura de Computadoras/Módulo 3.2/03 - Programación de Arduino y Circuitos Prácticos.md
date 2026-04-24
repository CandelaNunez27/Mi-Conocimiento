## 1. Instrucciones de Control y Entradas
* **Lectura Digital:** `digitalRead(pin)`. Lee 1 o 0. Ideal para botones.
* **Lectura Analógica:** `analogRead(pin)`. Lee de 0 a 1023. Ideal para potenciómetros o sensores IR.
* **Bucle `for`:** Útil para secuencias (ej. encender luces de "El Coche Fantástico" o recorrer arreglos/arrays).
    * *Sintaxis:* `for (int n = 0; n < 4; n++) { ... }`

## 2. Electrónica Básica para Arduino
Al conectar componentes a los pines, hay que respetar la corriente máxima que soportan.

* **Pulsadores (Resistencias Pull-up / Pull-down):** Para evitar lecturas "flotantes" (ruido electromagnético) al leer un botón, se usa una resistencia de 10kΩ.
    * *Pull-down:* Mantiene el pin en LOW (0V) cuando no se presiona. Al presionar, lee HIGH.
    * *Pull-up:* Mantiene el pin en HIGH (5V). Al presionar, lee LOW.

* **Control de Potencia (Relés y Motores DC):**
    Un pin de Arduino no tiene fuerza para mover un motor. Se debe usar un **Transistor** (como el BD137) que actúa como interruptor electrónico de potencia.
    * *Diodo Flyback (1N4001):* Es obligatorio colocar un diodo en antiparalelo a los motores o relés para proteger la placa de Arduino de las corrientes inductivas que se generan al apagarlos.

## 3. Ejemplo Práctico: PWM (Modulación de Ancho de Pulso)
Para atenuar una luz o controlar la velocidad de un motor sin variar el voltaje real, Arduino enciende y apaga el pin miles de veces por segundo. Variando el tiempo que pasa encendido frente al tiempo apagado (Duty Cycle), se reduce la potencia promedio entregada.
* Comando: `analogWrite(pin, valor);` (Donde el valor va de 0 a 255).