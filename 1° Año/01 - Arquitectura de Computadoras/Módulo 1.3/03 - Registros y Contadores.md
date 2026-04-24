# Aplicaciones: Registros y Contadores

## 1. Registros de Desplazamiento
Se utilizan para mover datos dentro del procesador o convertir formatos.
* **Serie-Serie:** El dato entra bit a bit y sale bit a bit.
* **Serie-Paralelo:** El dato entra bit a bit pero se puede leer todo el conjunto de bits al mismo tiempo (ej. recibir datos de una red y pasarlos a memoria).

## 2. Contadores
Circuitos secuenciales que pasan por una secuencia de estados predefinida.
* **Asincrónicos:** El reloj solo llega al primer Flip-Flop; el cambio se propaga como una "onda". Son más sencillos pero tienen retrasos.
* **Sincrónicos:** El reloj llega a todos los Flip-Flops al mismo tiempo. Son más rápidos y seguros.
* **Ejemplo Práctico (7490):** Es un contador de décadas muy común que cuenta del 0 al 9 en binario (BCD).

## 3. Diagramas de Tiempo
Representación gráfica que muestra cómo cambian las señales con respecto al tiempo. Es fundamental para analizar el comportamiento de los Flip-Flops y detectar errores de sincronismo.