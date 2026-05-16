# Desafío 3

## Ejercicio 1

##### A. En PSeInt, pedir por teclado el nombre de una persona y mostrar un saludo acompañando el nombre.

*RTA = 
Inicio
nombre = 
ingresar nombre
escribir "Hola" nombre
fin*
## Ejercicio 2

##### A. En PSeInt, pedir por teclado la edad de una persona, y que el programa decida si la persona es menor o mayor de edad.

*RTA = 
Inicio
edad = 
ingresar edad
si edad < 18
	escribir "Es menor de edad"
	sino
		escribir "Es mayor de edad"
fin*
## Ejercicio 3

##### A. Incrementar una variable con un bucle en PSeInt.

*RTA = 
Inicio
edad = 
ingresar edad
for edad < 18
	edad ++
fin

## Ejercicio 4

##### A. Crea un conjunto de numeros en PSeInt y mostrar alguno de los datos guardados.

*RTA = 
Inicio
edad = 
ingresar edad
for edad < 18
	edad ++
fin


## Ejercicio 5

##### A. Complete la tabla con los resultados.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516012342.png)

| p   | q   | p o q |
| --- | --- | ----- |
| V   | V   | *V*   |
| V   | F   | *V*   |
| F   | V   | *V*   |
| F   | F   | *F*   |


---

# Laboratorio 3

## Ejercicio 1

##### A. Programar
Desde PSeInt, crear un programa que pida por teclado la base y la altura de un triángulo, y nos arroje por pantalla el resultado del cálculo del área del triángulo.

*RTA = 
inicio
area = 0.0
base = 0
altura = 0
funcion pedir datos
ingresar base
ingresar altura
funcion calcular area
area = (base * altura)  / 2
escribir area
fin


## Ejercicio 2

##### A. Programar
Desde PSeInt, crear un programa que pida el radio de un círculo y luego muestre por pantalla el resultado del perímetro.

*RTA = 
inicio
radio = 0
diametro = 0
perimetro = 0
funcion pedir datos
ingresar radio
funcion calcular perimetro
diametro = radio * 2
perimetro = pi * diametro
escribir perometro
fin

## Ejercicio 3

##### A. Completar 
En todos los lenguajes de programación existe el operador " % " (permite saber si una división tiene resto nulo o no). En el módulo anterior vimos este operador. Estos ejemplos te serán de referencia: 10 % 2 == 0 , el resto es 0. Otro ejemplo, 8 % 3 == 2, el resto es 2

Entonces complete los siguientes casos: 
a) 11 % 2 == *1*
b) 9 % 3 == *0*
c) 7 % 2 == *1*
d) 100 % 5 == *0*

## Ejercicio 4

##### A. Programar
Desde PSeInt, pida un número entero por teclado. Luego, determine si ese número ingresado es múltiplo de 3 y de 5. Avisar al usuario que el número ingresado es múltiplo o no.

*RTA = 



``` python
# Creamos una lista vacía para guardar los múltiplos 
multiplos = [] 

# Vamos desde 1 hasta 50 (en Python, el límite superior no se incluye, así que frena en 49)
for numero in range(1, 50): 
	if numero % 3 == 0 or numero % 5 == 0: 
	multiplos.append(numero) 

# Mostramos el resultado en la pantalla
print("Los múltiplos de 3 y 5 menores a 50 son:")
print(multiplos)
````


## Ejercicio 5

##### A. Incrementar de uno en uno
Escriba (en papel, con sus palabras, pseudocódigo) un algoritmo que incremente una variable que arranca en 1 y aumente de uno en uno hasta 10.

*RTA = 
