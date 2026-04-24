La computación de alto rendimiento (**HPC**) busca resolver problemas que tardarían años en una PC normal.

## 1. El clúster y la Supercomputación
* **Nodos:** Cada unidad del clúster (servidores con procesadores como Intel Xeon o AMD EPYC/Threadripper).
* **Aceleradoras (GPGPU):** Uso de tarjetas gráficas (NVIDIA Tesla/Volta) para cálculos matemáticos masivos.
* **Ejemplos en Argentina:** **Tupac** (CONICET), **Mendieta** y **Cristina** (UNC). Requieren refrigeración de precisión y suelos técnicos.

## 2. Ley de Amdahl y Métricas
* **Speedup ($S$):** Cuánto más rápido es el sistema paralelo vs el secuencial. $S = T_s / T_p$.
* **Ley de Amdahl:** El rendimiento está limitado por la parte del código que **no** se puede paralelizar (fracción secuencial $f$). Si el 10% es secuencial, nunca superarás una aceleración de 10x, aunque uses mil núcleos.
* **Eficiencia ($E$):** $E = S / p$. Mide qué porcentaje del tiempo los procesadores están haciendo trabajo útil.

## 3. Modelos de Programación
* **Memoria Compartida (SMP):** Todos los núcleos ven la misma RAM. Se programa con **Hilos (Threads)**. Problema: Coherencia de caché.
* **Memoria Distribuida (MPP):** Cada nodo tiene su RAM. Se comunican mediante **Paso de Mensajes (MPI)**. Muy escalable.
* **HMP (Heterogeneous Multi-Processing):** Mezcla de núcleos de alta potencia y bajo consumo (como en los procesadores Intel actuales o móviles).