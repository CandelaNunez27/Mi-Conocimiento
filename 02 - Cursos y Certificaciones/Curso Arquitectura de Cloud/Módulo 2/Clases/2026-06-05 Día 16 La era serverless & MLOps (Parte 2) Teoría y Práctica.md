# Teoría: La era serverless & MLOps

# Fundamentos El código como base
No se utiliza los clics en interfaz web (peligro con los clics erróneos) sino por código. Definimos servidores,redes, bases de datos, roles y todo servicio, mediante archivos de texto plano que pueden ser versionados, revisados y automatizados. El crear la receta mayor se hará una única vez (dedicar tiempo en el desarrollo) y ya se puede cuantas veces querramos.

Se usa terrafor, con lenguaje compilado? se puede utilizar con docker.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260619235908.png)

# Fundamentos Infraestructura como código (IaC)
Se busca que la estructura sea escrita, se puede versionar para usar en github para que varios trabajadores trabajen en conjunto, aprovisionar con códigos para que cloud pueda implementar la arquitectura.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620000217.png)


# Fundamentos Paradigma IaC

- **Imperativo:** La forma como se va a ejecutar, tiene un orden que lee de arriba hacia abajo.
- **Declarativo:** Se le indica lo que uno quiere y no importa en que orden lo ejecute, simplemente que lo realice.

- **Mutable:** Si podemos modificar las cosas existentes con parches en caliente, como cambiar nombre de algo. Puede generar inconsistencia.
- **Inmutable:** Se debe borrar y subir ahora con las modificaciones. Garantiza coherencia absoluta. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620003425.png)

# Fundamentos Ahorro extremo
El MLOps aparecion con los distintos modelos (machine learning, ...). machine learning usa mucho el servicio serverless. El MLOps era una tarea de full stack developer (saber de front y back), pero no remplaza  a los que trabajan en cloud. 

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620004307.png)

# Fundamentos Básicos de IaC
Aparece Terraform que nos sirve para tener una arquitectura modificable. Si el desarrollo esta en aws y se quiere pasar a azure se debe cambiar algunos nombres nada más, por ende es facil el traspaso.  
Para que funcionen los comandos de terraform se debe tener un archivo.tf, para descargarse los plugins, librerias y demas para instalarse.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260620004449.png)

# Práctica: Muestra de opciones Serverless. Ver si un archivo se puede exportar según lo que pese con Lambda





---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1vMSbi1o2G3Lvbl50E0jDVKwOe_LDtBkD/view?usp=sharing
