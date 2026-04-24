El **Álgebra de Boole** es un sistema matemático desarrollado por George Boole (1854) para analizar la lógica del pensamiento. Posteriormente, Claude Shannon (1938) demostró que este álgebra podía utilizarse para simplificar y diseñar circuitos eléctricos y electrónicos conmutadores, dando origen a la lógica digital moderna.

## Operadores Lógicos y Compuertas Básicas
Las compuertas lógicas son los bloques de construcción de los circuitos digitales. Cada una tiene una función matemática, un símbolo, y una tabla de verdad que describe su comportamiento.

* **AND (Conjunción):** La salida es `1` solo si *todas* las entradas son `1`.
    * Expresión: $S = A \cdot B$ (o simplemente $S = AB$)
* **OR (Disyunción):** La salida es `1` si *al menos una* de las entradas es `1`.
    * Expresión: $S = A + B$
* **NOT (Negación o Inversor):** Invierte el estado de la entrada. Si entra `1`, sale `0`.
    * Expresión: $S = \overline{A}$ o $S = A'$
* **NAND (Not AND):** Es la negación de la compuerta AND.
    * Expresión: $S = \overline{A \cdot B}$
* **NOR (Not OR):** Es la negación de la compuerta OR.
    * Expresión: $S = \overline{A + B}$
* **XOR (OR Exclusiva):** La salida es `1` cuando las entradas son *diferentes* (un número impar de entradas en `1`).
    * Expresión: $S = A \oplus B$
* **XNOR (NOR Exclusiva):** Es la negación de XOR. La salida es `1` cuando las entradas son *iguales*.
    * Expresión: $S = \overline{A \oplus B}$