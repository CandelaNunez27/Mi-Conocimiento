# Módulo 2

## 1 Introducción
Este módulo se centra en conocer las principales herramientas y aplicaciones de código abierto, así como en entender cómo funcionan las licencias de este tipo de software.

---
## 2 Las Principales Aplicaciones de Código Abierto

En Linux, una computadora puede cumplir múltiples roles (como servidor, escritorio o máquina de desarrollo). La gran ventaja de Linux es que no hace distinción técnica entre estos roles; la función de la máquina depende únicamente de qué aplicaciones decidas instalar y configurar.

Ventaja para estudiantes y desarrollo: Permite simular entornos de producción completos (servidores reales) en hardware económico o máquinas virtuales, ahorrando los altísimos costos de equipos físicos y licencias comerciales.

El software en Linux se divide principalmente en tres categorías:

1. Software de Servidor: Funciona en segundo plano, sin interacción directa con el monitor o el teclado. Su función es procesar datos o servir información a otros equipos (llamados *clientes*).
2. Software de Escritorio: Aplicaciones con las que el usuario interactúa directamente (navegadores web, reproductores, editores). En muchos casos, este software actúa como un *cliente* que se conecta a un servidor. 

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260423231426.png)

3. Herramientas: Utilidades que facilitan la gestión del sistema operativo (herramientas de configuración, la terminal o *shell*, y compiladores de código).

Categoría adicional (Importante para el examen LPI):
Aplicaciones Móviles: Funcionan de manera similar a las de escritorio, pero están diseñadas para ejecutarse en teléfonos o tablets.

Diversidad y Libertad de Elección:
Para cualquier tarea en Linux, existen muchísimas opciones (distintos navegadores, múltiples editores de texto, etc.). La magia del código abierto es que, si a una persona o comunidad no le gusta cómo funciona un programa, tiene la libertad de tomar el código y crear el suyo propio. Una habilidad clave en Linux es aprender a evaluar qué software usar: si ir a lo seguro con la opción líder, o probar lo más nuevo y vanguardista.

---
## 2.1 Aplicaciones de Servidor
Linux es altamente confiable y eficiente para ejecutar servidores. La configuración depende de un principio básico: instalar el software adecuado para el servicio específico que se desea ofrecer.

1. Servidores Web
Alojan y entregan contenido a través de los protocolos HTTP/HTTPS. El contenido puede ser estático (archivos entregados tal cual están en el disco) o dinámico (generado al momento por aplicaciones, como WordPress).

- Apache: El líder histórico y dominante del mercado, mantenido por la Apache Software Foundation.

- nginx: Servidor enfocado en un altísimo rendimiento y concurrencia, utilizando características de kernels UNIX modernos.

2. Servidores de Correo Electrónico
El flujo de correo se divide en tres roles o componentes principales, lo que permite gran flexibilidad en Linux para elegir la herramienta ideal para cada etapa:

- MTA (Mail Transfer Agent): Usa SMTP para enrutar y transferir el correo entre servidores.
  Ejemplos: sendmail (el clásico) y Postfix (diseñado para ser más simple y seguro).

- MDA (Mail Delivery Agent / Agente Local): Recibe el correo del MTA y lo guarda en el buzón local del usuario.
  Ejemplo: procmail (permite crear filtros personalizados).

- Servidores POP/IMAP: Protocolos que permiten a los clientes de correo (las apps de los usuarios) conectarse al servidor y descargar/leer sus mensajes.
  Ejemplos: Dovecot (muy popular por su facilidad) y Cyrus IMAP.

3. Servidores para Compartir Archivos
La elección depende de los sistemas operativos que convivan en la red local:

- Samba: El estándar para redes mixtas. Permite que un servidor Linux se comporte como una máquina Windows (compartiendo archivos e integrándose a sus dominios).

- Netatalk: Permite a Linux comportarse como un servidor de archivos nativo para equipos Apple.

- NFS (Network File System): El protocolo nativo de UNIX/Linux. Suele estar integrado en el kernel y permite montar discos de red de forma transparente, como si fueran discos físicos locales.

4. Servicios de Infraestructura y Directorio
Servicios críticos para el funcionamiento de cualquier red de datos:

- DNS (Domain Name System): Traduce nombres de dominio (ej. linux.com) a direcciones IP. El software más utilizado es bind (mantenido por el Internet Software Consortium - ISC).

