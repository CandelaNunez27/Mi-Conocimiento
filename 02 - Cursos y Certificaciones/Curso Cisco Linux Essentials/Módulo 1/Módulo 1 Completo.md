# Módulo 1
## 1. Introducción
Linux es de Código Abierto, o sea, no es propiedad de una empresa. Libera a los usuarios de los costos de licencia y permite modificar el código según las necesidades cambiantes.

## 2. La evolución de Linux y los sistemas operativos populares
**¿Qué es Linux?**   Técnicamente es solo el kernel (núcleo), el controlador central de la comunicación entre el hardware del equipo y el software. Pero, comúnmente se refiere a una distribución (el sistema operativo completo: el kernel más un conjunto de herramientas).

**La relación entre Linux y UNIX:**
- UNIX: Sistema operativo creado en los años 70. Hoy es una marca registrada de Open Group; solo el software certificado por ellos puede llamarse así.
- Linux: Aunque adopta los requisitos de UNIX y funciona casi igual, no tiene la certificación oficial. Por lo tanto, no es UNIX, sino un sistema "tipo UNIX".

### 2.1 Rol del Kernel
El kernel actúa como el administrador central de los recursos de hardware:

- Gestión de procesos y memoria: Asigna memoria a los programas, inicia o finaliza procesos y arbitra el uso de recursos para evitar colapsos.

- Multitarea preferente: Gestiona el uso de la CPU entre múltiples tareas. El kernel decide cuándo cambiar de una aplicación a otra rápidamente, creando la ilusión de ejecución simultánea.

- Gestión de entrada/salida (E/S): Controla el acceso al disco, la visualización de texto en el monitor y las conexiones de red.

- Gestor de arranque(**bootloader**): **Es el código inicial que carga el kernel en memoria al encender la computadora**. En sistemas tipo UNIX, suele ser visible y editable.

- Transferencia de control: Una vez cargado, el kernel inicia los servicios necesarios (red, servidores, etc.) para que el equipo sea funcional. 

### 2.2 Las Aplicaciones
Las aplicaciones dependen totalmente del kernel para funcionar y obtener recursos.

- Abstracción del hardware (API): El kernel oculta la complejidad física del equipo. Las aplicaciones no necesitan saber qué tipo o marca de disco duro se está utilizando; simplemente se comunican con el kernel a través de su API (Interfaz de Programación de Aplicaciones), y este hace el trabajo pesado.

- El concepto de "Proceso": Al kernel no le importa si un programa es visual para el usuario (como un procesador de texto) o un servicio interno de red. Para el sistema operativo, cualquier tarea cargada y rastreada es simplemente un proceso.

- Gestión de recursos: Una sola aplicación puede requerir múltiples procesos para funcionar. El kernel es el único responsable de iniciar, detener y asignar los recursos del sistema (CPU, memoria, almacenamiento) a cada uno de estos procesos según sea necesario. 

### 2.3 Rol de Código Abierto
Origen: Inició en 1991 como un proyecto personal de Linus Torvalds. Al crearse desde cero de forma abierta, la comunidad de usuarios pudo influir en su desarrollo y evitar los errores de sistemas UNIX anteriores.

Código Fuente y Compilación: El software se escribe en código fuente (**instrucciones legibles por humanos; el kernel de Linux está escrito íntegramente en C**). Como la computadora no lo entiende de forma directa, un programa llamado compilador se encarga de traducirlo a instrucciones o código de máquina (ejecutable).

Filosofías de licenciamiento:

- **Código Cerrado**: El usuario solo recibe y tiene derecho a usar el código de máquina final. **Las licencias suelen prohibir expresamente ver o intentar aplicar ingeniería inversa para descubrir el código fuente**.

- Código Abierto (Open Source): Se centra en garantizar el derecho de obtener, modificar y compartir el código fuente original. Aunque existen distintas variantes con diferentes reglas de redistribución, todas garantizan el acceso al código.

El aporte del Proyecto GNU: Fue una iniciativa paralela (cuyo acrónimo significa "GNU No es Unix") que desarrollaba herramientas libres de alta calidad (como compiladores e interfaces). Linux adoptó estas utilidades gratuitas, integrándolas con su kernel para conformar el sistema operativo completo y funcional que conocemos hoy.

### 2.4 Distribuciones de Linux
Una distribución es un sistema listo para usar que empaqueta el kernel, herramientas GNU, aplicaciones y un gestor de paquetes. Aunque existan miles de distribuciones, los comandos y programas base son iguales o muy similares en todas.

Las principales familias son:

**Familia Red Hat (paquetes RPM- Red Hat Package Manager):**

- RHEL (Enterprise): Para servidores y empresas (muy estable, de pago).

