Cuando los integrados (CI) disponibles son más pequeños que la memoria total que necesitamos, realizamos una expansión.

## 1. Expansión de Palabra (En Ancho)
Se usa para aumentar la cantidad de bits que se pueden leer a la vez.
* **Conexión:** Se conectan los buses de direcciones en paralelo. Las salidas de datos de cada chip se unen para formar una palabra más larga.
* **Ejemplo:** Para obtener $2\text{ Mb} \times 32$ usando chips de $512\text{ Kb} \times 16$.

## 2. Expansión de Direcciones (En Largo)
Se usa para aumentar la cantidad de posiciones de memoria disponibles.
* **Conexión:** Se utiliza un **Decodificador de Direcciones** externo conectado a las líneas más significativas del Bus de Direcciones para activar la señal **CS** del chip correspondiente.
* **Ejemplo:** Para diseñar un banco de $128\text{ Kb} \times 8$ con chips de $32\text{ Kb} \times 8$:
    * Dividimos $128 / 32 = 4$ chips.
    * Necesitamos un decodificador de $2$ a $4$ (ya que $2^2 = 4$).

## 3. Cálculo de Chips Necesarios
$$\text{Total de Chips} = \frac{\text{Capacidad Deseada (Posiciones)}}{\text{Capacidad CI (Posiciones)}} \times \frac{\text{Ancho Deseado}}{\text{Ancho CI}}$$