- LDAP (Lightweight Directory Access Protocol): Base de datos jerárquica (en forma de árbol) para centralizar directorios de usuarios, roles y autenticación. El líder indiscutido es OpenLDAP.

- DHCP (Dynamic Host Configuration Protocol): Asigna dinámicamente direcciones IP a los equipos cuando se conectan a la red. El servidor más común es ISC DHCP.

5. Bases de Datos
Almacenan información estructurada y permiten realizar consultas o reportes utilizando el lenguaje SQL (Structured Query Language).

- Líderes de código abierto: MySQL y PostgreSQL.

---

### 2.2 Aplicaciones de Escritorio

Aunque los servidores son el fuerte de Linux, también cuenta con un riquísimo ecosistema de aplicaciones para el usuario final (escritorio).

**La Interfaz Gráfica (Cómo funciona lo visual)**

- X Window (X11 / X.org): Es el servidor gráfico base. Permite que el software opere en modo visual y acepta las entradas del teclado y el ratón.

- Administrador de Ventanas: Es el nivel básico. Se encarga de dibujar los menús y gestionar las ventanas en la pantalla (Ejemplos: _Compiz, FVWM, Enlightenment_).

- Entorno de Escritorio: Es el nivel completo. Incluye su propio administrador de ventanas, pero le suma pantallas de inicio, administrador de archivos y muchísimas utilidades integradas. Los dos gigantes indiscutibles son KDE y GNOME.


**Ofimática (Productividad)**

La alternativa libre a Microsoft Office.

- LibreOffice y OpenOffice: Ambas ofrecen procesador de textos, hojas de cálculo, presentaciones y buscan compatibilidad total con los formatos de Microsoft.

- _Historia y política del Open Source:_ Originalmente, _Sun Microsystems_ liberó OpenOffice. Cuando _Oracle_ compró Sun, la comunidad desconfió del soporte que Oracle le daría al proyecto. Como resultado, el proyecto se "bifurcó" (se dividió) creando LibreOffice. Hoy en día, LibreOffice tiene el mayor impulso y viene por defecto en la mayoría de las distribuciones.

**Navegadores Web y Correo Electrónico**

- Navegadores: Firefox y Google Chrome dominan el mercado de código abierto. Su sana competencia obliga a ambos equipos a innovar constantemente, lo que beneficia a todos los usuarios de internet.

- Clientes de Correo (Escritorio):  Thunderbird (de los creadores de Firefox/Mozilla).
    
    - **Evolution** (del entorno GNOME).
    
    - **KMail** (del entorno KDE).
    
    - _Ventaja:_ Al usar protocolos estándar (POP, IMAP, SMTP), puedes cambiar de un cliente a otro sin perder tus correos.


**Herramientas Creativas y Multimedia**

- Blender: Modelado, animación y creación de películas en 3D (utilizado incluso en producciones de Hollywood).

- GIMP: Manipulación y edición de imágenes en 2D (la gran alternativa a Photoshop).

- Audacity: Grabación y edición de audio.

---

### 2.3 Herramientas de Consola

La administración del sistema y la automatización de tareas en Linux se realizan a través de la línea de comandos utilizando un shell.

**El Shell y el Prompt**
El shell es la interfaz que recibe tus comandos y se los pasa al kernel para que los ejecute. Al abrir la terminal, ves el prompt (la línea que espera tus órdenes), que tiene una estructura típica como esta: `usuario@servidor:~$`

* `~` (Tilde o virgulilla): Es el atajo para referirse a tu directorio personal (*home*).
* `$` (Signo de dólar): Indica que estás usando una cuenta estándar (sin privilegios de administrador/root).

**Tipos de Shell**
Existen diferentes shells para elegir, variando en su sintaxis y capacidades para hacer *scripts* (programación de tareas):
* Familia Bourne: Su versión moderna es Bash (*Bourne Again Shell*). Es el shell predeterminado en la inmensa mayoría de los sistemas Linux.
* Familia C shell: Usa una sintaxis prestada del lenguaje C. Su versión moderna es tcsh.
* Otros populares: *Korn shell (ksh)* y *zsh*.

