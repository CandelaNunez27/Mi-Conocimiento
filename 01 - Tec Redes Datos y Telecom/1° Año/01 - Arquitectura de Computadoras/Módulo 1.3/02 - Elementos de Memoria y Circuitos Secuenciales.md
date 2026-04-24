A diferencia de los circuitos combinacionales, los **circuitos secuenciales** tienen memoria: su salida depende de las entradas actuales y del **estado anterior**.

## 1. Biestables (Flip-Flops)
Son la unidad mínima de almacenamiento (almacenan 1 bit).
* **Tipo D (Data):** La salida $Q$ toma el valor de la entrada $D$ cuando llega el pulso de reloj. Es ideal para registros de datos.
* **Tipo JK:** Es el más versátil. Puede setear, resetear, mantener el estado o "bascular" (cambiar al estado opuesto).
* **Tipo RS:** El más básico (Set/Reset). Tiene una condición prohibida cuando ambas entradas son 1.

## 2. El Reloj (Clock) y Sincronismo
Los circuitos secuenciales suelen ser **sincrónicos**, lo que significa que cambian de estado solo en los flancos (subida o bajada) de una señal de reloj. Esto evita errores de tiempo en el procesamiento.

## 3. Multiplexores y Decodificadores
* **Multiplexor (MUX):** Selecciona una de varias entradas de datos y la envía a una sola salida (selector de datos).
* **Decodificador:** Convierte una combinación binaria de entrada en la activación de una salida específica. Ejemplo: El decodificador de BCD a **Display de 7 segmentos** para visualizar números.