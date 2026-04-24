# Módulo 2

## 1 Introducción
Este módulo se centra en conocer las principales herramientas y aplicaciones de código abierto, así como en entender cómo funcionan las licencias de este tipo de software.

## 2 Las Principales Aplicaciones de Código Abierto

En Linux, una computadora puede cumplir múltiples roles (como servidor, escritorio o máquina de desarrollo). La gran ventaja de Linux es que no hace distinción técnica entre estos roles; la función de la máquina depende únicamente de qué aplicaciones decidas instalar y configurar.

Ventaja para estudiantes y desarrollo: Permite simular entornos de producción completos (servidores reales) en hardware económico o máquinas virtuales, ahorrando los altísimos costos de equipos físicos y licencias comerciales.

El software en Linux se divide principalmente en tres categorías:

1. Software de Servidor: Funciona en segundo plano, sin interacción directa con el monitor o el teclado. Su función es procesar datos o servir información a otros equipos (llamados *clientes*).
2. Software de Escritorio: Aplicaciones con las que el usuario interactúa directamente (navegadores web, reproductores, editores). En muchos casos, este software actúa como un *cliente* que se conecta a un servidor. 

![338](04%20-%20Otros/Imagenes/Pasted%20image%2020260423231426.png)

3. Herramientas: Utilidades que facilitan la gestión del sistema operativo (herramientas de configuración, la terminal o *shell*, y compiladores de código).

Categoría adicional (Importante para el examen LPI):
Aplicaciones Móviles: Funcionan de manera similar a las de escritorio, pero están diseñadas para ejecutarse en teléfonos o tablets.

Diversidad y Libertad de Elección:
Para cualquier tarea en Linux, existen muchísimas opciones (distintos navegadores, múltiples editores de texto, etc.). La magia del código abierto es que, si a una persona o comunidad no le gusta cómo funciona un programa, tiene la libertad de tomar el código y crear el suyo propio. Una habilidad clave en Linux es aprender a evaluar qué software usar: si ir a lo seguro con la opción líder, o probar lo más nuevo y vanguardista.


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

### 2.2 Aplicaciones de Escritorio

Aunque los servidores son el fuerte de Linux, también cuenta con un riquísimo ecosistema de aplicaciones para el usuario final (escritorio).

** La Interfaz Gráfica (Cómo funciona lo visual)**

Por defecto, una estación de trabajo Linux es solo texto. Para tener una interfaz gráfica (GUI) y usar el ratón, se necesitan capas de software:

- **X Window (X11 / X.org):** Es el servidor gráfico base. Permite que el software opere en modo visual y acepta las entradas del teclado y el ratón.
    
- **Administrador de Ventanas:** Es el nivel básico. Se encarga de dibujar los menús y gestionar las ventanas en la pantalla (Ejemplos: _Compiz, FVWM, Enlightenment_).
    
- **Entorno de Escritorio:** Es el nivel completo. Incluye su propio administrador de ventanas, pero le suma pantallas de inicio, administrador de archivos y muchísimas utilidades integradas. Los dos gigantes indiscutibles son **KDE** y **GNOME**.
    

#### 2. Ofimática (Productividad)

La alternativa libre a Microsoft Office.

- **LibreOffice y OpenOffice:** Ambas ofrecen procesador de textos, hojas de cálculo, presentaciones y buscan compatibilidad total con los formatos de Microsoft.
    
- _Historia y política del Open Source:_ Originalmente, _Sun Microsystems_ liberó **OpenOffice**. Cuando _Oracle_ compró Sun, la comunidad desconfió del soporte que Oracle le daría al proyecto. Como resultado, el proyecto se "bifurcó" (se dividió) creando **LibreOffice**. Hoy en día, LibreOffice tiene el mayor impulso y viene por defecto en la mayoría de las distribuciones.
    

#### 3. Navegadores Web y Correo Electrónico

- **Navegadores:** **Firefox** y **Google Chrome** dominan el mercado de código abierto. Su sana competencia obliga a ambos equipos a innovar constantemente, lo que beneficia a todos los usuarios de internet.
    
- **Clientes de Correo (Escritorio):** * **Thunderbird** (de los creadores de Firefox/Mozilla).
    
    - **Evolution** (del entorno GNOME).
        
    - **KMail** (del entorno KDE).
        
    - _Ventaja:_ Al usar protocolos estándar (POP, IMAP, SMTP), puedes cambiar de un cliente a otro sin perder tus correos.
        

##### 4. Herramientas Creativas y Multimedia

Linux cuenta con software de nivel profesional para creadores:

- **Blender:** Modelado, animación y creación de películas en **3D** (utilizado incluso en producciones de Hollywood).
    
- **GIMP:** Manipulación y edición de imágenes en **2D** (la gran alternativa a Photoshop).
    
- **Audacity:** Grabación y edición de **audio**.
    

¡Seguimos avanzando! Envíame el siguiente punto cuando estés listo.