**Editores de Texto en Consola**
Son vitales para editar archivos de configuración directamente desde la terminal, sin interfaz gráfica.
* Avanzados y complejos: vi (y su versión mejorada vim) y emacs. Son extremadamente potentes pero tienen una curva de aprendizaje alta.
* Básicos y sencillos: nano y pico. Ideales para ediciones rápidas y simples.
* La regla de oro de Linux: Aunque uses *nano* o *emacs* a diario, debes aprender el uso básico de `vi`. Es el único editor que viene preinstalado por obligación en *todos* los sistemas Linux, lo cual es vital si entras a un modo de recuperación para reparar un sistema dañado.

**Administradores de Paquetes**
Atrás quedaron los días de compilar software manualmente. Hoy se usan paquetes (aplicaciones empaquetadas y listas) que se descargan de servidores en internet llamados repositorios.
* En sistemas Debian (ej. Ubuntu, Mint): Se usan los comandos `dpkg`, `apt-get` y `apt-cache`.
* En sistemas Red Hat (ej. CentOS, Fedora): Se usan los comandos `rpm` y `yum`.

---

### 2.4 Herramientas de Desarrollo

Linux es una plataforma de primer nivel para programadores, ofreciendo un excelente soporte para múltiples lenguajes. Los lenguajes de programación se dividen en dos grandes grupos:

**Lenguajes Compilados** 

Se traducen completamente a código de máquina _antes_ de que el programa se ejecute. Son más rápidos y eficientes.

- C: Es el lenguaje en el que está escrito Linux. Es sumamente eficiente, requiere pocos recursos y es ideal para sistemas operativos porque se ejecuta rapidísimo. (A partir de él nacieron _C++_ y _Objective C_).

**El caso especial de Java (Compilación Intermedia):**

- Java: No compila directamente al lenguaje del equipo, sino a un código intermedio (_bytecode_) pensado para una CPU hipotética llamada Máquina Virtual de Java (JVM).

- _La gran ventaja:_ Puedes ejecutar un programa de Java en cualquier dispositivo del mundo (PC, servidor, TV) siempre y cuando tenga la JVM instalada. Además, la JVM se encarga de tareas complejas como asignar la memoria automáticamente.


**Lenguajes Interpretados** 

Se traducen a código de máquina línea por línea _mientras_ el programa se está ejecutando. Consumen más recursos del equipo, pero aumentan enormemente la productividad del programador (escriben menos código y no pierden tiempo compilando).

- Perl: Nacido para manipular texto, es el clásico favorito de los administradores de sistemas para automatizar tareas.

- PHP: Diseñado para crear páginas web dinámicas (trabaja en conjunto con servidores como Apache). Es muy fácil de aprender y es la base de proyectos gigantes como WordPress.

- Ruby: Facilita la programación compleja. Muy famoso por su entorno web _Ruby on Rails_ y por ser la base de herramientas modernas para gestionar servidores de Linux (como _Chef_ y _Puppet_).

- Python: Su sintaxis facilita tareas difíciles. Es el gran favorito en el mundo académico por sus potentes capacidades de procesamiento estadístico y de datos. Su entorno web más famoso es _Django_.


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
    
    - Licencia: Linus Torvalds utiliza la GPLv2 (_GNU Public License versión 2_).
    
    - Libertades y Reglas: El código fuente debe estar siempre disponible. Puedes modificarlo como quieras. Sin embargo, tiene una condición (copyleft): si distribuyes tus cambios, debes hacerlo bajo esta misma licencia para que la comunidad siga beneficiándose. Además, no puedes cobrar por el código fuente en sí, solo por los gastos de distribución física si los hubiera.


**FOSS (Software Libre y de Código Abierto)**

FOSS (_Free and Open Source Software_) agrupa a todo este tipo de software donde el creador original "libera" su derecho a restringir quién o cómo se usa el programa, garantizando el acceso y la redistribución del código fuente.

Diversidad de Licencias: Dado que el licenciamiento tiene un fuerte componente político y filosófico, muchas organizaciones han creado sus propias licencias de código abierto que se adaptan a sus intereses (ej. la licencia MIT, la de la Universidad de California, la de la Fundación Apache o las de la _Free Software Foundation_).

---

### 3.1 La Free Software Foundation y el Open Source Initiative

Existen dos grandes organizaciones que lideran el mundo del código abierto, cada una con su propia filosofía:

