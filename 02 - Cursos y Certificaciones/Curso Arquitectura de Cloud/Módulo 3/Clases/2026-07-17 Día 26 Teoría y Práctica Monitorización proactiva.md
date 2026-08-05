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
	 
	 Tenemos el archivo 02-configmap.yaml para meter variables entre ellos, prometheus tendra variables y grafana tiene recoje esa información de prometheus. este configmap esta en un archivo aparte solo para que no este todo junto en el archivo 03-deployments.yaml y por si me equivoco tipeando en el configmap no implique al deployment
	 
	 Tenemos el archivo 03-deployments.yaml apartado de prometheus con spec replicas 1, spec serviceAccountName prometheus-sa, containers .. port 9090 volumesMont. Para grafana parecido, tenemos  spec replicas 1, spec containers .. port 3000 volumesMont. Luego tenemos los servicios para conectarlos a estos dos que prometheus expone el puerto 9090 y el servicio de grafana que expone el puerto 3000.
	 
	 Tenemos el archivo 04-rbac.yaml que tiene kind ServiceAccount que es como un usuario de servicio ficticio que le damos indicaciones para que haga. Crea un kind ClusterRole que podra agarrar a los pods, los services y los endpoints, donde se les hará get, list y watch. esto porque prometheus necesita ingresara al kubernetes y hacer esas accciones para luego presentar esa información a grafana. Luego tenemos un kind ClusterRoleBinding que solo es para que el usuario sea atachado con ese role, se indica la api.
	 
	 En esta carpeta llamada monitoring tenemos también archivos con nomeclatura para que se desplieguen en orden con `kubectl apply -f monitoring` 
	 
	`kubectl -n labipap get sa` para ver los serviceaccount
	 

2. Generar logs 
	 `kubectl -n labipap get all` para ver como consume ahora
	 
	 en otra terminal tiramos `minikube tunnel` para tener conexión
	 
	 en otra termina tiramos `kubectl port-forward svc/grafana 3000:3000 -n labipap` nos tomara la consola
	 
	 en otra terminal tiramos `kubectl port-forward svc/prometheus 9090:9090 -n labipap` nos tomara la consola
	 
	 en otra consola tirar `curl localhost:3000` nos saldrá en la terminal de grafana handling. 


3. Primeras visualizaciones
	 
	 luego en el navegador colocamos `http://localhost:3000`  colocándole de contraseña y usuario por primera vez admin, admin. y en otra pestaña tendremos `http://localhost:9090` donde nos vamos a Status > RuleHeath. 
	 
	 En Grafana le damos al menú lateral DashBoards > Create DashBoard > le damos al + > config visualization > le indicamos que se muestre los ultimos 15 min > le damos a code >  escribimos este query `up{job="kubernetes-pods"}` > run queries > elejimos el trablero de tarjetas de 1s y 0s > a ese le colocamos que la base sea de color rojo, que si dice 1 colocarle verde > le colocamos panel status > save > colocarle nombre Status > save. Ahora nos vamos dashboar y deveria aparecer > le colocamos que muestre los últimos 15 min
	 
	 se compara con lo que muestra el grafico con lo que muestra la consola, `kubectl -n labipap get all`  y chequeamos que muestren los mismos pods
   
4. Resiliencia nuevamente pero ahora la visualizamos:
	 
	 En otra terminal tiramos `curl localhost` nos mostrara el mini-comerce
	 
	`curl localhost/api/data` si esta vacía tiramos un registro 
	 
	 `curl -X POST http://localhost/api/data -H "Content-Type: application/json" -d '{"nombre": "Estudiante", "clase": "Kubernetes"}' ` (`curl -X POST http://192.168.58.2/api/data -H "Content-Type: application/json" -d '{"nombre": "Estudiante", "clase": "Kubernetes"}'`)  para ver que se guardo con éxito ejecutamos `curl localhost/api/data` (`curl 192.168.58.2/api/data`) y nos sale.
	 
	 en una terminal dejamos corriendo `while true; do curl -s http://localhost/api/data; echo ""; sleep 1; done` (`while true; do curl -s http://192.168.58.2/api/data; echo ""; sleep 1; done`) (`watch -n 1 curl -s http://192.168.58.2/api/data`) esto nos toma la consola para mostrar los resultados en vivo
	 
	 en otra terminal revisamos como genera carga el comando anterior, `kubectl -n labipap get all` para ver como consume ahora
	 
	 En otra terminal se puede estresar al cpu con este comando `kubectl get hpa -w -n labipap`  o con nos `while true; do curl -s http://localhost/api/data > /dev/null; done` tomara la consola
	 
	 vemos que tal esta en cpu `kubectl -n labipap get all` vemos cuantos pod creo y nos vamos a grafana con un refresh para ver si se ve en el monitoreo, 
	 
	 
	 Tiramos un en otra terminal ``kubectl port-forward pod/backend-ashdklajsd 3000:3000 -n labipap`
	 en navegador por `http://localhost:3001` y `http://localhost/api/data`
	 

5. Vamor apagando las cosas de saturacion:
	 vemos que tal esta en cpu `kubectl -n labipap get all`
	 
	 contamos el `while true; do curl -s http://localhost/api/data > /dev/null; done`  y volvamos a revisar.
   
   Conclusiones: los logs los crea kubernetes con el addons metrics-server> prometheus los puede leer porque tiene los permisos para leerlos y los almacena en una pequeña base de datos por ello el pvc > y grafana los lee dese los pvc donde se almacenan los datos

### Borramos todo

1. Manera sencilla para borrar todo:
	 `kubectl delete ns labipap` automáticamente ira borrando todo. porque borramos la mamusca mas grande que contenía todo. comprobamos con `kubectl get all -labipap`



---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/17VGX1Fcr7mnPzqJK-KokNMgsOt7qBvmb/view
