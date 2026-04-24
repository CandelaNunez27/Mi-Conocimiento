La Unidad de Control es el "director de orquesta" del procesador. Funciona en un ciclo infinito de dos fases principales: **Búsqueda (Fetch)** y **Ejecución (Execute)**.

## 1. Registros Clave de la Unidad de Control
* **Contador de Programa (PC o IP - Instruction Pointer):** Siempre guarda la dirección de memoria de la *próxima* instrucción que se va a ejecutar.
* **Registro de Instrucciones (IR):** Guarda la palabra binaria de la instrucción que se acaba de traer de la memoria para ser decodificada.
* **Decodificador de Instrucciones:** Lee el código de operación (ej. saber que el binario "1011" significa "Sumar") y activa los circuitos de secuencia correspondientes.

## 2. El Ciclo de Máquina
1. **Fase de Búsqueda:**
   * La Unidad de Control lee la dirección que tiene el Contador de Programa (PC).
   * Va a esa dirección en la Memoria y copia la instrucción.
   * Guarda esa instrucción en el Registro de Instrucciones.
   * El Contador de Programa se incrementa en +1.
2. **Fase de Ejecución:**
   * El Decodificador analiza la instrucción.
   * Si la instrucción necesita datos extra (operandos), va a buscarlos a la memoria o a los registros (ej. Registro B).
   * Se ejecuta la operación (ej. una resta en la ULA).
   * El resultado se transfiere a un registro (Acumulador) o a la memoria, según indique la instrucción.