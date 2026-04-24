La capacidad total de memoria se expresa como el producto de **Número de Palabras × Ancho de Palabra**.

## 1. Unidades de Medida en Arquitectura
En informática se utiliza la base 2:
* **1 K (Kilo):** $2^{10} = 1.024$ posiciones.
* **1 M (Mega):** $2^{20} = 1.048.576$ posiciones.
* **1 G (Giga):** $2^{30} = 1.073.741.824$ posiciones.

## 2. Relación con los Buses
Para un chip de memoria con organización $N \times W$:
* **Líneas del Bus de Direcciones ($AB$):** Se calcula con el logaritmo en base 2 de $N$. Ejemplo: Si tengo $8\text{ Kb}$, necesito $13$ líneas ($2^{13} = 8.192$).
* **Líneas del Bus de Datos ($DB$):** Es igual al ancho de palabra $W$. Si la palabra es de $8\text{ bits}$, el $DB$ tiene $8$ líneas.

| Capacidad | $AB$ (Líneas) | $DB$ (Líneas) |
| :--- | :--- | :--- |
| $4\text{ Kb} \times 4$ | $12$ | $4$ |
| $32\text{ Kb} \times 8$ | $15$ | $8$ |
| $1\text{ Mb} \times 1$ | $20$ | $1$ |
| $64\text{ Mb} \times 16$ | $26$ | $16$ |
