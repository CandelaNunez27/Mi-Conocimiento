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

**Clase Grabada:** https://drive.google.com/file/d/1MhUkOfLbEgU0p18UHXuEaOCZvJZ57n4_/view
