 # Teoría: CI CD Github Actions

# Fundamentos Los primeros pasos

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805095929.png)

Luego de ya tener la solución desplegada el objetivo final para el desarrollador sería tener que desplegar todo con git push. Git bueno para trabajar en equipo

# Fundamentos El infinito CI / CD

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805100500.png)

El camino continuo que se divide en dos partes, una vez que ya tengo mi código en git debe estar preparado para que solo se compile y ya este operativo:
- **Integración Continua (CI):** No hay que desarrollar de cero una vez que ya lo tenemos, para acceder a él utilizaremos un repositorio, se ejecutara para compilar y se puede detectar errores antes de desplegarlo como de sintaxis.  Cuando tengo todo esto es ideal publicarlo en un dockerhub, conteiner redit, yeifromt o netsus. 
- **Despliegue y Entrega (CD):** Ahora en el proceso de despliegue seria encontrar la cuenta de aws o local, crear ese servidor local y actualizarlo, también se pueden pruebas de conectarse a tal servicio ya desplegados, y ya quedaria desplegado automaticamente todo.
  
  Lo importante es que cuanto más pequeña sea la interacción menor riesgo a errores, se puede realizar más monitoreo para ir mejorando.
  
# Fundametos CI/CD - CD

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805101951.png)

- **Integración Continua (CI):** El desarrollador crea el código en un repositorio, yo me encargo de estar pendiente a cada cambio y probarlo.
- **Entrega Continua (CD):** Una vez empaquetado y listo lo puedo tomar y entregar a un servidor. En entornos bajos puede ser automatizada pero en entornos de producción no.
- **Implementación Continua (CD):**  Suele estar integrado en Entrega Continua (CD). Una vez todo automatizado en entornos bajos, aunque en producción de despliegue se tiene que hacer el humano un run manual, luego sigue automático.
 
# Fundamentos Integración Continua

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805104432.png)

1. Tengo a mi semáforo que será nuestro git, que podemos automatizarlo. A cada subida puss de código yo le indiqué que si encuentra algún error por ejemplo de sintaxis lo bloquee, o si esta todo bien lo permita pasar.

2. Embutido de Pruebas viene después que pase el semáforo, hará pruebas mínimas, análisis de datos como que no haya variables expuestas estaticamente, que haya seguridad y dependencias necesarias. 
  
  3. Luego de todas esas pruebas nos dará un build o artefacto (puede ser una imagen de docker, una librería, binario, etc ) valido y ejecutable
  
# Fundamentos Despliegue Continuo
  
  ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805105437.png)
  
  1. Un artefacto empaquetado listo para despachar.
  2. Contenerizar si esa es la solución, o puede ser pasarlo a una librería, etc. Un segundo estadio. creando la imagen.
  3. Orquestación puede busca ese artefacto, desplegar el docker y luego orquestarlo.
  
# Fundamentos Implementación Continua
  
  ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805105923.png)
  
 Ya estaría implementado y  validado, y es el usuario final quien  se encontrara con esa solución accesible. Se puede segmentar por algunos usuarios o grupos que pueden ver ciertas cosas. 
  
# Fundamentos Github Actions

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805110509.png)

**Github Actions:** es el motor de la solución, va a leer código en estructura yaml, su gran ventaja es que su estructurador yaml para indicarle que hacer, estas acciones generan eventos.  Es totalmente trasparente para nuestras pc ya sea windows, linux, mac, ya que solo es descargar git y empezar a escribir las actions. Gran comunidad y gran aportación de soluciones de acciones prefabricadas. 

# Fundamentos Actions por dentro

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805112106.png)

Como funciona este motor / cual es su arquitectura (mamusca):
- **Workflow:** tiene la receta completa, donde le dice a github que todo lo que esta aca son procesos que tenes que ejecutar.
- **Job:** dentro de Workflow tendremos un lugar de trabajo, como una maquina virtual o pensarlo con contenedor. que jaran pequeñas acciones. por ejemplo workflow indicara a github que cree una mv con ubuntu, y el job pues se creara con ese ubuntu.
- **Step (Run):** Son las tareas personalizadas que tiene que hacer ese job, por ejemplo run npm install.
- **Step (User):**  Son tareas empaquetadas, tareas creadas por la comunidad como por jemplo hacer un git pull a un código.


  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1wLu2AA2cR1V113Cc8-bZQConWFBE0z9b/view
