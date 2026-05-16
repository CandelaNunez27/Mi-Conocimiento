# 1. Variables y Tipos de Datos

### Variables:
Son espacios reservados en la memoria de la computadora que almacenan información. Se identifican con un nombre único y su valor puede cambiar, actualizarse o reescribirse durante la ejecución del programa.
- hay lenguajes de tipado estáticos que solo aceptan variables de un solo tipo de dato
- hay lenguajes de tipado dinámico que aceptan variables de todo tipo de dato

### Tipos de Datos: 
Definen qué clase de información puede almacenar una variable y qué operaciones se pueden realizar con ella. 
Darle un valor a una variable se llama asignación *Ej: le asigno 400 a la variable dato, dato = 400*

- **Enteros (Integer):** Números exactos sin decimales (ejemplo: 10, -5).

- **Flotantes (Float):** Números con punto decimal (ejemplo: 3.14, -0.5).

- **Cadenas de texto (String):** Secuencias de caracteres, letras o palabras. En la mayoría de los lenguajes se encierran entre comillas (ejemplo: "Hola Mundo").

- **Booleanos (Boolean):** Representan valores lógicos básicos y solo pueden tener dos estados: Verdadero (True) o Falso (False).

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010043.png)


---

# 2. Operadores Aritméticos y Relacionales

### Operadores Aritméticos: 
Se utilizan para realizar cálculos matemáticos directamente en el código. Incluyen la suma (+), resta (-), multiplicación (asterisco), división (/) y el módulo o resto de una división (%).

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010219.png)


### Operadores Relacionales: 
Sirven para comparar dos valores o variables. El resultado de esta comparación siempre devuelve un valor booleano (Verdadero o Falso). El igual siempre va a la derecha.

- **Igualdad (= =):** Verifica si dos valores son exactamente iguales.

- **Desigualdad (!=):** Verifica si dos valores son diferentes.

- **Mayor que (>) y Menor que (<):** Compara qué valor es más grande en la recta numérica.

- **Mayor o igual (>=) y Menor o igual (<=):** Incluye el límite exacto dentro de la comparación.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010237.png)


---

# 3. Lógica y Operadores Booleanos

### Lógica Booleana: 
Es el sistema de toma de decisiones de una computadora, fundamentado en el álgebra de Boole.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010337.png)
### Operadores Lógicos: 
Permiten combinar múltiples condiciones relacionales para evaluar si un conjunto de reglas se cumple o no.

- **AND (Y lógico):** Devuelve Verdadero solo si **todas** las condiciones evaluadas son verdaderas. Si una sola es falsa, el resultado global es falso.

- **OR (O lógico):** Devuelve Verdadero si **al menos una** de las condiciones es verdadera. Solo devuelve falso cuando absolutamente todas las condiciones son falsas.

- **NOT (Negación):** Invierte el valor lógico de una condición. Si el resultado era Verdadero, lo convierte en Falso, y viceversa.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010356.png)


---

# 4. Estructuras de Control y Condicionales

- **Estructuras de Control:** Son bloques de código que alteran el flujo normal y secuencial de un programa. Permiten que la computadora decida qué camino tomar dependiendo de los datos que reciba.

- **Condicionales:** Es la implementación práctica de la toma de decisiones. El código solo se ejecuta si se aprueba una evaluación lógica.

- **IF (Si):** Evalúa una condición principal. Si el resultado es Verdadero, ejecuta el bloque de código interno.


![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010437.png)


- **ELSE (Sino):** Se utiliza siempre como complemento de un IF. Si la condición del IF fue Falsa, el programa ejecutará automáticamente el código que esté dentro del ELSE.


![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010450.png)


- **ELSE IF / ELIF (Sino si):** Permite evaluar múltiples condiciones en cadena si la primera (IF) no se cumplió. Si la condición del ELIF es verdadera, se ejecuta su código y se ignoran las demás.

*Ejemplo de tomar un café*
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516010509.png)

