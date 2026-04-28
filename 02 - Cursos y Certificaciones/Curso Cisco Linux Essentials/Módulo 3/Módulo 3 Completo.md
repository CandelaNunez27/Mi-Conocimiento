# Módulo 3

## 1 Introducción
Para ser un buen administrador de sistemas, primero debes usar Linux como tu escritorio diario y dominar las TIC básicas. Usarlo a diario acelera tu aprendizaje y te ayuda a empatizar con los usuarios. El trabajo no es solo configurar servidores; también incluye muchas tareas de oficina, como enviar correos y redactar documentación. El rol de "Administrador de Sistemas" es la posición más buscada por los reclutadores en el área de TI

---
## 2 Modo Gráfico vs. No Gráfico

**Modo Gráfico (Escritorio):**

 Entorno visual con ventanas que se pueden mover y redimensionar, menús e íconos. Es el entorno clásico para el usuario final (donde usas navegadores web, LibreOffice, clientes de correo visuales, etc.). Permite iniciar sesión visualmente y abrir múltiples ventanas de terminal (shells) al mismo tiempo, lo cual es muy útil para administrar varios equipos remotos.

**Modo No Gráfico (Consola / Texto):**

Interfaz basada puramente en texto. Tras ingresar tu usuario y contraseña, entras directamente al shell. No existen ventanas para navegar con el ratón. Aunque sigue habiendo editores de texto, navegadores y clientes de correo, todo funciona exclusivamente mediante texto. 
La mayoría de los servidores se ejecutan en este modo porque cargar una interfaz gráfica consumiría recursos innecesariamente (ya que casi nadie interactúa físicamente frente al servidor).

![406](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260428024408.png)

**Elementos en pantalla:**
- MOTD (Message of the Day / Mensaje del día):** Texto que puede aparecer justo después de iniciar sesión para dar información importante configurada por el administrador.

- Desplazamiento: A medida que ingresas comandos (como el comando `w` para ver quién está conectado), el texto viejo se desplaza hacia arriba. Es responsabilidad del programa de terminal recordar el historial para que puedas subir y leer comandos anteriores.

---
### 3.3 Línea de Comandos

- **¿Qué es?:** Es una interfaz de entrada de texto que te permite darle instrucciones al sistema operativo, abarcando desde un comando simple de una sola palabra hasta _scripts_ (secuencias de programación) muy complejos.

- **Cómo acceder a ella:**
    
    - **En Modo Texto:** Al iniciar sesión, te encuentras inmediatamente dentro de la consola.
    
    - **En Modo Gráfico:** Debes iniciar un **shell gráfico**, que es básicamente la misma consola de texto tradicional pero dentro de una ventana que puedes mover, maximizar o redimensionar. * **¿Cómo encontrarla en el escritorio gráfico?**
    
    - Los escritorios en Linux varían, pero generalmente debes buscar en tus menús una aplicación llamada **terminal** o **x-term** (ambas cumplen la misma función, solo varían en su aspecto estético).
    
    - _Tip de eficiencia:_ En lugar de perderte buscando en los menús, la forma más rápida es usar la herramienta de búsqueda de tu entorno (como el _Dash_ en Ubuntu) y simplemente escribir la palabra "terminal" para ejecutarla al instante.

---

### 2.2 Aplicaciones de Escritorio

Aunque los servidores son el fuerte de Linux, también cuenta con un riquísimo ecosistema de aplicaciones para el usuario final (escritorio).

**La Interfaz Gráfica (Cómo funciona lo visual)**

- X Window (X11 / X.org): Es el servidor gráfico base. Permite que el software opere en modo visual y acepta las entradas del teclado y el ratón.

- Administrador de Ventanas: Es el nivel básico. Se encarga de dibujar los menús y gestionar las ventanas en la pantalla (Ejemplos: Compiz, FVWM, Enlightenment).

- Entorno de Escritorio: Es el nivel completo. Incluye su propio administrador de ventanas, pero le suma pantallas de inicio, administrador de archivos y muchísimas utilidades integradas. Los dos gigantes indiscutibles son KDE y GNOME.


**Ofimática (Productividad)**

La alternativa libre a Microsoft Office.

- *LibreOffice y OpenOffice*: Ambas ofrecen procesador de textos, hojas de cálculo, presentaciones y buscan compatibilidad total con los formatos de Microsoft.

- Historia y política del Open Source: Originalmente, Sun Microsystems liberó OpenOffice. Cuando Oracle compró Sun, la comunidad desconfió del soporte que Oracle le daría al proyecto. Como resultado, el proyecto se "bifurcó" (se dividió) creando LibreOffice. Hoy en día, LibreOffice tiene el mayor impulso y viene por defecto en la mayoría de las distribuciones.