- Fedora: Para escritorio (gratis, software muy actualizado).

- CentOS: Clon exacto y gratuito de RHEL (sin soporte técnico de pago).

- Scientific Linux: Orientada a la ciencia (usada en el CERN).

**Familia SUSE:**

- Open SUSE: Comunitaria y gratuita (escritorio).

- SUSE Enterprise: Comercial y de pago (servidores).

**Familia Debian (paquetes .deb):**

- Debian: Proyecto 100% comunitario y muy estricto con el código abierto.

- **Ubuntu**: **Derivada de Debian**, muy popular y con soporte comercial de la empresa Canonical.

- Linux Mint: Basada en Ubuntu, es actualmente la más popular y fácil de usar para escritorio.

### 2.4.1 ¿Qué es un Comando?
Básicamente, un comando es un programa que, al ejecutarse en la línea de comandos (CLI), realiza un trabajo: lee una entrada, procesa los datos y devuelve una salida.

Sin embargo, desde la perspectiva de su origen, los comandos se dividen en cuatro tipos:

- Integrados en el shell (Built-ins): Vienen incorporados directamente en el shell (como bash). El sistema sabe cómo ejecutarlos inmediatamente sin buscar programas externos. Ej: *cd*.

- Almacenados en archivos (Ejecutables): Son programas guardados en el sistema. El shell busca en los directorios listados en la variable PATH para encontrarlos y ejecutarlos. Ej: *ls*.

- Alias: Son "apodos" o atajos personalizados para un comando largo o una serie de comandos. Ej: crear un alias llamado *mycal* que ejecute automáticamente *cal 2014*, *alias mycal="cal 2014"*.

- Funciones: Son agrupaciones de comandos existentes para crear rutinas nuevas o reemplazar comandos. Al igual que los alias, suelen cargarse automáticamente al iniciar el shell.

### 2.5 Plataformas de Hardware
Evolución: Pasó de funcionar exclusivamente en la PC básica de su creador a soportar desde computadoras convencionales hasta supercomputadoras.

Sistemas Integrados (Embedded): Se adaptó a chips pequeños para dispositivos cotidianos (como enrutadores o grabadoras). Resulta más eficiente y económico para los fabricantes usar Linux como base que crear sistemas desde cero.

**Dispositivos Móviles: El sistema operativo Android utiliza el kernel de Linux**. Esto aceleró el desarrollo de teléfonos y tablets, permitiendo a las empresas enfocarse en la interfaz del usuario final.

Transparencia: En la mayoría de estos dispositivos de consumo, el usuario no nota que está usando Linux; el kernel simplemente opera de forma invisible y estable en segundo plano.

### 3 Elegir un Sistema Operativo
Existen diversas opciones de sistemas operativos: los "tipo UNIX" (como Linux), los UNIX certificados, y los no-UNIX (como Windows).

La elección correcta se reduce a una pregunta fundamental: "¿Qué hará esta máquina?". El sistema operativo debe elegirse basándose estrictamente en el software que necesitas ejecutar.

### 3.1 Puntos de Decisión
Al elegir y configurar un sistema operativo, debes evaluar los siguientes factores clave:

Rol de la máquina:
- Escritorio: Usa interfaz gráfica (GUI) para interactuar con el usuario.
- Servidor: Sin interfaz gráfica para ahorrar recursos; su fin es alojar servicios.

Ciclos de Vida y Actualización:	
**Diferenciamos ciclo de liberación -cada cuánto sale uno nuevo- del ciclo de mantenimiento -cuánto tiempo recibe actualizaciones-.**
- Ciclo largo (ej. RHEL): Ideal para servidores. Prioriza la estabilidad a largo plazo.
- Ciclo corto (ej. Fedora): Ideal para escritorios. Ofrece el software más reciente.

Madurez del Software:
- Estable: Rigurosamente probado y seguro (obligatorio para servidores).
- Beta: Incluye funciones nuevas, pero aún está en fase de pruebas.

Compatibilidad:
- La capacidad del nuevo sistema operativo para seguir ejecutando tu software antiguo.

Costo y Gestión:
- Considerar el precio de licencias, el pago por soporte técnico, el hardware necesario y el nivel de conocimientos de tu equipo administrador.

### 3.2 Microsoft Windows
Versiones de Escritorio:

- Ciclo de vida: Nuevas versiones cada 3 a 5 años con soporte a largo plazo.

- Compatibilidad: Su gran prioridad es la compatibilidad con versiones anteriores, llegando a incluir tecnología de máquinas virtuales para asegurar que el software antiguo siga funcionando. **Windows no tenía ninguna compatibilidad con Linux.**

Versiones de Servidor:

