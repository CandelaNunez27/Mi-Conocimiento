# Desafío 4

## Ejercicio 1

##### A. Un banco decide entregar tarjetas de crédito a los clientes que tengan una edad mayor a 35 años y un sueldo mínimo de 500 dólares. Hacer un programa que pida la edad y el sueldo de una persona, luego decida si se le entrega o no el beneficio.

*RTA = 
Algoritmo banco
edad = 0 
sueldo = 0 

*Escribir “Ingrese su edad:” 
Leer edad
Escribir “Ingrese su sueldo en dolares:”
Leer sueldo 

*Si edad > 18 y sueldo > 500 Entonces 
	Escribir “Recibe la tarjeta de credito” 
	SiNo 
	Escribir “No recibe la tarjeta” 
	Fin Si 
Fin Algoritmo*
## Ejercicio 2

##### A. En PSeInt, pedir por teclado el peso y la altura de una persona. Calcular el índice de masa corporal (imc). El índice de masa corporal se calcula: 

*Algoritmo imc_calculo
peso = 0 
altura = 0 

*Escribir “Ingrese su peso:” 
Leer peso
Escribir “Ingrese su altura:”
Leer altura

*imc = peso / (altura . altura) 
Escribir “Su imc es:”, imc 
Fin Algoritmo*

##### B. A partir del punto A, determinar si la persona está con bajo peso, peso normal o sobrepeso. 
- imc < 18 : bajo peso 
- imc >= 18 y imc < 25: peso normal 
- imc>= 25 : sobrepeso

*RTA = 
Algoritmo imc_calculo 
peso = 0 
altura = 0 

*Escribir “Ingrese su peso:” 
Leer peso
Escribir “Ingrese su altura:” 
Leer altura 

*imc = peso / (altura . altura) 
	Escribir “Su imc es:”, imc 
Si imc < 18 Entonces
	Escribir “Bajo peso”
	 SiNo
		  Si imc ≥ 18 y imc < 25 Entonces
		   Escribir “Peso normal” 
		   SiNo 
		   Escribir “Sobrepeso”
		    Fin Si 
		Fin Si 
Fin Algoritmo*
## Ejercicio 3

##### A. Pasar el diagrama de flujo de la derecha a un programa de PSeInt.
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260516190002.png)

*RTA = 
Algoritmo costos_laborales
horast = 0
costoh = 0

*Escribir “Ingrese horas trabajadas:” 
Leer horast 
Escribir “Ingrese valor hora:” 
Leer costoh 

*sueldo = horast * costoh 
Escribir “Su sueldo es:”, sueldo 
Fin Algoritmo



---

# Laboratorio 4

## Ejercicio 1

##### A. Programar
Desde PSeInt crear un programa que incremente una variable de uno en uno desde 1, hasta 10. Resolverlo con la sentencia tipo bucle. Mostrar el incremento por pantalla.

*RTA = 
Algoritmo incremento
i = 1
Mientras i<10 Hacer 
	Escribir i
	 i = i + 1
	  Fin Mientras 
Fin Algoritmo*


## Ejercicio 2

##### A. Programar
Desde PSeInt, crear un programa que dado un número máximo (ingresado por teclado), diga los múltiplos de 3 y de 5 desde 1 hasta ese máximo.

*RTA = 
Algoritmo multiplo
i = 1 
maximo = 0 
Escribir “Ingrese un numero maximo:” 
Leer maximo 
Mientras i< maximo Hacer
	Si i%3 == 0 y i%5 == 0, Entonces 
	Escribir “El”, i, “es multiplo de 3 y 5”
	 Fin Si
	  i = i + 1 
	  Fin Mientras 
Fin Algoritmo
## Ejercicio 3

##### A. Completar 
Desde PSeInt, crear un programa que, al ingresar un número, determine si es primo o no es primo. (Los números primos son aquellos que solo son divisibles entre ellos mismos y el 1)

*RTA = 
Algoritmo primos 
i = 1
num = 0
contador = 0 
Escribir “Ingrese un numero:”
Leer num 
Mientras i≤num Hacer
	Si num%i == 0 Entonces
	 contador = contador + 1 
	 Fin Si
	  i = i + 1 
	  Fin Mientras 
	Si contador == 2 Entonces 
		Escribir num, “es primo”
		 SiNo
		  Escribir num, “no es primo” 
		  Fin Si
 Fin Algoritmo

## Ejercicio 4

##### A. Programar
Desde PSeInt, crear un programa que pida un número máximo (ingresar por teclado), y después pida otro segundo número hasta que este segundo supere al primero. (Si el segundo no supera al primero, vuelva a pedir hasta que en el algún momento se cumpla con lo pedido).

*RTA = 
Algoritmo bucle_2_numeros
numero_uno = 0 
numero_dos = 0 

*Escribir “Ingrese primer numero:” 
Leer numero_uno 
Escribir “Ingrese segundo numero:” 
Leer numero_dos 

*Mientras numero_uno > numero_dos Hacer 
	Escribir “El primero sigue siendo mayor” 
	Escribir “Vuelva a ingresar el segundo valor:” 
	Leer numero_dos 
	Fin Mientras 

*Escribir numero_uno, “vs”, numero_dos 
Fin Algoritmo

## Ejercicio 5

##### A. Incrementar de uno en uno
Calcular un promedio de 5 notas. Esas notas van a ingresar por teclado, pero debemos usar un bucle para que todo se realice de forma automática. La idea sería: 
1. Crear una variable para que cuentes las vueltas (i = 1) y crear una variable para que almacene la suma (suma = 0). 
2. Mientras i <= 5, pedir las notas en orden. 
3. Dentro del bucle debemos incrementar la variable suma que almacena todas las notas (suma = suma + nota), e incrementar la variable de las vueltas(i = i + 1). 
4. Por último, dividir suma en 5 (prom = suma / 5). 
5. Mostrar el resultado por la pantalla.

*RTA = 
Algoritmo promedio_5_notas_bucle
i = 1
suma = 0

*Mientras i≤5 Hacer
	nota = 0
	 Escribir “Ingrese nota”, i, “:”
	Leer nota
	 suma = suma + nota
	  i = i + 1
	Fin Mientras
 
 *prom = suma / 5
  Escribir “El promedio es”, prom
Fin Algoritmo