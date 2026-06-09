# Teoría: La era serverless & MLOPS
# Fundamentos El paradigma actual

El panorama antes era tener que gestionar absolutamente todo el servidor por cuenta propia. Ahora Serverless en delegar la gestión del servidor, enfocando nos en un código eficiente y sin necesidad de ir armando nuestros servidor, o sea, desarrollo y aws me lo da armado (infraestructura de código).

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608222118.png)

# Fundamentos Serverless y Faas

**Ecosistema de Serverless:** tenemos los tipos de motores de base de datos, gateway, balanceadores de carga, etc.
**FaaS (Function as a Service):** es el estándar dentro de serverless que nos da el poder de computo
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608224435.png)

# Fundamentos Los ejes

Lo que se busca son:
- **Foco en el Código:** no pensar en el hardware necesario.
- **Los Serverless se pagan por mili segundos:** solo se factura cuando se ejecute los códigos, sin cobrarte el tiempo ocioso.
- **Escalamiento Instantáneo:** puedo tener 0  a muchas arquitecturas creadas rápidamente y simultáneamente.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608225131.png)

# Fundamentos Ahorro extremo

Las base de datos tradicionales están prendidas 24/7, pero en entornos no productivos se pueden programar apagados. Y en caso en producción que tiene que estar activa 24/7 se puede hacer algunas configuraciones de picos de mas demanda y costo, junto con una base de consumo estandarizada. Ojo que siempre el almacenamiento y el poder de computo prendido será pago.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608230131.png)

# Fundamentos A tener en cuenta

Cuidado con el servicio serverless, el primer arranque puede tardar algunos segundos generando latencia y también hay tiempos de ejecución estándar de no más de 15 min, o sea que no esta pensado para correr cosas grandes de gran capacidad de procesamiento (además que empieza a ser muy cara a cada minuto que pase). 
Por ellos se usa por ejemplo Lambda para procesos que no tienen que tener latencias y ser super rápidas como los logins o que sea el pasa mano de ciertos datos.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608230857.png)

---
# Práctica: Muestra de opciones Serverless. Ver si un archivo se puede exportar según lo que pese con Lambda

Trabajaremos en la consola web de aws que nos servirá de contra punto para luego la práctica por código.

### Escenario

Tenemos un cliente que nos pide que provemos si puede subir un archivo CSV  y con una estructura se pueda usar lambda para que nos dé el peso del archivo y si se puede mover el archivo CSV.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609003540.png)


### SQS 

1. Creamos la Cola:
	Entramos a aws por web y ingresamos a Simple Queue Service. Que son las colas de procesos que esperan a que el Lambda los procese. Le damos a crear Cola y completamos los campos necesarios. Nos ayudan para los arranques en frio.
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608233840.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608233928.png)
	 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260608234006.png)
	Estándar es el orden de tráfico que el primero que entra es el primero que sale.
	Fifo: es el orden de tráfico que el último que entra es el primero que sale


### SNS

1. Creamos SNS
	nos vamos a Simple Notification Service, que es un cartero enviando notificaciones de un lado a otro, también nos ayudan un poco con los arranques en frio.
	Topicos(temas) es el cartero que tendra subcripciones que son sus direcciones asignada donde ira punto a punto. nos creamos un topico.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609002030.png)
	Una vez creado el topico, le creamos una subscripción para que trabaje con nuestro SQS indicandole su ARN (Identificador único)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609002545.png)
	Al crear la subscripción saldra que se subscribió correctamente pero por si llegase a fallar tendríamos que ir otra vez a SQS para modificar las políticas de acceso y agregarle este código.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609003018.png)
	

### S3 

1. Creamos el S3 Buckets
	nos vamos a S3 (nuestro almacenamiento) y le damos a crear Bucket
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609004343.png)
	El nombre no tiene que estar usado por nadie en el mundo.
	Una vez creada nos vamos a sus propiedades y nos vamos a event notifications para crearle una notificación. Nos permite poder si hay alguna ruta en expesifico que quiero que me alerte o que tipo de eventos me aviso como cuando se crea a

Nombre: ColaProcesamientoS3
ARN(Identificador unico) : arn:aws:sqs:us-east-1:632914961478:ColaProcesamientoS3
Topic: NotificacionesS3
arn:aws:sns:us-east-1:632914961478:NotificacionesS3
