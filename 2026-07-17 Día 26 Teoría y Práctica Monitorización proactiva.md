# Teoría: Monitorización

# Fundamentos Después del Despliegue

Cuando se termino de desplegar es el momento de monitoriarlo.
![](04%20-%20Otros/Imagenes/Pasted%20image%2020260803233307.png)

- **Monitorización Reactica:** arreglar algo luego de que se haya roto, respuesta luego del hecho, debe ser rápida la respuesta.
- **Monitorización Proactividad:** empezar a actual ante pequeñas anomalias previas a un error.
Se busca saber actuar de las dos formas.

# Fundamentos La 1º regla: MeLT

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260804010632.png)

Para poder utilizar las dos maneras tenemos la regla de oro MeLT
- **Métricas:** Son puramente los números, los porcentajes, rendimientos, promedios, de utilización de hardware, latencia de redes. Importante para el HPA ya que es estadistica pura.
- **Registros (Logs):** Son escritura, eventos, las respuestas de las consultas. Sentencias que dejan las aplicaciones y los servicios.
-  **Rastros (Traces):** Son el caminito a diferencia de los logs, camino de los distintos servicios para llegar a otros servicios, sirve para ver en que lugar hay latencia.
  
  Trabajadores de esto son:
   - Un trabajador de SRE (Site Reliability Engineer o Ingeniero de Confiabilidad de Sitios), ellos monitorean, automatizan, gestionan incidentes y despliegan de forma segura.
   - Un trabajador de NOC (Network Operations Center o Centro de Operaciones de Red) cuida que la red de internet y los servidores funcionen bien. 
   - Un trabajador de SOC (Security Operations Center o Centro de Operaciones de Seguridad) protege los sistemas contra virus, robos de datos y ataques de ciberdelincuentes.

# Herramientas /  Tools OpenTelemetry

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260804013034.png)

**OpenTelemetry (código abierto):** 

1. Permite lenguajes de programacion, todos escribin los log de manera distinta dando soluciones distintas. Si quiero algo mas en datos engineer usualmente me voy más por Python, si quiero un backend muy robusto opto por Java, o si quiero algo liguero, rápido y moderno voy por GO.

2.  Gracias a unas APIs y SDKs dedicada a cada uno, recibiendo sus logs los traducen.

3. Luego de que los logs ya esten traducidos el OTel Conllector recibe de cada lenguaje y se encarga de procesandolos, filtrando y acomodandolos.

4. Finalmente llegan a  los Backends Agnósticos que es donde vemos nosotros los datos filtrados y acomodados, algunas de ellas son Prometheus, Jaeger, AWS, plataformas de terceros.

# Herramientas / Tools Prometheus

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260804105424.png)

**Prometheus (código abierto):** 

1. Hace lo mismo que OpenTelemetry ya que recolecta datos, los procesa. Aunque tiene un plus también puede asociarle una base de datos PromQL guardando los datos pudiendo colocarle que cada cierto tiempo le haga un pull de los logs. OpenTelemetry es distinto solamente porque hay que trabajar con los APIs y SDKs, Prometheus solo le decia a quien queres conectart y se conecta.

2. Como guarda la inos permite hacer Contadores, Calibradores (Gauges), Hitrogramas, Resúmenes.







# Práctica: sawkl
### Preparación

1. sdssdf:
	sdsld

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
