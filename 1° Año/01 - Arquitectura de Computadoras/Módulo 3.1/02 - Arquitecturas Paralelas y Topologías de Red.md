Cuando un solo procesador no es suficiente, conectamos varios. La forma en que se comunican determina la escalabilidad del sistema.

## 1. Taxonomía de Flynn
* **SISD:** Procesador convencional (Una instrucción, un dato).
* **SIMD:** Procesadores vectoriales/GPUs (Una instrucción, múltiples datos).
* **MIMD:** Sistemas multiprocesador modernos (Múltiples instrucciones, múltiples datos).

## 2. Topologías de Interconexión
Define cómo se enlazan los nodos. Se miden por su **Diámetro** (distancia máxima) y **Ancho de Bisección** (capacidad de la red al cortarla a la mitad).

* **Estáticas (Enlaces fijos):**
	* **Lineal / Anillo:** Simple pero poco tolerante a fallos.
	* **Malla 2D / Toro:** Usada en supercomputadoras por su buen equilibrio costo/rendimiento.
	* **Hipercubo:** Muy baja latencia y alta tolerancia a fallos, pero costosa de cablear en gran escala.
* **Dinámicas (Uso de Switches):**
	* **Crossbar:** Conexión directa total. Muy rápida pero escala mal (costo $N^2$).
	* **Red Omega:** Red multietapa que usa menos conmutadores para conectar muchos nodos.

## 3. Redes de Interconexión Profesionales
En clústeres reales se usan estándares de baja latencia como **InfiniBand** (DDR, QDR, EDR) que superan ampliamente al Ethernet convencional en ancho de banda y tiempos de respuesta.