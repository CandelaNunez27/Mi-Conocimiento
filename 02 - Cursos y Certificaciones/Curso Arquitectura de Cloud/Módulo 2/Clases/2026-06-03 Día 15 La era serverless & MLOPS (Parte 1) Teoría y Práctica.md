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
# Práctica: Muestra de opciones Serverless. Ver si un archivo se puede exportar segun lo que pese con Lambda

Trabajaremos en la consola web de aws que nos servirá de contra punto para luego la práctica por código.

### Preparamos la Cola de espera 

1. Creamos la Cola:
	Entramos a aws por web y ingresamos a Simple Queue Service. Que son las colas de procesos que esperan a que el Lambda los procese. Le damos a crear Cola y completamos los campos necesarios.
	 
	