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
	
	Una vez creada nos vamos a sus propiedades y nos vamos a event notifications para crearle una notificación. Nos permite poder si hay alguna ruta en expesifico que quiero que me alerte o que tipo de eventos me aviso como cuando se crea algun objeto y muchas más opciones de configuración.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609005226.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609005253.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609005410.png)

### Lambda

1. Creamos Lambda
	Nos vamos a Lambda y le damos a crear una función. Donde será nuestro poder de computo,
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609005845.png)
	Al crearla nos saldra una ventana de visual studio code y colocaremos este código:
	``` python
	import json

  

def lambda_handler(event, context):

# SQS envía los mensajes agrupados en una lista llamada 'Records'

for record in event['Records']:

# 1. Extraer el cuerpo del mensaje (body)

body = json.loads(record['body'])

# 2. Desglosar la estructura del mensaje que vino desde SNS

if 'Message' in body:

sns_message = json.loads(body['Message'])

# 3. Extraer la información del archivo subido a S3

if 'Records' in sns_message:

s3_info = sns_message['Records'][0]['s3']

bucket_name = s3_info['bucket']['name']

file_key = s3_info['object']['key']

file_size = s3_info['object']['size']

print(f"🚀 [PROCESADOR] ¡Nuevo archivo detectado!")

print(f"📁 Bucket: {bucket_name}")

print(f"📄 Archivo: {file_key}")

print(f"⚖️ Tamaño: {file_size} bytes")

return {

'statusCode': 200,

'body': json.dumps('Procesamiento completado con éxito')

}
	```
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609013006.png)
	
	Y nos programa el proceso de como ingresa el archivo y que nos devuelve el volumen del archivo. Luego le damos Deploy para que se guarde
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609013343.png)
	Ahora le agragamos el Trigger (desencadenador) que es el SQS, para ello nos vamos a add trigger, donde nos tirara un error pero podemos ver como la inteligencia artificial de amazon no lo resuelve.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609013851.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609014042.png)
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609014135.png)
2. Solución con la IA
	Nos vamos a IAM, Roles y buscamos "ProcesadorMensajesSQS-role-g0bqf8eo", en permisos le damos a crear politicas insertadas
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609014604.png)
	
	Seleccionamos que es json y le colocamos el código que nos describe.
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609015049.png)
	
	Luego, le colocamos un nombre y la creamos
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609015318.png)
	y ahora volvemos a intentar agregar el trigger
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609015616.png)
	

### Prueba si nuestro caminito funciona

1. Monitoreo
	dentro del lamda nos vamos a Monitorear, le personalizamos para que muestre 30min
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609015958.png)

2. SQS
	En otra pestaña nos vamos a SQS, también nos vamos a monitoreo y a 30min
	![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260609020426.png)

3. S3
	En otra pestaña nos vamos al S3, Y le subimos el archivo CSV que tengamos
Nombre: ColaProcesamientoS3
ARN(Identificador unico) : arn:aws:sqs:us-east-1:632914961478:ColaProcesamientoS3
Topic: NotificacionesS3
arn:aws:sns:us-east-1:632914961478:NotificacionesS3



---
# Guía del Profesor

  

# Paso a Paso para la Configuración Manual en AWS

  

## Paso 1: Crear la Cola SQS (El Amortiguador)

  

Ve al servicio SQS (Simple Queue Service) en la consola de AWS.

  

Haz clic en Create queue.

  

Selecciona tipo Standard, nómbrala ColaProcesamientoS3 y deja el resto de valores por defecto. Haz clic en Create queue.

  

Copia el ARN de la cola (lo necesitarás más adelante).

  

## Paso 2: Crear el Topic de SNS (El Distribuidor)

  

Ve al servicio SNS (Simple Notification Service).

  

Selecciona Topics -> Create topic.

  

Selecciona tipo Standard, nómbralo NotificacionesS3 y haz clic en Create topic.

  

Suscribir la Cola SQS al SNS:

  

