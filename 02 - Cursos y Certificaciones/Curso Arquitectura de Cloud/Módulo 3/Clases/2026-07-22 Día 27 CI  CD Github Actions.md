# Teoría: CI CD Github Actions

# Fundamentos Los primeros pasos

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805095929.png)

Luego de ya tener la solución desplegada el objetivo final para el desarrollador sería tener que desplegar todo con git push. Git bueno para trabajar en equipo

# Fundamentos El infinito CI / CD

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805100500.png)

El camino continuo que se divide en dos partes, una vez que ya tengo mi código en git debe estar preparado para que solo se compile y ya este operativo:
- **Integración Continua (CI):** No hay que desarrollar de cero una vez que ya lo tenemos, para acceder a él utilizazremos un repositorio, se ejecutara para compilar y se puede detectar errores antes de desplegarlo como de sintaxis.  Cuando tengo todo esto es ideal publicarlo en un dockerhub, conteiner redit, yeifromt o netsus. 
- **Despliegue y Entrega (CD):** Ahora en el proceso de despliegue seria encontrar la cuenta de aws o local, crear ese servidor local y actualizarlo, también se pueden pruebas de conectarse a tal servicio ya desplegados, y ya quedaria desplegado automaticamente todo.
  
  Lo importante es que cuanto más pequeña sea la interacción menor riesgo a errores, se puede realizar más monitoreo para ir mejorando.
  
# Fundametos CI/CD - CD

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805101951.png)

- **Integración Continua (CI):** El desarrollador crea el código en un repositorio, yo me encargo de estar pendiente a cada cambio y probarlo.
- **Entrega Continua (CD):** Una vez empaquetado y listo lo puedo tomar y entragar a un servidor. En entornos bajos puede ser automatizada pero en entornos de producción no.
- **Implementación Continua (CD):**  Suele estra integrado en Entrega Continua (CD). Una vez todo automatizado en entornos bajos, aunque en producción de despliegue se tiene que hacer el humano un run manual, luego sigue automático.
 
# Fundamentos Integración Continua

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260805104432.png)

1. Tengo a mi semáforo que será nuestro git, que podemos automatizarlo. A cada subida puss de código yo le indiqué que si encuentra algún error por ejemplo de sintaxis lo bloquee, o si esta todo bien lo permita pasar.

2. Embutido de Pruebas viene despues que pase el semaforo, hará pruebas minimas, analisis de datos como que no haya variables expuestas estéticamente, que haya seguridad y 
  
  
  
  
  
  
  
  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1wLu2AA2cR1V113Cc8-bZQConWFBE0z9b/view
