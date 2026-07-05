# Teoría: Continuamos con Docker 

# Repasamos Flujo completo de Docker

Este seria el flujo, se suele descargar una docker hub pero ya luego se suele configurar y ya quedaria una versión nuestra. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260703232949.png)
# Fundamentos Docker - Compose

Docker compose no orquesta sino que dirige un poco los despliegues, para pocos dockers. Ya cuando uno quiere configurar puertos, variables de entornos (environment), pasar vasriables, declarar volumenes, que conllevan muchas linea a escribir y un simple error de tipeo hace que no ande. 
Pero docker compose me da la posibilidad, como el ejemplo de la imagen, puedo organizar que me cree a la vez ambos conteiners y encima que me los ordene, para acegurarse de no lanzar a node.js sin que no este lista ya el postgreSQL. 
Un orquestador entiende cuando tiene que crecer y cuando no, de manera automatica en base de algunas medidas que le configuremos. En cambio, un docker compose solo va a organizar como los tengo que crear, levantar, y el escalado tiene que ser manual indicandole al docker compose reescribiendolo. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260703235532.png)

# Evolución Networking

El networking en contenedores: es posible separaciones de conexiones en cada docker.
- Cuando no sé le coloca nada queda en modo **bridge**, asiendo de puente. El docker conecta interfaces virtuales a las computadores/servidores.
- **Host** elimina la conexion y el docker trabaja directamente con el hardware local donde este desplegado, se suele usar mucho para servidor proxy (intermediario entre tu dispositivo e internet)
- **Overlay** nos permite crear una pequeña subred que nos deja que varios contenedores expongan en el mismo puerto. Se necesitaria un proxy para hacerlo, siendo la base de los orquestadores como kubernetes para que  varios esten en un puerto y no se pisen. Casi no se usa en docker ya que seria más para orquestadores.
- Para un aislamiento total se utiliza **none**. se utiliza para contonedores efimeros para tareitas pequeñas.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260704001102.png)

# Evolución Volúmenes

Los docker son efimeros, los datos no deben ser permanentes. Si contenia algun dato y se reinicio o apago y prendio, ya no tenes los datos porque vuelve a cero nuevito.
Para lograr recuperar algunos datos, como logs, se le asigna un volumnen (como un espacio de disco, mas bien una ruta de una carpeta montandola, no es tanto como maquinas virtuales que le asignas una cantidad de disco). 
Esta idea de efimero sigue tambien para los orquestadores.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260704004133.png)

# Buenas Prácticas Eficacia y Seguridad

- Cuidar el tamaño de las imagenes con la Herramienta Multi-stage builds, genera imagenes en etapas para que de la imagen completa solo se usé una imagen chiquita que fue la última con el resultado final del despliegue. Tambien ganaría velocidad al subir y bajar cuya imagen.
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260704013722.png)

- Minimos privilegios, tratar de que nunca el usuario root sea el usuario de ejecución. Ya que se si se vulnera algun contenedor que opera en root, podria saltar con ssh a los servidores de arriba.
- Escaneo continuo de las imagenes, ya que hay que tener actualizada o migradas las versiones para que esten con las biblotecas parcheadas.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260704004829.png)

# Práctica: sawkl
### Preparación

1. Copiamos los mismos archivos de la práctica anterior:
	Dos carpetas una llamada front y otra back. (`mkdir front back`). 
	
	En front tendremos los archivos: index.html (`touch index.html`) que tendra una pequeña configuración html con su body y escuchando en la ruta http://localhost:3000/api/data  , Dockerfile (`touch Dockerfile`) que tendra el FROM con nginx:alpine COPY index.html /usr/share/nginx/html EXPONSE 80.
	
	En back tendremos los archivos: Dockerfile (`touch Dockerfile`) FROM node;18-slim WORDIR /app COPY package.json ./ RUN npm install COPY . . EXPOSE 3000 (puerto por defecto de node) CMD ["npm", "start"] , package.json (`touch package.json`) con unas dependencias, index.js (`touch index.js`) js porque es en back.

---
# Guía del Profesor

  Módulo 3 - Clase 2: Parte 2

  

🎯 Objetivo del Laboratorio

  

El alumno tomará la arquitectura web del Laboratorio anterior y la optimizará bajo estándares profesionales de producción:

  

Aislamiento de Redes (Networking): Separará la comunicación en dos redes independientes de forma que la Base de Datos sea totalmente invisible para el Frontend o el exterior, reduciendo el área de ataque.

  

Persistencia (Volúmenes): Integrará volúmenes locales gestionados por Docker para asegurar que los datos de Postgres sobrevivan a la destrucción del contenedor.

  

Optimización extrema (Multi-stage Build): Reestructurará los Dockerfiles utilizando compilación de múltiples etapas, reduciendo drásticamente el peso de las imágenes finales de producción.

  

🗺️ Arquitectura de Red Aislada (Fase 2: Producción)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260705003533.png)

















---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1MhUkOfLbEgU0p18UHXuEaOCZvJZ57n4_/view
