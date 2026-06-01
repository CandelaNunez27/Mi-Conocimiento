# Módulo 4

## 1 Introducción

**GUI (Interfaz Gráfica)**
Se controla haciendo clics. Es una forma fácil de administrar el sistema y resulta indispensable para trabajar con gráficos o videos.

 **CLI (Línea de Comandos)**
Se controla únicamente mediante el teclado. Aunque al principio cuesta porque exige memorizar comandos , ofrece mayor velocidad, un control más preciso y la capacidad de automatizar tareas (mediante scripting).

**¿Por qué elegir la CLI?:** 
Por la flexibilidad y movilidad que otorga. Si dominas la consola, serás capaz de operar de manera eficaz CUALQUIER distribución de Linux en cualquier empresa, sin depender de la interfaz gráfica que tengan instalada

---
## 2 Interfaz de Línea de Comandos (CLI)

La CLI es una interfaz basada en texto que funciona mediante el trabajo en equipo de dos elementos clave:

- El Terminal: Es la aplicación visible donde el usuario escribe los comandos y donde aparecen los resultados o los mensajes de error. Su función es tomar ese texto y pasárselo al shell.

- El Shell: Es el intérprete del sistema. Recibe el texto enviado por el terminal y lo traduce a instrucciones reales que el sistema operativo puede ejecutar

---
### 3 Acceso a la Terminal

El acceso a la línea de comandos depende de cómo inicie el sistema:

- Arranque Directo (Servidores): Inician directamente en la consola de texto para no desperdiciar recursos gráficos y maximizar la velocidad.

- Terminal de GUI: En sistemas con escritorio, es un programa que emula la terminal y se abre fácilmente desde los menús.

- Terminal Virtual: Es una consola pura que se ejecuta en paralelo a la interfaz gráfica. Se accede mediante atajos de teclado (como `Ctrl-Alt-F1`) y te exige iniciar sesión nuevamente antes de usarla. Puede no estar disponible si usas máquinas virtuales.

---
### 3.1 El Prompt (Símbolo del sistema)

El prompt es el indicador visual que aparece en la terminal cuando el sistema ha terminado de ejecutar cualquier proceso y está listo para que introduzcas un nuevo comando.

Aunque su aspecto puede variar según la distribución de Linux, normalmente proporciona información de contexto muy útil. Tomando como ejemplo la estructura `sysadmin@localhost:~$`:

- `sysadmin`: Indica el nombre del usuario que tiene la sesión iniciada.
- `localhost`: Es el nombre del equipo o sistema en el que estás trabajando.
- `~` (Tilde): Muestra el directorio actual en el que te encuentras. En el mundo Linux, este símbolo es una abreviatura universal para referirse al directorio personal (o home) de tu usuario (por ejemplo, `/home/sysadmin`).

---
### 3.2 El Shell

El shell es el intérprete del sistema: se encarga de traducir los comandos que escribe el usuario en acciones reales que el sistema operativo ejecuta. En Linux el más utilizado por defecto en las distribuciones es el BASH shell. Sus características y funciones principales incluyen:

- Historial de comandos: Recuerda el registro de lo que has escrito, permitiéndote volver a ejecutar comandos previos de forma rápida.

- Scripting: Permite guardar secuencias de comandos en un archivo para ejecutarlos todos a la vez. Además, soporta funciones de programación puras (como condicionales y subrutinas).

- Alias: Permite crear atajos o "apodos" cortos para ejecutar comandos largos o complejos.

- Variables: Se usan para almacenar información vital del sistema que el shell utiliza para modificar el comportamiento de los comandos y funciones.

---
### 3.3 El Formato de los Comandos

La estructura estándar de una instrucción en Linux es: `comando [opciones] [argumentos]`

- Comando: La acción principal que deseas ejecutar (ej. `ls` para listar).
- Opciones: Modifican cómo actúa el comando.
- Argumentos: Indican el objetivo sobre el cual recae la acción, como un archivo o la ruta de un directorio.

**Regla de Oro:** Linux es case-sensitive (distingue mayúsculas de minúsculas). Debes escribir comandos, opciones y argumentos exactamente como corresponden, ya que el sistema ve a las mayúsculas y minúsculas como caracteres totalmente distintos.

**Ejemplos prácticos con `ls`:**

- `ls`: Lista los archivos del directorio actual.
- `ls /etc/ppp`: Usa un argumento para listar los archivos de ese directorio en específico.
- `ls /etc/ppp /etc/ssh`: Utiliza múltiples argumentos (separados por un espacio) para listar el contenido de ambos directorios al mismo tiempo.

---
### 3.4 Trabajando con las Opciones

Las opciones se usan para modificar o ampliar el comportamiento de un comando.

**De una letra:** Llevan un solo guion (ej. `-l` o `-h`).

 **De palabra completa:** Llevan dos guiones (ej. `--human-readable`).

**Combinación:** Puedes agrupar varias opciones de una sola letra bajo un mismo guion, y el orden no importa (ej. `ls -l -h` es exactamente lo mismo que `ls -lh`).

**Uso con argumentos:** Las opciones pueden convivir con los argumentos para aplicar una acción modificada a un objetivo específico (ej. `ls -l /etc/ppp`).

- Ejemplo práctico: `ls -l` lista archivos con detalles precisos (tamaño en bytes), mientras que `ls -lh` muestra los tamaños en formato legible para humanos (ej. `11K`).

---
### 4 Historial de los Comandos

El sistema guarda automáticamente un registro de todo lo que escribes en la terminal para ahorrarte tiempo y evitar que vuelvas a teclear comandos largos.

**1. Ver y navegar por el historial:**

- `history`: Muestra una lista numerada con todos tus comandos recientes.

- Teclado: Usa la Flecha Arriba (↑) para retroceder por tu historial. Una vez encuentres el comando, presiona Enter para ejecutarlo, o usa las flechas laterales para editar el texto antes de enviarlo.    

**2. Atajos rápidos (Expansión del historial):** El signo de exclamación (`!`) te permite ejecutar comandos anteriores al instante sin tener que buscarlos:

- `!numero` (ej. `!3`): Ejecuta el comando ubicado en esa posición exacta de tu lista.

- `!!`: Vuelve a ejecutar inmediatamente tu último comando (muy útil si olvidaste poner `sudo` al principio).

- `!-5`: Ejecuta el quinto comando, pero contando desde el final de la lista hacia arriba.

- `!texto` (ej. `!ls`): Ejecuta el comando más reciente que empiece con esas letras.

- `history 5`: En lugar de toda la lista, te muestra únicamente los últimos 5 comandos ejecutados.

![](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260501021742.png)

---
### 5, Introducción a las Variables del Shell BASH






---



---



