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






---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1v9GjIZS6uk3JauRg4DBsPvfJWRie3iqT/view?usp=sharing