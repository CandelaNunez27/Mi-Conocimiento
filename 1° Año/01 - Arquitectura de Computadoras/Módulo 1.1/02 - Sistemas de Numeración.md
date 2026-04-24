Un sistema de numeración posicional utiliza una base (cantidad de símbolos distintos) y el valor de cada cifra depende de su ubicación relativa.

## 1. Sistemas Principales
* **Decimal (Base 10):** Usa 10 símbolos (0-9). Es nuestro sistema cotidiano.
* **Binario (Base 2):** Usa solo 2 símbolos (0 y 1). Es el utilizado por las computadoras porque los circuitos electrónicos presentan solo dos estados (pasa o no pasa corriente).
* **Octal (Base 8):** Usa 8 símbolos (0-7). Agrupa bits de a tres.
* **Hexadecimal (Base 16):** Usa 16 símbolos (0-9 y A, B, C, D, E, F, donde A=10, F=15). Es vital en informática porque un conjunto de 4 bits (nibble) tiene exactamente 16 combinaciones posibles, aprovechando el espacio al máximo.

## 2. Conversión entre Bases
* **De Decimal a otra base (Enteros):** Se realizan divisiones sucesivas del número decimal por la base destino (2, 8 o 16). El número se forma con los restos en orden inverso.
* **De Decimal a otra base (Fraccionarios):** Se multiplica la parte fraccionaria por la base. La parte entera del resultado forma el número en la nueva base.
* **De cualquier base a Decimal:** Se multiplica cada dígito por la base elevada a una potencia igual a la posición del dígito (empezando por 0 de derecha a izquierda en los enteros) y se suman los resultados.