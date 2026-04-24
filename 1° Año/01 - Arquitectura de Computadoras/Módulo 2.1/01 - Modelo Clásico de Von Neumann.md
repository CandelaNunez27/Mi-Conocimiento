Casi todas las computadoras modernas se basan en la arquitectura diseñada por John Von Neumann. Sus cuatro principios fundamentales son:

1. **Memoria Única:** Existe una sola unidad de memoria que almacena tanto los **datos** como las **instrucciones** del programa, sin diferenciarlos físicamente.
2. **Unidad Lógica-Aritmética (ULA/ALU):** Es la encargada de operar y calcular todo en formato binario.
3. **Unidad de Control Única:** Se encarga de interpretar las instrucciones de la memoria y generar las señales para que el resto del hardware actúe.
4. **Entrada/Salida (E/S):** El equipamiento periférico es operado a través de la Unidad de Control.

## Componentes Internos de la UCP (Unidad Central de Proceso)
La UCP está formada por la unión de la Unidad de Control y la ULA. Se comunica mediante un **BUS** (un canal compartido de cables por donde viaja la información).

* **Acumulador (ACM / Reg A):** Es el registro principal de la ULA. Aquí se guarda temporalmente uno de los operandos antes de un cálculo, y aquí mismo se guarda el resultado después de operar.
* **Registro B/C/D:** Registros de propósito general o auxiliares para guardar el segundo operando.