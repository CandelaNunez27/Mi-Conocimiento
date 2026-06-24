# Teoría: Conceptos básicos y Flujos de Trabajo Local

# Fundamentos Containerización

La transicion estructural de configurar sistemas operativos complejos a empaquetar de forma segura procesos efimeros e independientes.


# Fundamentos El finde de: En mi PC funciona

El tipico caso de desplegarlo en mi computadora y en servidor ya no. Esto pasa porque la computadora del desarrollador tiene el Framework perfecto y anduvo, ya el servidor le puede faltar una libreria o siemplemente tienen distintos S.O. Para esto nos sirve containerizar.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624180427.png)

# Fundamentos VM vs Containers

Containerizar no necesita un hypervisor ni otro sistema operativo. Docker utiliza el hardware sin tener que simularlo, aislando por servicios / procesos independientes una de la otra. Como base de datos no tendría que estar en containers.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624180335.png)

# Fundamentos El motor

Con la terminal mandamos las instrucciones al daemon (proceso que corre en segundo plano) de docker para que realice las tareas, crea y destruye los contenedores también gestionando recursos del kernet.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624182411.png)

# Fundamentos Los 3 pilares de Docker

Se utiliza la analogía de un restaurante
- **Dockerfile (La receta):** las instrucciones paso a paso para realizar las tareas para generar una imagen de lo que se quiere.  Importante para poder replicarlo y que funcione en todos lados.
- **Imagen (El pastel congelado):** Resultado  de ejecutar la receta que nos da lo que queremos pero sin realizar nada con el aun.
- **Contenedor (El pastel Servido):** El resultado ya puesto en marcha, siendo utilizado para su función.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624182900.png)

# Fundamentos La receta desde dentro Dockerfile

Siempre arranca con el termino `FROM` para de esa manera descarga la imagen, por ejemplo una parte pequeña de ubuntu para utilizar python, sin necesidad de utilizar iso pesadas.
`WORKDIR` Le indicamos la carpeta base del usuario y `COPY` es para copiar un archivo para el director de trabajo. 
`RUN` Sirve para indicarle que haga o corra alguna acción, cualquier comando.  `COPY . .` Es copiar todo el directorio hasta el dockerfile, cuidado porque se puede copiar cosas que no queremos, aunque se utiliza para proyectos grandes.  Suele ser la última linea del dockerfile, aunque puede estar o no, `CMD ["", ""]` suele para dejar un proceso activo en segundo plano, solo funciona cuando le damos `docker start`.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624183220.png)


# Fundamentos Dockerhub 

Es un repositorio que contiene muchas imágenes listas para descargar y usar. Cuidado por empresas más grandes por los limites de descarga en capa gratuita.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624184441.png)


# Fundamentos Docker Compose

Es un agregado que se descarga aparte, siendo el mejor amigo de docker para gestionar varios dockers que se quieren comunicar. No los orquesta simplemente los ordena. Tiene un limite al escalamiento, pero si nos permite lanzar varios docker a la vez de forma ordenada con un solo comando.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624185240.png)


# Fundamentos Comandos

- `docker build -t mi-app .`: build es quien transforma el dockerfile en imagen, -t es para agrarle un nombre a la imagen, y el . es para indicarle que el dockerfile esta en el directorio actual.
- `docker run -d -p `

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260624185339.png)












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

**Clase Grabada:** https://drive.google.com/file/d/1JFjlDQ5OMTTrGijM0gEDE21sfv4Yizzs/view 