- Interfaz: A diferencia de los servidores Linux, incluye una interfaz gráfica (GUI) por defecto. También puede instalarse un paquete opcional para que se vea como un escritorio tradicional.

- Línea de comandos: Ha mejorado enormemente su capacidad de administración y automatización a través de la herramienta de scripting PowerShell.

### 3.3 Apple OS X
Base UNIX: **A diferencia de Linux, OS X es un sistema operativo UNIX certificado, basado parcialmente en el proyecto FreeBSD.**

Enfoque Principal: Está diseñado principalmente para escritorio, aunque cuenta con paquetes opcionales para gestionar servicios de red (como compartir archivos o inicios de sesión).

Ventajas: Es considerado muy intuitivo y fácil de usar. Su gran popularidad le asegura un excelente soporte por parte de los desarrolladores de software.

Nicho de Mercado: Es la opción predilecta en las industrias creativas (como la producción de video y diseño).

Hardware Exclusivo: Es un claro ejemplo de cómo la necesidad de una aplicación define el sistema operativo, y este a su vez el hardware, ya que OS X solo se ejecuta de forma oficial en equipos fabricados por Apple.

### 3.4 BSD (Berkeley Software Distribution)
BSD es una familia de sistemas operativos de código abierto, siendo una alternativa a Linux aunque funcionan de manera muy similar y comparten una gran cantidad de software en común. Sus proyectos más destacados son OpenBSD, FreeBSD y NetBSD.

- Rol principal: Se implementan fundamentalmente en servidores.
- Rol secundario: También pueden usarse como equipos de escritorio mediante la instalación de entornos gráficos como GNOME o KDE.

### 3.5 Otros UNIX Comerciales (Oracle Solaris, IBM AIX y HP-UX)
**Los UNIX comerciales, a diferencia de Linux, sí pagan y pasan por la certificación oficial para usar el nombre UNIX legalmente.**

Hardware propietario: A diferencia de Linux, estos sistemas se ejecutan exclusivamente en los equipos fabricados por sus propios creadores. Suelen ser máquinas grandes y muy potentes, diseñadas para integrarse con mainframes (sistemas informáticos heredados).

¿Por qué se eligen?

- Por requerimientos estrictos de la aplicación (hardware específico o necesidad de alta redundancia).

- Por ecosistema corporativo: Muchas empresas los eligen porque ya tienen una infraestructura o tradición con esa marca. Por ejemplo, una empresa usará IBM AIX si ya cuenta con hardware heredado de IBM o utiliza su software (como WebSphere).

### 3.6 Linux
Existen desde versiones comerciales para servidores hasta distribuciones creadas para tareas muy específicas (como convertir un equipo viejo en un firewall).

Soporte de Software y Empresarial:

- Los desarrolladores de aplicaciones solo dan soporte a un grupo reducido de distribuciones debido a las variaciones en las bibliotecas del sistema.

- Gobiernos y grandes empresas suelen elegir distribuciones que ofrecen soporte comercial de pago para mitigar riesgos de caídas del sistema.

Ciclos de Liberación y Soporte:

- LTS (Long Term Support): Soporte a largo plazo (5 años o más), ideal para entornos que requieren máxima estabilidad.

- Soporte corto: Ciclos de actualización rápidos (ej. cada 6 meses) pero con una vida útil breve (2 años o menos).

Niveles de Estabilidad:

- Estable: Software rigurosamente probado, seguro y confiable.

- De prueba (Testing) / Beta: Versiones preliminares para encontrar y solucionar errores.

- Inestable (ej. Debian "sid"): Prioriza incluir las funciones más nuevas y recientes a costa de sacrificar la fiabilidad (puede presentar errores graves o fallos de dependencias).

- Ejemplo de ecosistema: Fedora funciona como el entorno "Beta" o de pruebas de la comunidad; allí se ensayan las nuevas funciones antes de que sean consideradas lo suficientemente estables para integrarse en Red Hat Enterprise Linux (RHEL).


### 3.7 Android
Es la **distribución Linux para móviles más popular del mundo**, patrocinada por Google.

La diferencia clave (Sin GNU): Usa el kernel de Linux, pero no incluye las herramientas tradicionales de GNU ni entornos gráficos clásicos (como Xorg). En su lugar, utiliza la máquina virtual Dalvik para ejecutar aplicaciones.

Incompatibilidad con Escritorio: Las distribuciones Linux (como Ubuntu) no pueden usar aplicaciones de Google Play. La terminal nativa de Android carece de los comandos clásicos de Linux.

Solución técnica: Si se necesita usar los comandos tradicionales de Linux en un dispositivo Android, se debe instalar una herramienta de terceros llamada BusyBox.
