# Módulo 4

## 1 Introducción

**GUI (Interfaz Gráfica)**
Se controla haciendo clics. Es una forma fácil de administrar el sistema y resulta indispensable para trabajar con gráficos o videos.

 **CLI (Línea de Comandos)**
Se controla únicamente mediante el teclado. Aunque al principio cuesta porque exige memorizar comandos , ofrece mayor velocidad, un control más preciso y la capacidad de automatizar tareas (mediante scripting).

**¿Por qué elegir la CLI?:** 
Por la flexibilidad y movilidad que otorga. Si dominas la consola, serás capaz de operar de manera eficaz CUALQUIER distribución de Linux en cualquier empresa, sin depender de la interfaz gráfica que tengan instalada

---
## 2 Interfaz de Línea de Comandos (CLI)

La CLI es una interfaz basada en texto que funciona mediante el trabajo en equipo de dos elementos clave:

- El Terminal: Es la aplicación visible donde el usuario escribe los comandos y donde aparecen los resultados o los mensajes de error. Su función es tomar ese texto y pasárselo al shell.

- El Shell: Es el intérprete del sistema. Recibe el texto enviado por el terminal y lo traduce a instrucciones reales que el sistema operativo puede ejecutar

---
### 3 Acceso a la Terminal

El acceso a la línea de comandos depende de cómo inicie el sistema:

- Arranque Directo (Servidores): Inician directamente en la consola de texto para no desperdiciar recursos gráficos y maximizar la velocidad.

- Terminal de GUI: En sistemas con escritorio, es un programa que emula la terminal y se abre fácilmente desde los menús.

- Terminal Virtual: Es una consola pura que se ejecuta en paralelo a la interfaz gráfica. Se accede mediante atajos de teclado (como `Ctrl-Alt-F1`) y te exige iniciar sesión nuevamente antes de usarla. Puede no estar disponible si usas máquinas virtuales.

---
### 3.1 El Prompt (Símbolo del sistema)

El prompt es el indicador visual que aparece en la terminal cuando el sistema ha terminado de ejecutar cualquier proceso y está listo para que introduzcas un nuevo comando.

Aunque su aspecto puede variar según la distribución de Linux, normalmente proporciona información de contexto muy útil. Tomando como ejemplo la estructura `sysadmin@localhost:~$`:

- `sysadmin`: Indica el nombre del usuario que tiene la sesión iniciada.
- `localhost`: Es el nombre del equipo o sistema en el que estás trabajando.
- `~` (Tilde): Muestra el directorio actual en el que te encuentras. En el mundo Linux, este símbolo es una abreviatura universal para referirse al directorio personal (o home) de tu usuario (por ejemplo, `/home/sysadmin`).

---

### 5 Utilizar Linux para el Trabajo

**Ofimática: LibreOffice (y OpenOffice)**

Es la suite principal que cubre las tres grandes necesidades de oficina. Es altamente compatible con formatos de Microsoft Office y permite exportar directamente a PDF

- *Procesador de Textos (Writer): Para crear informes y memos. Soporta texto, imágenes, tablas y permite vincular datos desde una hoja de cálculo (para que los informes se actualicen automáticamente si cambian los números).*

- Hoja de Cálculo (Calc): Para números, análisis de ventas y predicciones. No solo usa celdas; permite aplicar fórmulas matemáticas complejas y generar gráficos dinámicos.

- Presentaciones: Para crear diapositivas para exponer con texto, gráficos y videos.

- Extras: Permite el uso de extensiones, pudiendo integrarse, por ejemplo, con software Wiki para intranets empresariales.


**Navegadores Web**

- Firefox y Google Chrome: consideran a Linux un "ciudadano de primera clase". Esto significa que las versiones de Linux reciben las actualizaciones, nuevas funciones y parches de seguridad al mismo tiempo que Windows o Mac.

- Limitación externa: Históricamente, algunos complementos cerrados de terceros (como el antiguo Adobe Flash) podían tener problemas, ya que dependían del soporte de empresas externas con otras prioridades.

---

### 6 Proteger tu Equipo Linux

Dado que Linux no distingue entre un usuario sentado frente al teclado y uno conectado desde internet, la seguridad es un factor obligatorio. Se basa en tres medidas fundamentales:

**1. Gestión de Contraseñas**

La regla de oro es usar contraseñas fuertes (mínimo 10 caracteres, combinando mayúsculas, minúsculas, números y símbolos) y únicas para cada sitio o servicio.

- *Herramienta clave: Para no tener que memorizar decenas de claves complejas, se recomienda usar un gestor como KeePassX. De esta forma, solo necesitas recordar la contraseña de inicio de sesión de tu equipo y la contraseña maestra de KeePassX.*

**2. Actualizaciones Constantes**

Mantener el software al día es vital para cerrar brechas de seguridad. En distribuciones como Ubuntu, *se puede configurar el sistema gráficamente para que busque actualizaciones diariamente*.* Las actualizaciones críticas (de seguridad) te pedirán instalarse de inmediato, mientras que el resto puede agruparse para instalarse semanalmente.


**3. Firewall (Cortafuegos)**

*Es un sistema que filtra el tráfico de red, bloqueando conexiones entrantes que no hayas solicitado tú mismo para evitar que las personas remotas ejecuten los programas en tu computadora.*

- iptables: Es el potente sistema de firewall que Linux trae integrado "bajo el capó" (se maneja mediante complejos comandos de texto).

- gufw: Es una interfaz gráfica (GUI) sencilla para el firewall de Ubuntu. Permite activar la protección con un solo clic y añadir excepciones fácilmente, sin tener que lidiar con la complejidad de `iptables`.

---
### 7 Protegerte a ti Mismo

Cada vez que navegas dejas un rastro o "huella digital". Para proteger tu información de anunciantes o atacantes maliciosos, ten en cuenta estas medidas:

**Datos y Contraseñas**
 Usa contraseñas únicas para cada sitio (apoyándote en gestores como KeePassX). Así, si hackean una página, el resto de tus cuentas estarán a salvo. Además, comparte solo los datos personales estrictamente necesarios para evitar que suplanten tu identidad en el banco.

**El Rastreo de las Cookies**
Las cookies "propias" son útiles (mantienen tu sesión iniciada), pero el problema son las cookies de terceros *(píxeles de anunciantes o botones/likes de redes sociales incrustados). Al estar en muchas webs distintas, rastrean tu actividad a través de todo internet para armar un perfil sobre ti.*

**Configuración del Navegador**
 Puedes limitar esto configurando tu navegador para que envíe la señal voluntaria de "No rastrear", rechace automáticamente las cookies de terceros y elimine el historial al cerrarse. *(Nota: una privacidad demasiado estricta puede hacer que algunas páginas dejen de funcionar bien).*
 
 **Anonimato Extremo con Tor** 
 *Si buscas ocultar totalmente quién eres y desde dónde te conectas, el Navegador Tor ("The Onion Router")* es la herramienta indicada. Rebota tu tráfico por distintos servidores del mundo para ocultar tu origen. La desventaja es que, por seguridad extrema, desactiva funciones (scripts) que hacen que muchas webs modernas no se vean bien.

---