| **Característica**       | **Free Software Foundation (FSF)**                                                                                    | **Open Source Initiative (OSI)**                                                                                          |
| ------------------------ | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| **Fundadores**           | Richard Stallman (1985).                                                                                              | Bruce Perens y Eric Raymond (1998).                                                                                       |
| **Enfoque**              | "Software Libre": Se enfoca en la ética y la libertad. Consideran que el software cerrado/propietario es perjudicial. | "Código Abierto": Nació porque sentían que la FSF era muy extrema/política. Tienen un enfoque más práctico y empresarial. |
| **Regla de Oro**         | Copyleft: Si modificas un software libre, _estás obligado_ a compartir tus cambios bajo la misma licencia.            | Permisivo: Cero restricciones. Puedes usar el código abierto y modificarlo, sin estar obligado a compartir tus cambios.   |
| **Gestión de Licencias** | Crea sus propias licencias (Familia GPL).                                                                             | No crea licencias; evalúa y _certifica_ licencias de terceros que cumplen sus principios.                                 |
**Detalles Clave de la FSF (Free Software Foundation)**

- Licencias GPL y LGPL: Crearon la GPL (la de Linux) y la LGPL (_Lesser GPL_). La diferencia es que la LGPL permite que el software libre se enlace o trabaje junto a software cerrado (como un controlador de hardware propietario).

- Activismo: Luchan contra las patentes de software y el DRM (Administración de Derechos Digitales) porque restringen la libertad del usuario.

- "Tivoización": La empresa _TiVo_ usó Linux en sus grabadoras. Cumplió con entregar el código fuente, pero diseñó su hardware para que _rechazara_ cualquier código modificado por el usuario.
    
    - La FSF consideró esto una trampa y creó la **GPLv3** para prohibirlo.
    
    - Linus Torvalds estuvo en desacuerdo con la FSF en este punto, por lo que el kernel de Linux se quedó en la versión **GPLv2**.


**Detalles Clave de la OSI (Open Source Initiative)**

- Licencias Permisivas (BSD y MIT): La OSI certifica licencias muy simples cuyo único gran requisito es: _"Haz lo que quieras, pero no digas que lo escribiste tú (respeta el derecho de autor original)"_.

- A diferencia del _Copyleft_ de la FSF, con una licencia permisiva (como BSD) puedes tomar código abierto, modificarlo y venderlo como un producto de código cerrado. Por esta razón, la FSF no aprueba este tipo de licencias.

---

### 3.2 Más Términos para lo Mismo (FOSS y FLOSS)

Para evitar debates constantes entre las posturas de la FSF y la OSI, la comunidad empezó a utilizar siglas que agrupan a ambos mundos:

- FOSS (Software Libre y de Código Abierto): Agrupa tanto los principios de _Free Software_ como de _Open Source_.

- El problema de la traducción: En inglés, la palabra _"free"_ es ambigua. Puede significar gratuito ("gratis como una cerveza") o libre ("libre como la libertad de expresión").

- FLOSS: Para solucionar esta ambigüedad del inglés, se incluyó la palabra _"Libre"_ (del español/francés), creando las siglas FLOSS (_Free / Libre / Open Source Software_).

Conclusión práctica: Aunque estos términos "paraguas" ocultan las profundas diferencias filosóficas entre la FSF y la OSI, a nivel práctico significan una cosa muy clara para el usuario: *si un software es FOSS/FLOSS, sabes que no tienes que pagar por él y que tienes el derecho de redistribuirlo.*

---

### 3.3 Otros Esquemas de Concesión de Licencias

Las licencias de software (FOSS) no están pensadas para obras creativas como dibujos, textos o planos. Para este tipo de contenido se usan otros esquemas:

- **Dominio Público (CC0):** El autor renuncia a _todos_ los derechos sobre su obra. Cualquiera puede usarla sin restricciones.

- **Licencias Creative Commons (CC):** Permiten al autor elegir exactamente qué permisos otorga sobre su obra, combinando estas 4 reglas básicas:
    
    - **BY (Atribución):** Uso libre, pero es obligatorio dar crédito al autor.
    
    - **SA (Compartir Igual / ShareAlike):** Las obras derivadas deben usar esta misma licencia (funciona como el _copyleft_).
    
    - **ND (Sin Derivadas / No-Derivs):** Se puede compartir la obra, pero _está prohibido modificarla_.
    
    - **NC (No Comercial):** Prohíbe utilizar la obra para ganar dinero.

_(Estas reglas se combinan para crear la licencia deseada. Por ejemplo, **CC-BY-NC** te obliga a dar crédito y te prohíbe el uso comercial)_

