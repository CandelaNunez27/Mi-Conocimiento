Una **función booleana** es una expresión algebraica formada por variables binarias, las constantes 0 y 1, y los operadores lógicos. 

## Circuitos Combinacionales
Son aquellos circuitos digitales cuyas salidas dependen *única y exclusivamente* del estado actual de sus entradas en un momento dado, sin importar el historial anterior (no tienen memoria).

### Metodología de Diseño de un Circuito Combinacional
Para resolver problemas lógicos mediante hardware (como activar una alarma, comparar números o indicar la posición de una cinta transportadora), se siguen estos pasos:

1.  **Análisis del problema:** Definir claramente la cantidad y el significado de las variables de entrada y las variables de salida.
2.  **Tabla de Verdad:** Construir una tabla con todas las combinaciones posibles de las entradas (si hay $n$ entradas, habrá $2^n$ combinaciones o filas). Determinar el valor de salida (0 o 1) deseado para cada fila.
3.  **Ecuación Lógica:** Obtener la función booleana a partir de la tabla. Un método común es sumar los "minitérminos" (las filas donde la salida es `1`). Por ejemplo, de una tabla de 3 entradas, podemos obtener: $F(A,B,C) = A \cdot \overline{B} \cdot C + A \cdot B \cdot C$.
4.  **Simplificación:** Utilizar las leyes del álgebra de Boole para reducir la ecuación a su mínima expresión.
5.  **Diagrama Lógico:** Dibujar el circuito final utilizando la simbología estándar de las compuertas lógicas (AND, OR, NOT, etc.) conectadas según la ecuación simplificada.