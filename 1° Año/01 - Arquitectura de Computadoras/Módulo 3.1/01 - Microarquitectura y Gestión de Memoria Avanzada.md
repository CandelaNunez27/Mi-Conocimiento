Los procesadores actuales han evolucionado para superar el "cuello de botella" de Von Neumann mediante el paralelismo a nivel de instrucción y una gestión inteligente de la memoria.

## 1. Técnicas de Rendimiento en el Núcleo
* **Pipeline (Segmentación):** Divide la ejecución en etapas (Fetch, Decode, Execute, Write). Permite procesar varias instrucciones en diferentes etapas simultáneamente.
* **Superescalar:** El procesador tiene múltiples unidades funcionales (ALUs, FPUs) para ejecutar más de una instrucción por ciclo de reloj.
* **Ejecución Dinámica (Out-of-Order):** El procesador reordena las instrucciones para ejecutar primero aquellas cuyos datos ya están disponibles, evitando esperas innecesarias.
* **Predicción de Bifurcaciones:** El procesador "arriesga" un resultado en saltos condicionales (`if`) para no detener la cadena de montaje.

## 2. Jerarquía de Caché y Políticas
* **Niveles (L1, L2, L3):** L1 es la más rápida y cercana al núcleo (usualmente con arquitectura Harvard: separa instrucciones de datos). L3 es la más grande y compartida entre núcleos.
* **Políticas de Escritura:**
	* *Write Through:* Actualiza caché y RAM al mismo tiempo.
	* *Write Back:* Solo actualiza caché; solo va a RAM si el dato es expulsado o solicitado por otro componente.

## 3. MMU (Memory Management Unit)
Es el hardware que permite la existencia de Sistemas Operativos modernos.
* **Modo Protegido:** Permite direccionar más de 1MB de RAM, habilita la multitarea y protege la memoria de un proceso para que no sea invadida por otro.
* **Memoria Virtual:** La MMU traduce direcciones lógicas en físicas mediante:
	* **Segmentación:** Divide la memoria en bloques de tamaño variable (segmentos) con privilegios de acceso.
	* **Paginación:** Divide la memoria en bloques fijos (páginas, ej. 4KB). Permite usar el disco duro como extensión de la RAM (Swap).