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

 Permite lenguajes de programacion, todos escribin los log de manera distinta dando soluciones distintas. Si quiero algo mas en datos engineer usualmente me voy más por Python, si quiero un backend muy robusto opto por Java, o si quiero algo liguero, rápido y moderno voy por GO.

 Gracias a unas APIs y SDKs dedicada a cada uno, recibiendo sus logs los traducen.

 Luego de que los logs ya esten traducidos el OTel Conllector recibe de cada lenguaje y se encarga de procesandolos, filtrando y acomodandolos.

 Finalmente llegan a  los Backends Agnósticos que es donde vemos nosotros los datos filtrados y acomodados, algunas de ellas son Prometheus, Jaeger, AWS, plataformas de terceros.

# Herramientas / Tools Prometheus

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260804105424.png)

**Prometheus (código abierto):** 

 Hace lo mismo que OpenTelemetry ya que recolecta datos, los procesa. Aunque tiene un plus también puede asociarle una base de datos PromQL guardando los datos pudiendo colocarle que cada cierto tiempo le haga un pull de los logs. OpenTelemetry es distinto solamente porque hay que trabajar con los APIs y SDKs, Prometheus solo le decia a quien queres conectart y se conecta.

 Como guarda la información en su pequeña base de datos nos permite ostrarla haciendo Contadores para ver como te fue a lo largo del tiempo, Calibradores (Gauges) para ver consumo de hardware, Histogramas para ver los picos de como responde nuestro programa, Resúmenes de como respondio nuestra app.

# Herramientas / Tools Stacks: TIG ó LGP

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260804111619.png)

- **Stack TIG (Telegraf > InfluxDB > Grafana):** Son expecializados en métricas. Su camino sería Telegraf que recoge los datos numéricos muy bueno para redes, luego InfluxDB que almacena estos datos rápidamente para tener valor + tiempo. Finalmente Grafana que crea los tableros visuales de estas metricas.
  
- **Stack LGP (Promtal > Loki > Grafana):** Son expecializados en Logs. Su camino sería Promtail que recoge los datos leyendo los archivo logs filtrandolos, luego Loki que almacena estos logs una base de datos no estructurada no sql indexando solo etiquetas no todo el texto así lo hace más eficiente y economico de espacio. Finalmente Grafana que crea los tableros visuales de estos Logs.

Los dos apuntan a **Grafana** es el visualizador, se puede hacer tableros tipo semáforo (Rojo error 500, amarillo si hay muchas demanda, verde si esta en 200 todo bien ), tableros de linea, barra, etc.
Hay también más stacks: (AlertManagger > Prometheus > Grafana), ELK (Elasticsearch > Logstash > Kibana ), Zabixx dolor de cabeza, 

# Herramientas / Tools Nativo AWS: Cloudwatch

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260804114340.png)

La herramienta de las nubes es Cloudwatch, es se Naturaleza SaaS, muy facil de activarlo. Se útiliza para el monitoreo de computo y redes. Es algo límitado su uso pero se le suele utilizar mucho como pasa mano, todo lo que este pasando en aws, cloudwatch lo pasa a un visualizador, como teitadock nuestro monitoreo.
Si son muchos logs se va el precio, tener precaución con eso.




# Práctica: Monitorizar lo de la clase anterior
### Preparación

1. minikube:
	`minikube start` iniciamos minikube
	 
	`minikube addons enable ingress` agregamos el addons de ingress si no lo tenemos
	 
	 `minikube addons enable metrics-server ` que es el nativo de kubernetes para registrar metricas.
	 
	 `minikube addons list` para ver los addos activados.
	 
	 `minikube image load courseipap/backend:1.0.0` y `minikube image load courseipap/frontend:1.0.0` si no lo tengo en `minikube image list`
	 
	 
	 
	 
	 

2. Lo dejamos como la clase anterior:
	 
	 Una manera facil y rápida de desplegar todo lo de la clase anterior sin tener que ir uno por uno de los archivos, se coloco todo en una carpeta llamada labipap donde tiene todos los archivos de la clase anterior pero con una nomenclatura para que se ejecuten en orden (primero la ns, luego los secrets, ...). Para ello usamos `kubectl apply -f labipap`
	 
	 

### HPA

1. HPA el agregado de la clase anterior:
	
	 
	 `kubectl -n labipap get all` para ver si se levanto todo
	 
	 Con la diferencia que antes no aparecia el horizontalpodautoscaler, esto se encuentra en el archivo 05-backend-hpa.yaml que contiene, apiVersion autoscaler/v2, kind HorizontalPodAutoscaler, name backend-hpa,  spec kind deployment, minReplicas 1, maxReplicas 3, metrics type resource, resource name cpu, target type utilization averageUtilizatios 10 Como se ve esta hpa en 12%, por ende me creo mas pods, igualmente seguramente fueron creaods por el estres que sufre el cpu al crear todo el lab, por ende esperamos para ver como avanza y tiramos nuevamente `kubectl -n labipap get all`
	 
	 Luego revisamos que en el archivo 03-postgres-deployment-yaml tiene un apartado en el backend donde sale resources requests cpu 50m (solicita 50 milicores), limits cpu 100m (hasta 100 como maximo puede trabajar). Tambien se podria colocar memory para tambien colocarle cuanto puede usar. Cuando llega al limite va a ser como cuando se nos satura nuestra computadora, cuando se satura el cpu se vuelve lente, cuando es saturacion de memory puede reiniciarce. 
	 
	 `
	 
	 `kubectl -n labipap get all` para ver como consume de normal luego de ya haber arrancado, actualmente de 7% por ende nos vamos al 05 y a averageUtilizations lo subimos a  20 par ver como nos borra los pod que nos creaba para balancear. Ahora para aplicar los cambios `kubectl apply -f labipap` y volvemos a revisar
	 
	 
	 
	 
	 

### Monitoring

1. Nueva carpeta:
	 
	 Tenemos el archivo 01-pvc.yml que tiene unos pv (volumenes persistentes) uno para prometheus y otro para grafana.
	 
	 Tenemos el archivo 02-configmap.yaml para meter variables entre ellos, prometheus tendra variables y grafana tiene recoje esa información de prometheus. este configmap esta en un archivo aparte solo para que no este todo junto en el archivo 03-deploymen
	 
	 En esta carpeta llamada monitoring tenemos también archivos con nomeclatura para que se desplieguen en orden con `kubectl apply -f monitoring` 
	 
	 
   
   
   
   
   
   
   
   
   
   
   
   
	 Luego en otra terminal tiramos `minikube tunnel` y en otra nuevamente preguntamos si tenemos conexión con `curl `




---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
