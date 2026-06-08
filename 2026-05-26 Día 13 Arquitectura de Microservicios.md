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

Desafío en la capa de aplicación, porque los servicios empizan a interactuar por APIs, etc. Pero si 
![](04%20-%20Otros/Imagenes/Pasted%20image%2020260608012111.png)