**Navegadores Web y Correo Electrónico**

- Navegadores: Firefox y Google Chrome dominan el mercado de código abierto. Su sana competencia obliga a ambos equipos a innovar constantemente, lo que beneficia a todos los usuarios de internet.

- Clientes de Correo (Escritorio):  Thunderbird (de los creadores de Firefox/Mozilla).
    
    - **Evolution** (del entorno GNOME).
    
    - **KMail** (del entorno KDE).
    
    - _Ventaja:_ Al usar protocolos estándar (POP, IMAP, SMTP), puedes cambiar de un cliente a otro sin perder tus correos.


**Herramientas Creativas y Multimedia**

- Blender: Modelado, animación y creación de películas en 3D (utilizado incluso en producciones de Hollywood).

- GIMP: Manipulación y edición de imágenes en 2D (la gran alternativa a Photoshop).

- *Audacity: Grabación y edición de audio.*

---

### 2.3 Herramientas de Consola

La administración del sistema y la automatización de tareas en Linux se realizan a través de la línea de comandos utilizando un shell.

**El Shell y el Prompt**
El shell es la interfaz que recibe tus comandos y se los pasa al kernel para que los ejecute. Al abrir la terminal, ves el prompt (la línea que espera tus órdenes), que tiene una estructura típica como esta: `usuario@servidor:~$`

* `~` (Tilde o virgulilla): Es el atajo para referirse a tu directorio personal (home).
* `$` (Signo de dólar): Indica que estás usando una cuenta estándar (sin privilegios de administrador/root).

**Tipos de Shell**
Existen diferentes shells para elegir, variando en su sintaxis y capacidades para hacer scripts (programación de tareas):
* Familia Bourne: Su versión moderna es Bash (Bourne Again Shell). Es el shell predeterminado en la inmensa mayoría de los sistemas Linux.
* Familia C shell: Usa una sintaxis prestada del lenguaje C. Su versión moderna es tcsh.
* Otros populares: Korn shell (ksh) y zsh.

**Editores de Texto en Consola**
Son vitales para editar archivos de configuración directamente desde la terminal, sin interfaz gráfica.
* Avanzados y complejos: `vi` (y su versión mejorada `vim`) y `emacs`. Son extremadamente potentes pero tienen una curva de aprendizaje alta.
* Básicos y sencillos: `nano` y `pico`. Ideales para ediciones rápidas y simples.
* La regla de oro de Linux: Aunque uses `nano` o `emacs` a diario, debes aprender el uso básico de `vi`. Es el único editor que viene preinstalado por obligación en todos los sistemas Linux, lo cual es vital si entras a un modo de recuperación para reparar un sistema dañado.

**Administradores de Paquetes**
Atrás quedaron los días de compilar software manualmente. *Hoy se usan paquetes (aplicaciones empaquetadas y listas) que se descargan de servidores en internet llamados repositorios.*
* En sistemas Debian (ej. Ubuntu, Mint): Se usan los comandos `dpkg`, `apt-get` y `apt-cache`.
* En sistemas Red Hat (ej. CentOS, Fedora): Se usan los comandos `rpm` y `yum`.

---

### 2.4 Herramientas de Desarrollo

Linux es una plataforma de primer nivel para programadores, ofreciendo un excelente soporte para múltiples lenguajes. Los lenguajes de programación se dividen en dos grandes grupos:

**Lenguajes Compilados** 

Se traducen completamente a código de máquina antes de que el programa se ejecute. Son más rápidos y eficientes.

- *C*: Es el lenguaje en el que está escrito Linux. Es sumamente eficiente, requiere pocos recursos y es ideal para sistemas operativos porque se ejecuta rapidísimo. (A partir de él nacieron C++ y Objective C).

**El caso especial de Java (Compilación Intermedia):**

- Java: No compila directamente al lenguaje del equipo, sino a un código intermedio (bytecode) pensado para una CPU hipotética llamada Máquina Virtual de Java (JVM).

- La gran ventaja: Puedes ejecutar un programa de Java en cualquier dispositivo del mundo (PC, servidor, TV) siempre y cuando tenga la JVM instalada. Además, la JVM se encarga de tareas complejas como asignar la memoria automáticamente.


**Lenguajes Interpretados** 

Se traducen a código de máquina línea por línea mientras el programa se está ejecutando. Consumen más recursos del equipo, pero aumentan enormemente la productividad del programador (escriben menos código y no pierden tiempo compilando).

- Perl: Nacido para manipular texto, es el clásico favorito de los administradores de sistemas para automatizar tareas.

- PHP: Diseñado para crear páginas web dinámicas (trabaja en conjunto con servidores como Apache). Es muy fácil de aprender y es la base de proyectos gigantes como WordPress.

