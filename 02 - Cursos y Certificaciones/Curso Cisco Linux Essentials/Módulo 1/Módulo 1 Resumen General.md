# Módulo 1

## Conceptos Fundamentales

- Código Fuente (Origen): Es el conjunto de instrucciones del programa escritas de forma que sean legibles para el ser humano.
- Código Abierto: Garantiza el acceso al código fuente para verlo, modificarlo y compartirlo.
- Código Cerrado: No permite el acceso al código fuente, solo al código máquina final.
- Lenguaje base: El kernel de Linux está escrito íntegramente en el lenguaje C.
- Gestor de arranque (Bootloader): Es el código o pequeño programa encargado de cargar el kernel en la memoria al encender la computadora.
- Linux vs. UNIX: UNIX es un sistema histórico y una marca registrada. Linux funciona de manera casi idéntica, pero al no pagar la certificación oficial, se denomina sistema "tipo UNIX".
- Kernel: Es el núcleo del sistema. Administra los recursos del hardware (memoria, CPU, discos) y decide qué aplicación se ejecuta en cada momento (multitarea preferente).
- Distribución (Distro): Es el sistema operativo listo para usar (Kernel de Linux + Herramientas GNU + Aplicaciones + Gestor de paquetes).
- Código Abierto: Filosofía que garantiza a los usuarios el derecho a ver, modificar y compartir el código fuente (a diferencia del software cerrado).

## Componentes del Sistema
Aplicaciones y Procesos: Los programas piden recursos al kernel a través de una API. Para el kernel, cualquier tarea en ejecución se denomina simplemente proceso.

Comandos: Instrucciones en la terminal. Pueden ser:
- Integrados (vienen en el propio shell, como cd).
- Ejecutables (archivos guardados en el sistema que se buscan a través del PATH, como ls).
- Alias (atajos personalizados) o Funciones (rutinas agrupadas).

## Familias de Distribuciones Linux
![](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260423231123.png)
## Elegir un Sistema Operativo

La elección siempre depende de la pregunta: "¿Qué hará esta máquina?"

Escritorio vs. Servidor: El escritorio necesita interfaz gráfica (GUI) y software actualizado (ciclo corto). El servidor no usa gráficos para ahorrar recursos y prioriza la estabilidad extrema (ciclo largo, ej. versiones LTS).

Ciclos de Vida:
- Ciclo de liberación: Describe con qué frecuencia se lanza una nueva versión del software.
- Ciclo de mantenimiento: Describe por cuánto tiempo esa versión recibirá soporte y actualizaciones de seguridad.

Alternativas en el Mercado:
- Windows: Viene en variantes de escritorio y servidor. Cuenta con virtualización integrada y potentes capacidades de scripting (PowerShell), pero no tiene un modo de compatibilidad nativo con Linux (en el contexto clásico).
- Apple OS X: UNIX certificado (basado en FreeBSD, no deriva de Linux), hardware exclusivo de Apple, ideal para la industria creativa y audiovisual.
- BSD (FreeBSD, OpenBSD): Familia Open Source muy similar a Linux, usada mayormente en servidores.
- UNIX Comerciales (IBM AIX, Oracle Solaris): Son sistemas certificados por UNIX que se ejecutan en hardware exclusivo y potente; se usan cuando la empresa ya tiene infraestructura de esa marca.

## El Caso Especial de Android
Es la distribución Linux más usada del mundo, pero no usa GNU. Combina el kernel de Linux con la máquina virtual Dalvik para ejecutar apps móviles. Al carecer de las herramientas tradicionales, no es compatible con Linux de escritorio (requiere instalar una app como BusyBox para poder usar los comandos clásicos).