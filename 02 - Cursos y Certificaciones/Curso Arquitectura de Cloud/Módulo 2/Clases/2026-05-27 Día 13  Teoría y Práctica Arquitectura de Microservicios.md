# Teoría :Arquitectura de Microservicios

# Fundamentos Monolito - Microservicios

**Monolito:** un solo bloque de código, difícil de separar. Riesgos de que si se actualizara algo se rompiera todo o si se vulneraba se podría llegar a datos sensibles.

**Microservicios:** con los nuevos fundamentos en programación (con lenguajes más dedicados a ciertas áreas) se pudo empezar a trabajar con pequeñas cajitas separadas. Ej se saco la base de datos, se separa la parte front end y así con los otros servicios.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608002031.png)

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608010825.png)

# Fundamentos Autonomía de datos

Hay varias bases de datos para distintos servicios (autonomia de los microservicios), ej:

**Para Servicio Financiero:** base de datos estructurada como SQL, lenta a la busqueda porque busca linea por linea.

**Para Servicio Catálogo:** base de datos no estructurada noSQL, como un yaml, nos permite búsquedas rápidas.

**Para Servicio Usuario:** base de datos no estructurada Graph DB.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608011227.png)


# Nuevo desafíos: La Red

Monolito tiene el desafío en la capa de aplicación, porque los servicios empiezan a interactuan por APIs, red, etc. O sea que si se cae uno empiezan a caerse todos. Pero los microservicios no pasan por esto porque si pierden conectividad en un bloque no afecta al resto de servicios.
![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608012111.png)

# Patrones de diseño Disyuntor - Saga

Los sistemas distribuidos asumen que el fallo es la norma, no la excepción. Contruir resiliencia es nuestra responsabilidad.

Para evitar errores 500, se sigue este diseño (es buena práctica utilizar los dos dependiendo de la situación):

**Patrón Disyuntor:** sea un corto circuito o disyuntor. Si ocurre un error corta y aísla el error (sin cerrar aplicación se muestra una pantalla de "Estamos trabajando en el error, vuelva en unos minutos"). para prevenir esto hay que tener un buen sistema de monitoreo o alarmas.

**Patrón Saga:** busca que los datos estén correctos y sean correlativos. Si ocurre errores, hace arreglos en la base de datos.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608012734.png)

# Ejemplo Netflix - Disyuntor

Cuando les fallaba la sección de Tus Sugerencias, ponían las tendencias más vistas por todos los usuarios hasta volver a arreglarlo y ahí si mostrar tus preferencias según lo que veías. Por esto los usuarios no veían el error.
![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608014114.png)

# Ejemplo Reservas de vuelos - Saga

En las etapas de reservas, les deja completar las primeras pero en la última falla teniendo que generar un rembolso y liberación del asiento por el error final . 
![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608014141.png)

---

# Práctica: Demostrar cómo un fallo en un microservicio secundario agora los recursos del servicio principal y cómo aplicar una "Degradación Elegante" (Fallback)

### El Escenario

Tenemos dos servicios:

1. **Servicio de Órdenes (Frontend):** Recibe las compras del usuario.

2. **Servicio de Inventario (Backend):** Verifica si hay stock.

Simularemos que el Inventario se vuelve extremadamente lento (latencia de 10 segundos). Veremos cómo esto bloquea al Servicio de Órdenes hasta dejarlo inútil.

### Preparación

1. Se necesitara ciertas carpetas y archivos:
	Una carpeta llamada resiliencia que contendra el docker compose (para automatizar los run de los servicios). Una sub carpeta llamada app-inventario con un archivo app.py y un Dockerfile ( crea la imagen a mi gusto). Otra sub carpeta llamada app-ordenes que también tiene un app.py y su Dockerfile (con distinto puerto).

2. Arrancar el contenedor:
	`sudo docker compose up -d `






# Guía del Profesor

# Laboratorio Práctico: Microservicios y el Efecto Dominó

**Objetivo:** Demostrar cómo un fallo en un microservicio secundario agota los recursos del servicio principal y cómo aplicar una "Degradación Elegante" (Fallback).
  

## 1. El Escenario

Tenemos dos servicios:

1. **Servicio de Órdenes (Frontend):** Recibe las compras del usuario.

2. **Servicio de Inventario (Backend):** Verifica si hay stock.

  

Simularemos que el **Inventario** se vuelve extremadamente lento (latencia de 10 segundos). Veremos cómo esto bloquea al **Servicio de Órdenes** hasta dejarlo inútil.

  

---

  

## 2. Preparación de la "App Lenta"

  

Crea una carpeta llamada `lab-resiliencia` con la siguiente estructura:

```text

resiliencia/

├── compose.yaml

├── app-ordenes/

│ ├── app.py

│ └── Dockerfile

└── app-inventario/

├── app.py

└── Dockerfile

  

Nos paramos en resiliencia y desde ahi vamos a ejecutar el docker compose.

  

Luego ejecutremos:

curl localhost:5000/comprar

o

curl -w " - Status: %{http_code} - Tiempo: %{time_total}s\n" -s http://localhost:5000/comprar

  

Simulamos muchas compras:

for i in {1..50}; do curl -w " - Status: %{http_code} - Tiempo: %{time_total}s\n" -s http://localhost:5000/comprar; done;

  

Demora demasiado.

  

### Circuit braker - disyuntor

Entrar a:

├── app-ordenes/

│ ├── app.py

  

Comentar todo el bloque de codigo que esta en parte 1 y descomentar el bloque que esta en parte 2 guardar el archivo

  

Ejecutar nuevamente docker compose up build y proceder a ejecutar:

curl http://localhost:5000/comprar-resiliente

o

curl -w " - Status: %{http_code} - Tiempo: %{time_total}s\n" -s http://localhost:5000/comprar-resiliente

  

Tambien podemos probar:

for i in {1..50}; do curl -w " - Status: %{http_code} - Tiempo: %{time_total}s\n" -s http://localhost:5000/comprar-resiliente; done;

  

corre mas rapido.

---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1v9GjIZS6uk3JauRg4DBsPvfJWRie3iqT/view?usp=sharing