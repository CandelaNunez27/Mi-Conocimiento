Para que la UCP y los periféricos se pongan de acuerdo para transferir datos, existen tres técnicas principales:

## 1. Polling (Sondeo)
La UCP tiene que detener su trabajo para preguntarle constantemente al periférico si está listo para enviar o recibir datos. Es muy ineficiente porque desperdicia muchísimo tiempo de procesamiento.

## 2. Interrupciones
En lugar de preguntar, la UCP sigue trabajando normalmente. Cuando el periférico está listo, le envía una señal "avisando" (interrumpiendo) a la UCP.
* **PIC (Controlador Programable de Interrupciones):** Es el chip encargado de recibir estas peticiones, priorizarlas (decidir cuál es más urgente), pausar a la UCP y enviarla a la rutina de servicio.
* **Instrucciones `RET` / `IRET`:** Al finalizar la interrupción, el procesador debe volver a lo que estaba haciendo. Estas instrucciones no necesitan tener escrita la dirección de retorno porque esa dirección se guardó automáticamente en la **Pila (Stack)** del sistema.

### Señales Críticas de Interrupción:
* **INT (Enmascarable):** El procesador puede decidir ignorarla si se usa la instrucción de deshabilitar (DI). Se usa para periféricos comunes.
* **NMI (No Enmascarable):** El procesador *no puede* ignorarla nunca. Se usa para eventos críticos, como fallas graves de hardware.
* **RESET:** Reinicia el sistema por completo, obligando al procesador a volver a su estado inicial de arranque.

## 3. DMA (Acceso Directo a Memoria)
Se utiliza para periféricos de altísimo rendimiento (como tarjetas gráficas o placas de red de alta velocidad). 
* **Funcionamiento:** Permite que el periférico lea o escriba directamente en la memoria RAM del sistema **sin tener que interrumpir ni pasar por el procesador**. Esto libera a la UCP de esa carga, mejorando drásticamente el rendimiento general del equipo.