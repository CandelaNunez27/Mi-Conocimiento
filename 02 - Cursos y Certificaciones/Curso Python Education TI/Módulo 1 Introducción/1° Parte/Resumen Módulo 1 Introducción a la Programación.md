

# 1. Glosario y Conceptos Clave de Programación

* **Variable:** Es un nombre utilizado en informática para representar un valor o dato.
* **Conjuntos de datos:** Son colecciones o agrupaciones de variables.
* **Bucle:** Secuencia de instrucciones en el código que se repite mientras se cumpla una condición.
* **Función:** Subrutina que describe una secuencia de órdenes para cumplir una tarea específica.
* **Operadores Aritméticos:** Realizan operaciones matemáticas como la suma, resta, multiplicación, división y división modular.
* **Operadores Lógicos:** Sirven para evaluar expresiones mediante operadores relacionales y determinar si son verdaderas o falsas.
* **Python:** Es un lenguaje de programación interpretado, multiplataforma, multiparadigma, de tipado dinámico y de propósito general.

---
# 2. Informática y Evolución de las Computadoras

La **informática** es la disciplina que abarca los métodos y técnicas para el tratamiento automático de la información. Su objetivo es almacenar, procesar y transmitir datos en formato digital mediante sistemas computacionales, utilizando tanto medios físicos (hardware) como lógicos (software).

### Generaciones de Computadoras:

- **Pre - Generaciones:** Se decía que todo comenzó con la maquina anticitera (200 A.C)que padecía los movimientos de los astros en los cielos.  Luego la primera calculadora llamada la Pascalina (1623 - 1662). La maquina Diferencial era una calculadora, pero para funciones polinómicas. Y por ultimo, la Z1, que era una gran calculadora electromecánica que dio inicio a las generaciones

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515232241.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515232423.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515232658.png)
 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231526.png)

* **1ra Generación (1946-1955):** Utilizaban tubos de vacío o válvulas electrónicas. Eran máquinas de gran tamaño, no tenían sistema operativo y funcionaban mediante tarjetas perforadas,  para cálculos físicos y el ejercito (ej. ENIAC). 

 ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231612.png) 

* **2da Generación (1958-1964):** Las válvulas fueron sustituidas por transistores y memorias magnéticas. En esta etapa se comenzaron a utilizar lenguajes de alto nivel como ALGOL, FORTRAN y COBOL.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231638.png)

* **3ra Generación (1964-1971):** Se caracterizó por la invención del circuito integrado (chip, conjunto de transistores) y el almacenamiento magnetico. Esto permitió integrar los componentes en una sola pieza, logrando equipos más rápidos, confiables, de menor tamaño y con menor consumo de energía.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231655.png)

* **4ta Generación (1971-1981):** Marcada por la aparición del microprocesador. Surgen los primeros prototipos de computadoras personales de marcas como Apple e IBM, junto con el primer disquete.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231720.png)

* **5ta Generación (1981-1989):** Enfocada en desarrollar ordenadores con tecnología más avanzada para el disquete y lenguajes de programación más potentes. IBM estableció el estándar de compatibilidad para la "computadora de escritorio".

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231737.png)

* **6ta Generación (1990-Actualidad):** Destaca por una mayor potencia de cómputo, arquitectura paralela, y grandes cambios en las formas de almacenamiento.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231755.png)

* **7ma Generación (Proyección):** Se espera que el próximo gran salto esté marcado por el desarrollo de la informática cuántica.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515231814.png)

---

# 3. Sistemas Numéricos

Son conjuntos ordenados de símbolos y reglas utilizados para representar cantidades numéricas, y cada sistema se identifica por su base (cantidad de símbolos diferentes que emplea). Son sistemas posicionales, ya que un símbolo cambia de valor según su posición.

* **Sistema Decimal:** Es de base 10 y utiliza los dígitos del 0 al 9.

* **Sistema Binario:** Es de base 2 y emplea solo los símbolos 0 y 1. Es fundamental en la informática para representar el voltaje del hardware (0 = apagado, 1 = encendido).

* **Sistema Hexadecimal:** Es de base 16 y utiliza los números del 0 al 9, seguidos de las letras A, B, C, D, E y F (las cuales representan los valores del 10 al 15 respectivamente).

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515233555.png)

### Conversiones

* *Decimal a Binario / Hexadecimal:* Se realizan divisiones sucesivas (por 2 o por 16, según corresponda) y se escriben los restos obtenidos en orden inverso.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515233703.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515233811.png)

* *Binario a Decimal:* Se multiplica cada dígito por la potencia de 2 correspondiente a su posición (empezando de derecha a izquierda con el exponente 0) y se suman todos los valores.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515233836.png)

* *Hexadecimal a Decimal a Binario:* Podemos establecer una equivalencia directa entre cada digito hezxadecimal, decimal y cuatro dígitos binarios.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515234114.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515234146.png)


---

# 4. Hardware, Software y Sistemas Operativos

### Hardware:
Son los componentes físicos y tangibles de la computadora. Se clasifica según su función:


* **Entrada (Inputs):** Dispositivos para introducir datos, como el teclado, mouse, micrófono, escáner y webcam.

* **Proceso:** El Microprocesador o Unidad Central de Procesos (CPU) es el encargado de procesar y ejecutar las instrucciones codificadas en números binarios.

* **Almacenamiento (Memorias):** La memoria RAM guarda datos para un procesamiento rápido, pero es volátil y se borra al apagar el equipo. Los dispositivos de almacenamiento masivo (discos rígidos, USB, SD) son más lentos pero conservan la información permanentemente.

* **Salida (Outputs):** Dispositivos que muestran los resultados del procesamiento, como monitores, parlantes e impresoras.

### Software:
Es el código escrito por programadores que contiene las instrucciones para manejar el hardware. Incluye elementos intangibles como aplicaciones y sistemas operativos.


* **Sistema Operativo (OS):** Es el software base que controla el funcionamiento de todos los componentes físicos y administra los programas. Ejemplos principales:

	* *Microsoft Windows:* El más utilizado en computadoras personales, basado en interfaz gráfica.
	* *MAC OS:* Sistema de Apple basado en el núcleo de UNIX.
	* *Linux:* Familia de sistemas operativos de dominio público y gratuito.


---

# 5. Algoritmos, Diagramas de Flujo y Pseudocódigo

### Algoritmo:
Es un método lógico resolutivo, escrito paso a paso, diseñado para resolver problemas. Actúa como el núcleo de un programa y abarca cálculos y procesamiento de datos.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515234712.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515234801.png)

### Diagrama de Flujo: 
Es la representación gráfica de un algoritmo mediante símbolos estandarizados.
* *Inicio/Final:* Representa los extremos del proceso.
* *Línea de Flujo (flecha):* Indica el orden de ejecución.
* *Entrada/Salida (paralelogramo):* Lectura e impresión de datos.
* *Proceso (rectángulo):* Operaciones.
* *Decisión (rombo):* Analiza situaciones en base a verdadero/falso.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515234555.png) ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515234627.png)

### Pseudocódigo:
Es un boceto escrito de la idea. Se redacta de la forma más cercana al lenguaje humano (en español) para facilitar su entendimiento antes de traducirlo a un lenguaje de programación.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260515234731.png)

---

