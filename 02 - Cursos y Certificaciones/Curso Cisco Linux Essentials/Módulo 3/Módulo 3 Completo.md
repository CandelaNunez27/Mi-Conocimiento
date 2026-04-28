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
### 3 Línea de Comandos

Es una interfaz de entrada de texto que te permite darle instrucciones al sistema operativo, abarcando desde un comando simple de una sola palabra hasta scripts (secuencias de programación) muy complejos.

- **Cómo acceder a ella:**
    
    - En Modo Texto: Al iniciar sesión, te encuentras inmediatamente dentro de la consola.
    
    - *En Modo Gráfico: Debes iniciar un shell gráfico, que es básicamente la misma consola de texto tradicional pero dentro de una ventana que puedes mover, maximizar o redimensionar. *

---

### 4 Virtualización y Cloud Computing

Dado que el modo multiusuario clásico de Linux tiene límites (un usuario puede consumir todos los recursos del sistema), la industria utiliza la virtualización.

**Virtualización** 
Es dividir un servidor físico potente en varios servidores virtuales totalmente independientes.

- *Host (Anfitrión): El servidor físico real.*

- Hipervisor: El software que reparte la CPU, RAM y disco.

- *Invitados (Guests): Las máquinas virtuales (VMs). Funcionan aisladas y no saben que están virtualizadas.*

- Ventajas: Ahorro gigante en hardware, energía y espacio. Es muy fácil crear y borrar máquinas de prueba.


**Cloud Computing (La Nube)**
Es llevar la virtualización a una escala global, utilizando centros de datos remotos de terceros.

- El Modelo: En lugar de comprar y mantener tus propios servidores físicos, los alquilas en la nube de forma virtual.

- Pago por uso: Solo pagas por los recursos exactos (Gigabytes, CPU) que consumes al mes.

- El Rey de la Nube: Linux es el motor absoluto; la inmensa mayoría de la infraestructura en la nube funciona sobre su kernel.

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
