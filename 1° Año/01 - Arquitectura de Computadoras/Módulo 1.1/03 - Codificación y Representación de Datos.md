Como el lenguaje natural o decimal es ineficiente o imposible de leer directamente por los circuitos, se utilizan códigos binarios para representar caracteres y números.

## 1. Códigos Numéricos
* **BCD (Binary Coded Decimal):** Cada dígito decimal se reemplaza por una combinación de 4 bits. 
    * *BCD Natural (8421):* Usa los mismos pesos que el binario puro.
    * *BCD Aiken (2421) y Exceso 3:* Son útiles porque son "autocomplementarios", facilitando cálculos.
* **Códigos Continuos/Cíclicos:** Como el **Código Gray** (binario reflejado) o el código **Johnson**. Su característica principal es que codificaciones adyacentes se diferencian en un solo bit (ideal para evitar errores de lectura mecánica o electrónica).

## 2. Complementos (Para números negativos)
En lugar de restar en binario, las computadoras suman el "complemento".
* **Complemento a 1:** Se calcula rápidamente cambiando todos los ceros por unos y los unos por ceros.
* **Complemento a 2:** Se resta el dígito menos significativo de 2 y el resto de 1 (matemáticamente, equivale a calcular el complemento a 1 y sumarle 1)

## 3. Detección de Errores (Bit de Paridad)
Se usa en telecomunicaciones añadiendo un bit extra a la transmisión para detectar alteraciones.
* **Paridad Par:** El bit añadido hace que la cantidad total de unos en la trama sea un número par.
* **Paridad Impar:** El bit añadido hace que la cantidad total de unos sea un número impar.
* *Limitación:* Falla si los errores cambian un número par de bits a la vez, ya que la paridad final no se ve afectada.

## 4. Códigos Alfanuméricos
Representan letras, números, signos de puntuación y comandos de control.
* **ASCII:** (American Standard Code for Information Interchange). Es el estándar más utilizado. Suele usar paquetes de 8 bits (Bytes) para representar cada carácter. Ejemplo: La letra "A" mayúscula es el valor hexadecimal `41` (o 65 en decimal).