El álgebra booleana obedece a un conjunto de reglas matemáticas que permiten simplificar funciones lógicas complejas, reduciendo así la cantidad de compuertas físicas necesarias en un circuito.

## 1. Operaciones con 0 y 1
* **AND:** * $A \cdot 0 = 0$
    * $A \cdot 1 = A$
* **OR:** * $A + 0 = A$
    * $A + 1 = 1$

## 2. Idempotencia y Complemento
* **Idempotencia:** Multiplicar o sumar una variable por sí misma no la altera.
    * $A \cdot A = A$
    * $A + A = A$
* **Complemento:**
    * $A \cdot \overline{A} = 0$ (Una variable no puede ser verdadera y falsa al mismo tiempo).
    * $A + \overline{A} = 1$ (Una variable o su negación siempre será verdadera).

## 3. Propiedades de la compuerta XOR
* $A \oplus 0 = A$
* $A \oplus 1 = \overline{A}$
* $A \oplus A = 0$
* $A \oplus \overline{A} = 1$

## 4. Involución (Doble Negación)
* $\overline{\overline{A}} = A$