Dentro del Topic, haz clic en Create subscription.

  

En Protocol, selecciona Amazon SQS.

  

En Endpoint, pega el ARN de tu cola SQS ColaProcesamientoS3.

  

Haz clic en Create subscription.

  

Nota de seguridad: Para que SNS pueda escribir en SQS, ve a tu cola en SQS -> pestaña Access policy -> Edit, y añade permisos para que la cola acepte acciones SendMessage desde tu ARN de SNS.

  

## Paso 3: Crear el S3 Bucket y vincular las alertas

  

Ve a S3 y haz clic en Create bucket. Nómbralo con un prefijo único (ej: formatec-ingesta-datos-2026).

  

Ve a la pestaña Properties del Bucket.

  

Baja hasta la sección Event notifications -> Create event notification.

  

Nómbrala AlertaArchivoS3, marca la opción All object create events (peticiones PUT/POST).

  

En la sección de Destination, selecciona SNS Topic y elige tu topic NotificacionesS3. Haz clic en Save changes.

  

## Paso 4: Crear la Función Lambda y Configurar sus Permisos de IAM

  

Ve a Lambda -> Create function.

  

Nómbrala ProcesadorMensajesSQS, selecciona Python 3.11 como Runtime.

  

En el código de la función (lambda_function.py), pega el siguiente código de procesamiento:

  

import json

  

def lambda_handler(event, context):

# SQS envía los mensajes agrupados en una lista llamada 'Records'

for record in event['Records']:

# 1. Extraer el cuerpo del mensaje (body)

body = json.loads(record['body'])

# 2. Desglosar la estructura del mensaje que vino desde SNS

if 'Message' in body:

sns_message = json.loads(body['Message'])

# 3. Extraer la información del archivo subido a S3

if 'Records' in sns_message:

s3_info = sns_message['Records'][0]['s3']

bucket_name = s3_info['bucket']['name']

file_key = s3_info['object']['key']

file_size = s3_info['object']['size']

print(f"🚀 [PROCESADOR] ¡Nuevo archivo detectado!")

print(f"📁 Bucket: {bucket_name}")

print(f"📄 Archivo: {file_key}")

print(f"⚖️ Tamaño: {file_size} bytes")

return {

'statusCode': 200,

'body': json.dumps('Procesamiento completado con éxito')

}

  
  

Haz clic en Deploy.

  
  

## Paso 5 Agregar el Trigger de SQS:

  

Regresa a la consola de tu Lambda -> pestaña Function overview -> Haz clic en Add trigger.

  

Selecciona SQS y busca tu cola ColaProcesamientoS3.

  

Deja los valores por defecto (Batch size: 10) y haz clic en Add.

  
  

## ⚠️ ¡PASO CRÍTICO DE SEGURIDAD (IAM)! > Para que el trigger de SQS funcione y la Lambda pueda consumir los mensajes, el rol de ejecución de tu Lambda (ej: ProcesadorMensajesSQS-role-xxxx) debe tener permisos explícitos sobre tu cola de SQS.

  

Cómo resolverlo de forma manual:

  

Ve a la pestaña Configuration de tu Lambda -> Permissions -> Haz clic en el nombre del rol bajo Execution role para abrirlo en la consola de IAM.

  

Haz clic en Add permissions -> Create inline policy (o Attach policies).

  

En la pestaña JSON, pega la siguiente política de acceso (SQSQueueAccessPolicy), asegurándote de reemplazar el ARN por el de tu propia cola SQS:

  

{

"Version": "2012-10-17",

"Statement": [

{

"Effect": "Allow",

"Action": [

"sqs:ReceiveMessage",

"sqs:DeleteMessage",

"sqs:GetQueueAttributes"

],

"Resource": "arn:aws:sqs:us-east-1:609898226152:ColaProcesamientoS3"

}

]

}

  
  

(Alternativamente, puedes adjuntar la política administrada oficial de AWS llamada AWSLambdaSQSQueueExecutionRole que ya contiene estos permisos de forma genérica).


