La unidad de memoria central almacena datos, instrucciones y resultados. Se comunica con la UCP mediante tres buses principales.

## 1. Los Buses de Memoria
* **Bus de Direcciones (AB):** Unidireccional. La UCP coloca aquí el código binario de la celda a la que quiere acceder. El número de líneas determina el máximo de direcciones direccionables ($2^n$).
* **Bus de Datos (DB):** Bidireccional. Transporta la información leída o a escribir. Su ancho define el tamaño de la "palabra" de memoria.
* **Bus de Control:** Envía señales de sincronismo:
    * **CS (Chip Select):** Activa el chip de memoria.
    * **R/W (Read/Write):** Indica si se va a realizar una lectura (1) o una escritura (0).

## 2. Ciclos de Operación
* **Lectura:** Dirección en AB → CS activo → R/W en 1 → El dato aparece en el DB.
* **Escritura:** Dirección en AB → Dato en DB → CS activo → R/W en 0 → El dato se guarda.

## 3. Decodificador de Direcciones
Es el circuito interno que interpreta el Bus de Direcciones para habilitar una única posición de memoria entre miles de opciones posibles.