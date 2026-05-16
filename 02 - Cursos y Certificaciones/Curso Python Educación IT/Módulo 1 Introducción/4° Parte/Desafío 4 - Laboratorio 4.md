# Desafío 4

## Ejercicio 1

##### A. Un banco decide entregar tarjetas de crédito a los clientes que tengan una edad mayor a 35 años y un sueldo mínimo de 500 dólares. Hacer un programa que pida la edad y el sueldo de una persona, luego decida si se le entrega o no el beneficio.

*RTA = 
Algoritmo Ingresar_Nombre
nombre = ""
Escribir "Ingrese su nombre: "
leer nombre
escribir "Hola ", nombre
FinAlgoritmo*
## Ejercicio 2

##### A. En PSeInt, pedir por teclado el peso y la altura de una persona. Calcular el índice de masa corporal (imc). El índice de masa corporal se calcula: 

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

##### B. A partir del punto A, determinar si la persona está con bajo peso, peso normal o sobrepeso. 
- imc < 18 : bajo peso 
- imc >= 18 y imc < 25: peso normal 
- imc>= 25 : sobrepeso

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

##### A. Pasar el diagrama de flujo de la derecha a un programa de PSeInt.
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516190002.png)

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
Algoritmo ejemplo_conjuntos
Dimension datos (5)
datos[1] = 50
datos[2] = 100
datos[3] = 150 
datos[4] = 200
datos[5] = 250
Escribir datos [1]
FinAlgoritmo


## Ejercicio 5

##### A. Crear un programa en PSeInt para recorrer un conjunto de datos.

*RTA = 
Algoritmo ejemplo_conjuntos
Dimension datos (5)
datos[1] = 50
datos[2] = 100
datos[3] = 150 
datos[4] = 200
datos[5] = 250
Indice = 1
Mientras indice ≤ 5 Hacer 
	Escribir datos[indice] 
	indice = indice + 1 
	Fin Mientras 
FinAlgoritmo






---

# Laboratorio 4

## Ejercicio 1

##### A. Programar
Desde PSeInt crear un programa que incremente una variable de uno en uno desde 1, hasta 10. Resolverlo con la sentencia tipo bucle. Mostrar el incremento por pantalla.

*RTA = 
Algoritmo area_triangulo
area = 0.0
base = 0
altura = 0

*Escribir "Ingrese base:"
leer base
Escribir "Ingrese altura:"
leer altura

*area = (base * altura)  / 2
Escribir "El area del triangulo es ", area
FinAlgoritmo*


## Ejercicio 2

##### A. Programar
Desde PSeInt, crear un programa que dado un número máximo (ingresado por teclado), diga los múltiplos de 3 y de 5 desde 1 hasta ese máximo.

*RTA = 
Algoritmo perímetro_circulo
radio = 0
diámetro = 0
perímetro = 0

*Escribir "Ingrese radio:"
leer radio

*diametro = radio * 2
perimetro = pi * diametro
Escribir "El perimetro el circulo es ",  perimetro
FinAlgoritmo

## Ejercicio 3

##### A. Completar 
Desde PSeInt, crear un programa que, al ingresar un número, determine si es primo o no es primo. (Los números primos son aquellos que solo son divisibles entre ellos mismos y el 1)

Entonces complete los siguientes casos: 
a) 11 % 2 == *1*
b) 9 % 3 == *0*
c) 7 % 2 == *1*
d) 100 % 5 == *0*

## Ejercicio 4

##### A. Programar
Desde PSeInt, crear un programa que pida un número máximo (ingresar por teclado), y después pida otro segundo número hasta que este segundo supere al primero. (Si el segundo no supera al primero, vuelva a pedir hasta que en el algún momento se cumpla con lo pedido).

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
Calcular un promedio de 5 notas. Esas notas van a ingresar por teclado, pero debemos usar un bucle para que todo se realice de forma automática. La idea sería: 
1. Crear una variable para que cuentes las vueltas (i = 1) y crear una variable para que almacene la suma (suma = 0). 
2. Mientras i <= 5, pedir las notas en orden. 
3. Dentro del bucle debemos incrementar la variable suma que almacena todas las notas (suma = suma + nota), e incrementar la variable de las vueltas(i = i + 1). 
4. Por último, dividir suma en 5 (prom = suma / 5). 
5. Mostrar el resultado por la pantalla.

*RTA = 
1. Tengo la variable i = 1 (que arranca en 1) 
2. Mientras i < 10 (menor a diez) 
3. Dentro del bucle puedo incrementar a i de uno en uno. i = i + 1 (Podría ir mostrando dentro del bucle por pantalla el incremento)
4. código
while i < 10
	print i
	i++