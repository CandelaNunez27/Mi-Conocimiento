# Desafío 3

## Ejercicio 1

##### A. En PSeInt, pedir por teclado el nombre de una persona y mostrar un saludo acompañando el nombre.

*RTA = 
Algoritmo Ingresar_Nombre
nombre = ""
Escribir "Ingrese su nombre: "
leer nombre
escribir "Hola ", nombre
FinAlgoritmo*
## Ejercicio 2

##### A. En PSeInt, pedir por teclado la edad de una persona, y que el programa decida si la persona es menor o mayor de edad.

*RTA = 
Algoritmo Comparar_edad
edad = 0

*Escribir "Ingrese su edad: "
leer edad
Si edad < 18
	escribir "Es menor de edad"
	Sino
		escribir "Es mayor de edad"
		FinSI
FinAlgoritmo*
## Ejercicio 3

##### A. Incrementar una variable con un bucle en PSeInt.

*RTA = 
Algoritmo Incrementar_variable
x = 0

*Mientras x < 10 Hacer
	Escribir x
	x ++
	Fin Mientras
FinAlgoritmo

## Ejercicio 4

##### A. Crea un conjunto de numeros en PSeInt y mostrar alguno de los datos guardados.

*RTA = 
Inicio
edad = 
edades =[]
ingresar edad
for edad < 18
	edad ++
	edades = edad
fin


## Ejercicio 5

##### A. Crear un programa en PSeInt para recorrer un conjunto de datos.

*RTA = 
Inicio
edad = 
edades =[5]
ingresar edad
for edad < 18
	edad ++
	edades = edad
for i <=1 && i >=5
	escribir edades
	i++
fin




---

# Laboratorio 3

## Ejercicio 1

##### A. Programar
Desde PSeInt, crear un programa que pida por teclado la base y la altura de un triángulo, y nos arroje por pantalla el resultado del cálculo del área del triángulo.

*RTA = 
Algoritmo area_triangulo
area = 0.0
base = 0
altura = 0

*funcion pedir datos
Escribir "Ingrese base:"
leer base

*Escribir "Ingrese altura:"
leer altura

*funcion calcular area
area = (base * altura)  / 2
Escribir "El area del triangulo es ", area
FinAlgoritmo*


## Ejercicio 2

##### A. Programar
Desde PSeInt, crear un programa que pida el radio de un círculo y luego muestre por pantalla el resultado del perímetro.

*RTA = 
Algoritmo perímetro_circulo
radio = 0
diámetro = 0
perímetro = 0

*funcion pedir datos
Escribir "Ingrese radio:"
leer radio

*funcion calcular perimetro
diametro = radio * 2
perimetro = pi * diametro
Escribir "El perimetro el circulo es ",  perimetro
FinAlgoritmo

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
Algoritmo multiplo
num = 0 
Escribir "Es multiplo de 3 y de 5 ?"
Escribir "Ingrese el numero: " 
Leer num
Si num % 3 == 0 y num % 5 = =0 Entonces 
	Escribir "El numero ingresado es multiplo de 3 y de 5"
	 SiNo 
		 Escribir "El numero no es multiplo"
 Fin Si FinAlgoritmo

otra forma
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
1. Tengo la variable i = 1 (que arranca en 1) 
2. Mientras i < 10 (menor a diez) 
3. Dentro del bucle puedo incrementar a i de uno en uno. i = i + 1 (Podría ir mostrando dentro del bucle por pantalla el incremento)
4. código
while i < 10
	print i
	i++