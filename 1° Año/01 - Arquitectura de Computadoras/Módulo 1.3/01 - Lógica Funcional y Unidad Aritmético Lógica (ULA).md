La **ULA (Arithmetic Logic Unit)** es el componente del procesador encargado de realizar operaciones aritméticas (suma, resta) y lógicas (AND, OR, XOR).

## 1. Sumadores Binarios
Son la base del cálculo en la computadora.
* **Medio Sumador (Half Adder):** Suma dos bits y genera un bit de suma (S) y un bit de arrastre (C). No tiene entrada para un acarreo previo.
    * $S = A \oplus B$
    * $C = A \cdot B$
* **Sumador Completo (Full Adder):** Suma tres bits (dos operandos y un acarreo de entrada $C_{in}$). Es el que se usa para sumar números de varios bits en cascada.

## 2. Comparadores
Circuitos que comparan dos números binarios ($A$ y $B$) para determinar si $A > B$, $A < B$ o $A = B$. Se utilizan para la toma de decisiones en el software (instrucciones `if`).

## 3. Mecanización de la Suma
* **Suma Serie:** Utiliza un solo sumador completo y procesa bit a bit, guardando el acarreo en un elemento de memoria (Flip-Flop). Es lenta pero ahorra espacio.
* **Suma Paralelo:** Utiliza un sumador completo por cada bit del número. Es mucho más rápida pero requiere más circuitería.