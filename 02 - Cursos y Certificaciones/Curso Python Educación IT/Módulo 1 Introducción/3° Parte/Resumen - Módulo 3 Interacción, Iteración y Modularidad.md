# 1. Entrada de datos

La entrada de datos es el mecanismo por el cual un programa recibe información del mundo exterior (generalmente del usuario a través del teclado) para procesarla. Esto hace que los programas sean interactivos y dinámicos, ya que no siempre trabajan con valores fijos predefinidos en el código.

- **Captura de datos:** En la mayoría de los lenguajes, el programa "pausa" su ejecución y queda a la espera de que el usuario ingrese un valor y presione _Enter_.

- **Conversión de Tipos (Casting):** Por defecto, casi todo lo que ingresa el usuario se lee como una cadena de texto (_String_). Si necesitas hacer cálculos matemáticos con ese ingreso, es obligatorio convertir ese texto al tipo de dato numérico adecuado (_Integer_ o _Float_) antes de procesarlo.

- **Hay otros medios de entrada de datos:** Como micrófonos, cámaras, sensores, etc.

*Ejemplos de entrada de dato por teclado por PSeINT*
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516175040.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516175126.png)

---

# 2. Estructura de Control tipo Bucle

Los bucles (o ciclos) son estructuras que te permiten repetir un bloque de código múltiples veces sin tener que escribirlo una y otra vez. Se basan en una condición lógica.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516175236.png)

### Distintos Bucles 

- **Bucle MIENTRAS (While):** Repite un bloque de código _mientras_ una condición específica sea Verdadera (True). Antes de cada nueva repetición, vuelve a evaluar la condición. Si la condición se vuelve Falsa (False), el bucle se detiene y el programa continúa.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516175358.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516175740.png)

- **Bucle PARA (For):** Se utiliza generalmente cuando sabes de antemano cuántas veces necesitas repetir el código, o cuando necesitas recorrer elemento por elemento un conjunto de datos (como una lista).

- **Bucles Infinitos:** Es un error común donde la condición de un bucle `While` nunca se vuelve Falsa, haciendo que el programa se quede atascado repitiendo el mismo código para siempre. Siempre debes asegurarte de que haya una instrucción dentro del bucle que modifique la condición de corte.


---

# 3. Conjunto de datos y operaciones

 A diferencia de una variable normal que guarda un solo valor, un conjunto de datos permite almacenar múltiples valores bajo un mismo nombre.

### Listas / Arreglos (Arrays): 

Son colecciones ordenadas de datos. Puedes guardar números, textos, booleanos e incluso otras listas dentro de ellas. Se suele hacer lista de distintas cosas pero de la misma categoria.

- **Índices:** Los elementos dentro de una lista están ordenados por posiciones llamadas índices. En la programación, **los índices siempre empiezan a contar desde el cero (0)**. Es decir, el primer elemento de tu lista está en la posición 0, el segundo en la 1, y así sucesivamente.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516032117.png)

- **Operaciones comunes:**
    - _Lectura:_ Acceder a un dato específico utilizando su índice.
    - _Escritura:_ Modificar el valor de un dato en una posición específica.
    - _Agregar/Eliminar:_ Sumar nuevos elementos al final o en el medio del conjunto, o borrar elementos existentes.
    - _Longitud:_ Obtener la cantidad total de elementos que contiene el conjunto.
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516181312.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516181413.png)


---

# 4. Concepto de funciones

Una función es un bloque de código encapsulado y con un nombre específico que realiza una tarea determinada. Sigue el principio "DRY" (_Don't Repeat Yourself_ - No te repitas): si tienes un código que usas muchas veces, lo metes en una función y simplemente la "llamas" cuando la necesites.

- **Parámetros / Argumentos:** Son los datos de entrada que la función necesita para trabajar. Funcionan como variables locales que solo existen dentro de la función. Por ejemplo, una función llamada `sumar(a, b)` necesita dos parámetros.

- **Retorno (Return):** Es el resultado que la función "devuelve" al programa principal una vez que termina su trabajo. No todas las funciones retornan algo (algunas solo imprimen un mensaje), pero cuando lo hacen, ese valor puede guardarse en una variable para seguir operando.

- **Modularidad:** Las funciones permiten dividir un problema complejo en problemas más pequeños y fáciles de resolver. Hacen que el código sea más ordenado, legible y fácil de reparar si algo falla.

*Ejemplo de funcion
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516032230.png)




- **Concepto:** Una función es un bloque de código encapsulado y con un nombre específico que realiza una tarea determinada. Sigue el principio "DRY" (_Don't Repeat Yourself_ - No te repitas): si tienes un código que usas muchas veces, lo metes en una función y simplemente la "llamas" cuando la necesites.

- **Parámetros / Argumentos:** Son los datos de entrada que la función necesita para trabajar. Funcionan como variables locales que solo existen dentro de la función. Por ejemplo, una función llamada `sumar(a, b)` necesita dos parámetros.

- **Retorno (Return):** Es el resultado que la función "devuelve" al programa principal una vez que termina su trabajo. No todas las funciones retornan algo (algunas solo imprimen un mensaje), pero cuando lo hacen, ese valor puede guardarse en una variable para seguir operando.

- **Modularidad:** Las funciones permiten dividir un problema complejo en problemas más pequeños y fáciles de resolver. Hacen que el código sea más ordenado, legible y fácil de reparar si algo falla.