- Ruby: Facilita la programación compleja. Muy famoso por su entorno web Ruby on Rails y por ser la base de herramientas modernas para gestionar servidores de Linux (como Chef y Puppet).

- Python: Su sintaxis facilita tareas difíciles. Es el gran favorito en el mundo académico por sus potentes capacidades de procesamiento estadístico y de datos. Su entorno web más famoso es Django.


**Librerías (Bibliotecas)**

Son paquetes de código preescrito que resuelven tareas comunes, para que el programador no tenga que "reinventar la rueda".

- ImageMagick: Librería para manipular imágenes directamente desde el código o la consola.

- OpenSSL: Librería criptográfica estándar para añadir seguridad a programas y servidores web.

- Librería de C (Nivel bajo): Proporciona las funciones más básicas del sistema (como leer y escribir archivos en el disco) y es utilizada "por debajo" por casi todos los demás lenguajes y aplicaciones.

---

### 2.3 Entendiendo el Software de Código Abierto y el Licenciamiento

Al hablar de adquirir software, existen tres componentes fundamentales a tener en cuenta:

1. Propiedad (Intelectual): ¿Quién es el dueño original de la idea o el código?

2. Dinero: ¿Cómo es el modelo de negocio o la transacción financiera?

3. Licencia: ¿Qué derechos adquieres tú? ¿Puedes usarlo en varias PCs, modificarlo o regalarlo?

La regla general es que el creador siempre retiene la propiedad intelectual; lo que te otorgan es una licencia de uso. Precisamente, es la licencia el factor clave que distingue al código cerrado del código abierto.

***Comparativa de Modelos:**

- Modelo de Código Cerrado (Ej. Microsoft Windows):
    
    - Licencia: Utiliza un CLUF / EULA (Contrato de Licencia de Usuario Final).
    
    - Restricciones: Microsoft entrega solo el código binario (ejecutable). Se restringe a una instalación por equipo, prohíbe realizar ingeniería inversa para ver el código fuente original y cobra por las versiones mayores.

- Modelo de Código Abierto (Ej. Linux):
    
    - *Licencia: Linus Torvalds utiliza la GPLv2 (GNU Public License versión 2).*
    
    - Libertades y Reglas: El código fuente debe estar siempre disponible. Puedes modificarlo como quieras. Sin embargo, tiene una condición (copyleft): si distribuyes tus cambios, debes hacerlo bajo esta misma licencia para que la comunidad siga beneficiándose. Además, no puedes cobrar por el código fuente en sí, solo por los gastos de distribución física si los hubiera.


**FOSS (Software Libre y de Código Abierto)**

FOSS (Free and Open Source Software) agrupa a todo este tipo de software donde el creador original "libera" su derecho a restringir quién o cómo se usa el programa, garantizando el acceso y la redistribución del código fuente.

Diversidad de Licencias: Dado que el licenciamiento tiene un fuerte componente político y filosófico, muchas organizaciones han creado sus propias licencias de código abierto que se adaptan a sus intereses (ej. la licencia MIT, la de la Universidad de California, la de la Fundación Apache o las de la Free Software Foundation).

---

### 3.1 La Free Software Foundation y el Open Source Initiative

Existen dos grandes organizaciones que lideran el mundo del código abierto, cada una con su propia filosofía:

| **Característica**       | **Free Software Foundation (FSF)**                                                                                    | **Open Source Initiative (OSI)**                                                                                          |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Fundadores**           | *Richard Stallman (1985).*                                                                                            | Bruce Perens y Eric Raymond (1998).                                                                                       |
| **Enfoque**              | "Software Libre": Se enfoca en la ética y la libertad. Consideran que el software cerrado/propietario es perjudicial. | "Código Abierto": Nació porque sentían que la FSF era muy extrema/política. Tienen un enfoque más práctico y empresarial. |
| **Regla de Oro**         | Copyleft: Si modificas un software libre, estás obligado a compartir tus cambios bajo la misma licencia.              | Permisivo: Cero restricciones. Puedes usar el código abierto y modificarlo, sin estar obligado a compartir tus cambios.   |
| **Gestión de Licencias** | Crea sus propias licencias (Familia GPL).                                                                             | No crea licencias; evalúa y certifica licencias de terceros que cumplen sus principios.                                   |
**Detalles Clave de la FSF (Free Software Foundation)**

- Licencias GPL y LGPL: Crearon la GPL (la de Linux) y la LGPL (Lesser GPL). *La diferencia es que la LGPL permite que el software libre se enlace o trabaje junto a software cerrado (como un controlador de hardware propietario).*

- Activismo: Luchan contra las patentes de software y el DRM (Administración de Derechos Digitales) porque restringen la libertad del usuario.

