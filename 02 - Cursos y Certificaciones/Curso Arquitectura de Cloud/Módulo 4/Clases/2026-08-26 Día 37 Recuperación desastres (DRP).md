# Teoría: Recuperación desastres (DRP)

# Fundamentos Resiliencia

Asumir que las cosas fallan y planificar que hacer en esos eventos. 
- Desastres naturales: corte de luz, internet, sismos, incendios.
- Ataques masivos de Ransomware o ciberataques: base de datos son tentativos o para minería.
- Errores humanos: algo desconectado

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260930014723.png)


# Fundamentos RPO - RTO

- RPO (Recovery Point Objetive): la máxima de datos que acepto perder. por ejemplo entre que hago un back up a otro tengo una hora de proceso, por ende ese es mi rango que acepto perder. 
- RTO (Recovery Time Objetive): el maximo de tiempo que acepto que puedo estar caído, por ejemplo establezco que de RTO solo tener 20 min de caía para volver a estar operativo.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260930015512.png)


# Fundamentos Evento Cero (datos vs velocidad)

Buen monitoreo para darnos cuenta del evento comenzó y esta en el momento 0. Por ende se evalúa varios aspectos, principalmente el costo. Para RPO tener menos perdida de datos es un gran costo porque requiere back up más grandes y frecuentes (más espacio de almacenamiento). Para RTO tener menos inactividad es un gran costo porque requiere un mayor trabajo constante del empleado para que vuelva el servicio.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260930020045.png)


# Fundamentos RPO

Enfocado a la protección de los datos midiendo en tiempo. su mecanismo en principalmente el backup volviendo para atras perdiendo una franja horaria, cada más antiguio sea el backup menos costo pero más perdida de datos. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260930020830.png)

# Fundamento RTO

Enfocada en la continuidad del negocio y la funcionalidad a futuro. su mecanismo es establezer un tiempo estimado que los técnicos tendran que volver a dejar el sisntema operavito, por ende se hacen sistemas redundantes, conmutación y arquitectura de alta disponibilidad, para solucionar problemas variados que pueden ser hardware, software, humano. Mientras mejores sean las soluciones serán más costosas pero con la ganancia de poco tiempo de inactividad.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261001234835.png)


# Fundamentos La nube y la resiliencia

Hablando de RTO, unas de las mejores soluciones para continuidad es la nube. También es bueno tener redundancia de varios proveedores, tener dos datacenter separados físicamente o simplemente la nube. Tener nuestra estructura en varias regiones, servicios de base de datos que hacen backup, las base de datos casi siempre tienen dos nodos donde uno es readonly y otro tiene acceso a escritura, pero el readonly puede ser resilientes al otro teniendo muy poca perdida de datos al sustituir al otro, y ademas seguros para usar el readonly porque así no modificamos sin querer algo. 
Migrar a la nube se trata de buscar con más facilidad que lo que se pueda lograr con on-prime

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002001645.png)

# Fundamentos Estrategias de Recovery

- Backup y Restore: Bajo costo de inversión pero perdida de tiempo ya que es lento por emde más tiempo de inactividad.
  
  ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002124700.png)
  
- Pilot light: mantiene una versión mínima de la infraestructura crítica ejecutándose constantemente en una región o entorno secundario. Esta configuración "llama piloto" siempre encendida, permite escalar rápidamente a un entorno de producción completo en caso de interrupción.
  
  ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002124854.png)
  
  
  
- Warm Standbly: es parecido a pilot light pero esta apagado, con mucha más grande cantidad. se apaga el que falla y se levanta el warm standbly.
  
  ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002124909.png)
  
  
  
  
- Multi-Site: duplicación 100% y manejado 100% de manera activca y que entre ellos no sé pisen o rompam.

  ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002124937.png)


![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002004006.png)


# Fundamentos DRP vs BCP

- DRP (Plande recuperación de desastres): conjunto de BCP (Plan de continuidad de negocio) con la Norma ISO 22301. 
- La comunicación es fundamental para unas buenas primeras acciones, luego los roles para ver quien se encarga de qué acción y no se pisen. La logística para que el personal clave siga funcionando.


![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002130800.png)


# Fundamentos Pruebas Obligatorias

Hay que prácticar los planes porque a la hora que el escenario se vuelva realidad no sabremos si realmente el plan nos solucione o sea una perdida de tiempo. Para prácticar se usa aws fault injection simulator y Chaos Monkey de Newtflix

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002131719.png)


# Conclusión



![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020261002132109.png)






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

**Clase Grabada:** https://drive.google.com/file/d/1bjgIR5RZFhqW6vqOX_tRtSvtKXLXAPi4/view
