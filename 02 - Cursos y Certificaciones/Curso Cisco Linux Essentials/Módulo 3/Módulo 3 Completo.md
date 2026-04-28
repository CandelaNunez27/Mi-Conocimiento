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

Es una interfaz de entrada de texto que te permite darle instrucciones al sistema operativo, abarcando desde un comando simple de una sola palabra hasta scripts (secuencias de programación) muy complejos.

- **Cómo acceder a ella:**
    
    - En Modo Texto: Al iniciar sesión, te encuentras inmediatamente dentro de la consola.
    
    - En Modo Gráfico: Debes iniciar un shell gráfico, que es básicamente la misma consola de texto tradicional pero dentro de una ventana que puedes mover, maximizar o redimensionar. 

---

### 3.4 Virtualización y Cloud Computing

Dado que el modo multiusuario clásico de Linux tiene límites (un usuario puede consumir todos los recursos del sistema), la industria utiliza la virtualización.

**Virtualización** 
Es dividir un servidor físico potente en varios servidores virtuales totalmente independientes.

- Host (Anfitrión): El servidor físico real.

- Hipervisor: El software que reparte la CPU, RAM y disco.

- Invitados (Guests): Las máquinas virtuales (VMs). Funcionan aisladas y no saben que están virtualizadas.

- Ventajas: Ahorro gigante en hardware, energía y espacio. Es muy fácil crear y borrar máquinas de prueba.


**Cloud Computing (La Nube)**
Es llevar la virtualización a una escala global, utilizando centros de datos remotos de terceros.

- El Modelo: En lugar de comprar y mantener tus propios servidores físicos, los alquilas en la nube de forma virtual.

- Pago por uso: Solo pagas por los recursos exactos (Gigabytes, CPU) que consumes al mes.

- El Rey de la Nube: Linux es el motor absoluto; la inmensa mayoría de la infraestructura en la nube funciona sobre su kernel.

---

### 3.5 Utilizar Linux para el Trabajo

**Ofimática: LibreOffice (y OpenOffice)**

Es la suite principal que cubre las tres grandes necesidades de oficina. Es altamente compatible con formatos de Microsoft Office y permite exportar directamente a PDF

- Procesador de Textos (Writer): Para crear informes y memos. Soporta texto, imágenes, tablas y permite vincular datos desde una hoja de cálculo (para que los informes se actualicen automáticamente si cambian los números).

- Hoja de Cálculo (Calc): Para números, análisis de ventas y predicciones. No solo usa celdas; permite aplicar fórmulas matemáticas complejas y generar gráficos dinámicos.

- Presentaciones: Para crear diapositivas para exponer con texto, gráficos y videos.

- Extras: Permite el uso de extensiones, pudiendo integrarse, por ejemplo, con software Wiki para intranets empresariales.


**Navegadores Web**

- Firefox y Google Chrome: consideran a Linux un "ciudadano de primera clase". Esto significa que las versiones de Linux reciben las actualizaciones, nuevas funciones y parches de seguridad al mismo tiempo que Windows o Mac.

- Limitación externa: Históricamente, algunos complementos cerrados de terceros (como el antiguo Adobe Flash) podían tener problemas, ya que dependían del soporte de empresas externas con otras prioridades.

---

### 3.6 Proteger tu Equipo Linux

Dado que Linux no distingue entre un usuario sentado frente al teclado y uno conectado desde internet, la seguridad es un factor obligatorio. Se basa en tres medidas fundamentales:

**1. Gestión de Contraseñas**

La regla de oro es usar contraseñas fuertes (mínimo 10 caracteres, combinando mayúsculas, minúsculas, números y símbolos) y únicas para cada sitio o servicio.

- Herramienta clave: Para no tener que memorizar decenas de claves complejas, se recomienda usar un gestor como KeePassX. De esta forma, solo necesitas recordar la contraseña de inicio de sesión de tu equipo y la contraseña maestra de KeePassX.

**2. Actualizaciones Constantes**

Mantener el software al día es vital para cerrar brechas de seguridad. En distribuciones como Ubuntu, se puede configurar el sistema gráficamente para que busque actualizaciones diariamente. Las actualizaciones críticas (de seguridad) te pedirán instalarse de inmediato, mientras que el resto puede agruparse para instalarse semanalmente.


**3. Firewall (Cortafuegos)**

 Es un sistema que filtra el tráfico de red, bloqueando conexiones entrantes que no hayas solicitado tú mismo.

- iptables: Es el potente sistema de firewall que Linux trae integrado "bajo el capó" (se maneja mediante complejos comandos de texto).

- **gufw:** Es una interfaz gráfica (GUI) sencilla para el firewall de Ubuntu. Permite activar la protección con un solo clic y añadir excepciones fácilmente, sin tener que lidiar con la complejidad de `iptables`.

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