- "Tivoización": La empresa TiVo usó Linux en sus grabadoras. Cumplió con entregar el código fuente, pero diseñó su hardware para que rechazara cualquier código modificado por el usuario.
    
    - *La FSF consideró esto una trampa y creó la **GPLv3** para prohibirlo.*
    
    - Linus Torvalds estuvo en desacuerdo con la FSF en este punto, por lo que el kernel de Linux se quedó en la versión **GPLv2**.


**Detalles Clave de la OSI (Open Source Initiative)**

- Licencias Permisivas (BSD y MIT): La OSI certifica licencias muy simples cuyo único gran requisito es: _"Haz lo que quieras, pero no digas que lo escribiste tú (respeta el derecho de autor original)"_.

- *A diferencia del Copyleft de la FSF, con una licencia permisiva (como BSD) puedes tomar código abierto, modificarlo y venderlo como un producto de código cerrado. Por esta razón, la FSF no aprueba este tipo de licencias.*

---

### 3.2 Más Términos para lo Mismo (FOSS y FLOSS)

Para evitar debates constantes entre las posturas de la FSF y la OSI, la comunidad empezó a utilizar siglas que agrupan a ambos mundos:

- FOSS (Software Libre y de Código Abierto): Agrupa tanto los principios de Free Software como de Open Source.

- El problema de la traducción: En inglés, la palabra "free" es ambigua. Puede significar gratuito ("gratis como una cerveza") o libre ("libre como la libertad de expresión").

- FLOSS: Para solucionar esta ambigüedad del inglés, se incluyó la palabra "Libre" (del español/francés), creando las siglas FLOSS (Free / Libre / Open Source Software).

Conclusión práctica: Aunque estos términos "paraguas" ocultan las profundas diferencias filosóficas entre la FSF y la OSI, a nivel práctico significan una cosa muy clara para el usuario: *si un software es FOSS/FLOSS, sabes que no tienes que pagar por él y que tienes el derecho de redistribuirlo.*

---

### 3.3 Otros Esquemas de Concesión de Licencias

Las licencias de software (FOSS) no están pensadas para obras creativas como dibujos, textos o planos. Para este tipo de contenido se usan otros esquemas:

- Dominio Público (CC0 o *No Rights Reserved*): El autor renuncia a todos los derechos sobre su obra. Cualquiera puede usarla sin restricciones.

- Licencias Creative Commons (CC): Permiten al autor elegir exactamente qué permisos otorga sobre su obra, combinando estas 4 reglas básicas:
    
    - BY (Atribución): Uso libre, pero es obligatorio dar crédito al autor.
    
    - SA (Compartir Igual / ShareAlike): Las obras derivadas deben usar esta misma licencia (funciona como el copyleft).
    
    - ND (Sin Derivadas / No-Derivs): Se puede compartir la obra, pero está prohibido modificarla.
    
    - NC (No Comercial): Prohíbe utilizar la obra para ganar dinero.

(Estas reglas se combinan para crear la licencia deseada. Por ejemplo, **CC-BY-NC** te obliga a dar crédito y te prohíbe el uso comercial)

---

### 3.4 Los Modelos de Negocio de Código Abierto

Si el software de código abierto se distribuye gratuitamente ¿Cómo es posible generar ingresos?

- Soporte y Consultoría: El modelo más común. Entregas el software gratis, pero cobras por instalarlo, brindar soporte técnico, ofrecer garantías o solucionar errores específicos a medida.

- Suscripciones y Servicios Adicionales: Se ofrece el programa gratuitamente, pero se cobra por conectarlo a un servicio exclusivo que mejora su funcionamiento (ej. el software _MythTV_ es gratis, pero se paga una suscripción para recibir la guía de horarios de televisión).

- Empaquetado con Hardware: Integrar el software libre en un dispositivo físico o sistema cerrado y vender el equipo completo (ej. enrutadores, firewalls o consolas de entretenimiento).

- Patrocinio y Desarrollo Corporativo:
    
    - Muchas empresas dependen tanto de proyectos de código abierto que contratan a desarrolladores a tiempo completo para mantenerlos.
    
    - _Ejemplos notables:_ La Fundación Linux contrató a Linus Torvalds para dedicarse a Linux; Google contrató al creador de Python; AT&T paga a empleados exclusivamente para mantener proyectos de Ruby on Rails.

- Prestigio Profesional y Reclutamiento:
    
    - _Para el programador:_ Contribuir al código abierto es una forma de mostrar un currículum real y público. Los empleadores pueden ver directamente la calidad de tu trabajo.
    
    - _Para las empresas:_ Liberar partes de su código interno atrae a talentos de alto nivel interesados en el proyecto.

---
