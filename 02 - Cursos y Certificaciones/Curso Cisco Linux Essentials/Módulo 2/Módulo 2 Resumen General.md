# Módulo 2

### Conceptos Fundamentales y Roles

- **Roles de la máquina:** En Linux, no existe una distinción técnica entre un servidor, un escritorio o una máquina de desarrollo; la función depende exclusivamente del software que decidas instalar y configurar.

- **Categorías de software:** Se divide en software de **servidor** (procesa datos en segundo plano y atiende clientes), software de **escritorio** (interactúa con el usuario), **herramientas** (para gestionar el sistema) y **aplicaciones móviles**.


---

### Aplicaciones de Servidor y Red

La regla de oro es instalar el software específico para el servicio que deseas ofrecer.

- **Servidores Web:** Alojan contenido mediante HTTP/HTTPS.
    
    - _Apache:_ El líder histórico del mercado.
    
    - _nginx:_ Enfocado en altísimo rendimiento.

- **Correo Electrónico (E-mail):**
    
    - _MTA (Mail Transfer Agent):_ Enruta el correo (ej. **sendmail**, **Postfix**).
    
    - _MDA (Mail Delivery Agent):_ Entrega localmente en el buzón (ej. **procmail**).
    
    - _POP/IMAP:_ Protocolos para leer el correo (ej. **Dovecot**, **Cyrus IMAP**).

- **Compartir Archivos:**
    
    - _Samba:_ Para redes con máquinas Windows.
    
    - _Netatalk:_ Para redes con máquinas Apple.
    
    - _NFS:_ Nativo de UNIX/Linux, integrado al kernel.

- **Infraestructura de Red y Bases de Datos:**
    
    - _DNS:_ Traduce dominios a IPs (el software líder es **bind**).
    
    - _LDAP:_ Directorio jerárquico de usuarios (líder: **OpenLDAP**).
    
    - _DHCP:_ Asigna direcciones IP dinámicamente (líder: **ISC DHCP**).
    
    - _Bases de Datos:_ Almacenan información consultable mediante SQL (líderes: **MySQL** y **PostgreSQL**).


---

### Aplicaciones de Escritorio y Multimedia

- **La Interfaz Gráfica (GUI):**
    
    - _X Window (X11 / X.org):_ El servidor gráfico base que acepta teclado y ratón.
    
    - _Administrador de ventanas:_ Dibuja menús y recuadros (ej. Compiz).
    
    - _Entorno de escritorio:_ Paquete completo con utilidades. Los gigantes son **KDE** y **GNOME**.
    
- **Ofimática:** **LibreOffice** y **OpenOffice** son las alternativas a MS Office. _(LibreOffice nació como una bifurcación de OpenOffice cuando Oracle compró Sun Microsystems)_.

- **Navegadores y Correo Local:** Destacan **Firefox** y **Google Chrome** en la web , y **Thunderbird**, **Evolution** o **KMail** para gestionar correos locales.

- **Creatividad:** **Blender** (películas/modelado 3D) , **GIMP** (imágenes 2D) , **Audacity** (audio).


---

### ⌨️ Herramientas de Consola y Desarrollo _(Repaso)_

- **Shell:** La interfaz de comandos. **Bash** es el predeterminado en la mayoría de sistemas.

- **Editores de texto:** **vi / vim** (complejos y presentes en _todos_ los sistemas Linux, vitales para recuperación), **emacs**, **nano** y **pico** (básicos).

- **Gestores de paquetes:** `dpkg`/`apt-get` en Debian/Ubuntu; `rpm`/`yum` en Red Hat.

- **Lenguajes:**
    
    - _Compilados:_ **C** (lenguaje base de Linux) y **Java** (usa la máquina virtual JVM para funcionar en cualquier equipo).
    
    - _Interpretados:_ **Perl** (scripts de sistema), **PHP** (web), **Ruby** y **Python** (poderosos y usados en automatización/datos).


---

### 📜 Licencias y Modelos de Negocio

- **FSF vs. OSI:**
    
    - **Free Software Foundation (FSF):** Liderada por Richard Stallman. Filosofía estricta de _Software Libre_. Usan la familia de licencias **GPL** que impone el **Copyleft** (obligación de compartir modificaciones).
    
    - **Open Source Initiative (OSI):** Filosofía práctica de _Código Abierto_. Aprueban licencias **permisivas** como **BSD** o **MIT** (puedes usar y modificar sin obligación de compartir el código modificado).

- **FOSS / FLOSS:** Términos universales para referirse al Software Libre y de Código Abierto en conjunto, garantizando que el usuario no paga y puede redistribuirlo.

- **Creative Commons (CC):** Esquemas de licencias para obras no de software (arte, textos).
    
    - **CC0:** Dominio público total.
    
    - Reglas combinables: **BY** (Atribución obligatoria) , **SA** (ShareAlike / Copyleft) , **ND** (Sin Derivadas / no modificar) , **NC** (No Comercial).

- **Cómo ganar dinero (Modelos de Negocio):**
    
    - Vender soporte, garantías o consultoría (el método más común).
    
    - Cobrar por suscripciones a servicios adicionales.
    
    - Vender dispositivos físicos (hardware) que traen el software preinstalado.
    
    - Patrocinios corporativos (ej. empresas que contratan a desarrolladores a tiempo completo para mantener proyectos).
    
    - Prestigio para conseguir empleos de alto nivel (el código es tu currículum público).


