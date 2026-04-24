El lenguaje ensamblador es la representación legible por humanos del lenguaje de máquina (ceros y unos). Cada instrucción de ensamblador corresponde a una acción directa en el hardware del procesador.

## 1. Banderas (Flags)
Son pequeños indicadores de 1 bit que avisan sobre el resultado de la última operación de la ULA.
* **Z (Zero):** Se pone en TRUE (1) si el resultado de una operación o comparación es cero.
* **C (Carry):** Se pone en TRUE (1) si hubo un acarreo (overflow) en una suma.

## 2. Set de Instrucciones Básico
* `MOV destino, origen`: Mueve o copia un dato. Puede ser entre registros (`MOV A, B`), o usando la memoria con corchetes (`MOV [50], 0x04` mueve el valor hexadecimal 04 a la dirección 50).
* `ADD A, B`: Suma el contenido del registro B al registro A, y guarda el resultado en A.
* `MUL [51]`: Multiplica el registro A por el valor en la dirección de memoria 51.
* `CMP A, B`: Compara dos valores (internamente hace una resta). Si son iguales, activa la bandera **Z** (Zero).
* `AND A, 0x01`: Realiza una compuerta lógica AND bit a bit. Útil para saber si un número es par o impar (si el último bit es 0, es par).

## 3. Saltos (Jumps)
Modifican el Contador de Programa (PC) para romper la ejecución secuencial y crear bucles o condicionales.
* `JZ` o `JE` (Jump if Zero / Equal): Salta a una línea específica de código *solamente* si la bandera Z está en TRUE.
* `HLT` (Halt): Detiene el reloj del procesador y finaliza la ejecución.

> **Ejemplo de código (Condicional):**
```assembly
CMP A, 0x00 ; Compara el registro A con cero
JZ FIN ; Si es cero (Z=TRUE), salta a la etiqueta FIN
ADD A, B ; Si no es cero, ejecuta esta suma
FIN:
HLT ; Termina el programa
```

