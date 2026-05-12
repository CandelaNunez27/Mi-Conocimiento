# ¿Cómo funciona la nube?
Se puede crear su propia nube. Necesitan corriente, refrigeración, baterías, conexión de red estable, ciberseguridad, equipos potentes para configuraciones de red contemplando la seguridad de firmware, poder de computo, gran capacidad para almacenar base de datos. 

![Pasted image 20260422083337](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260422083337.png)

# Responsabilidades del usuario o proveedor
**On-Premise:** Todo mío.

**IaaS (Infraestructura de Servicio):** Te dejo limpiamente el hardware y red para que uno pueda usar cualquier hipervisor y S.O. que quiera. Vas a tener que administrar todo el S.O. 

![Pasted image 20260422085556](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260422085556.png)

**PaaS (Plataforma de Servicio):** Te deja la computadora lista para usar sin tener que administrar, no tendrás que mantener la seguridad, las actualización de S.O. Usas las aplicaciones directamente.

![Pasted image 20260422085724](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260422085724.png)

**SaaS (Software de Servicio):** Por ejemplo App Google Drive, usas una cuenta y vos controlas tus datos. No actualizas el software.

![Pasted image 20260422085912](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260422085912.png)


![Pasted image 20260422083736](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260422083736.png)
![Pasted image 20260422090053](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260422090053.png)

# Modelos de despliegue

**Nube Pública:** Muchos servicios compartidos fáciles de escalabilidad, aunque menos control. Básicamente consiste en que consumo a lo que me suscribo en cualquier lado.
**Nube Privada:** Conectarse a una infraestructura privada de un datacenter particular de uso únicamente para mí.  Es mayor en costo monetario.
**Nube Hibrida:** Se suele usar para cuando se trata de migrar a la nube

![Pasted image 20260422091704](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260422091704.png)

# Seguridad: Responsabilidad Compartida
El proveedor se asegura de Hardware, red, región (Suelen desatenderse en apartados legales).

El cliente se asegura de los datos, de IAM, Cifrado, no hay que ser un punto de inseguridad ya que la mayoría de fallas suelen ser por malas configuraciones del usuario. Si perdiste datos, si dejaste puertos abiertos o contraseñas débiles es tu responsabilidad.

---

# Material de Clase

### 1. Introducción

En esta clase vamos a meternos en cómo funciona la nube por dentro. Si en la Semana 1 vimos los “fierros” y la virtualización, hoy vamos a analizar quién se hace cargo de qué dentro de la infraestructura


#### Modelos de servicio: La pirámide de responsabilidad

La diferencia crítica entre estos modelos no es solo tecnológica, sino de gestión y control. Se suele explicar con la analogía de "La pizza como servicio", pero aquí lo veremos desde la ingeniería de sistemas.


###### A. IaaS (Infrastructure as a Service) - "Tú lo construyes"**

Es el nivel más bajo de abstracción. El proveedor te da los recursos de computación básicos (servidores virtuales, red, almacenamiento).

●       **Qué gestionas tú:** Sistema Operativo (parches, actualizaciones), Middleware, Tiempo de ejecución (Runtime), Datos y Aplicaciones.

●       **Qué gestiona el proveedor:** El hardware físico, la virtualización, la refrigeración y la conectividad de red física.

●       **Ejemplo:** Un servidor **EC2 de AWS** o una **VM en Azure**. Tú eliges si instalas Linux o Windows y eres responsable de que sea seguro.

###### B. PaaS (Platform as a Service) - "Tú solo programas"

Diseñado para desarrolladores. El proveedor abstrae el sistema operativo y el hardware. Tú solo entregas el código.

●       **Qué gestionas tú:** Solo la aplicación y sus datos.

●       **Qué gestiona el proveedor:** Todo lo de IaaS + el Sistema Operativo, el servidor web (Apache, Nginx) y el entorno de ejecución (Java, Python, Node.js).

●       **Ejemplo: Google App Engine o Heroku.** No tenés que preocuparte por actualizar el sistema operativo o el kernel; solo por que tu código funcione correctamente.

###### C. SaaS (Software as a Service) - "Tú solo consumes"

El modelo de consumo final. No ves servidores, ni código, ni bases de datos.

●       **Qué gestionas tú:** Solo configuraciones básicas de usuario.

●       **Qué gestiona el proveedor:** Absolutamente todo el stack tecnológico.

●       **Ejemplo:** **Google Workspace (Gmail, Drive)** o **Salesforce**.

###### Análisis de diferencias críticas: cuadro comparativo entre ambos modelos.

| Característica   | IaaS                                           | PaaS                        | SaaS                       |
| ---------------- | ---------------------------------------------- | --------------------------- | -------------------------- |
| Control          | Máximo                                         | Medio                       | Mínimo                     |
| Complejidad      | Alta                                           | Media                       | Baja                       |
| Público objetivo | Administradores de Sistemas / Cloud Architects | Desarrolladores de Software | Usuarios finales / Negocio |
| Mantenimiento    | Alto (actualizar SO)                           | Bajo (solo código)          | Nulo                       |

#### Modelos de despliegue:

**Antes de empezar pensemos ¿Dónde están mis datos? ....**

![](https://youtu.be/tVbniAqMEPs?si=FXrwqZqjLnj7Hzve)  

  
###### A. Nube Pública (Public Cloud)

Los servicios se ofrecen a través de la internet pública y son compartidos por múltiples organizaciones (multi-tenancy).

●       **Ventaja:** Escalabilidad infinita y pago por uso (OPEX).

●       **Desventaja:** Menor control sobre la ubicación física exacta de los datos.

●       **Líderes:** AWS, Azure, Google Cloud (GCP).

###### B. Nube Privada (Private Cloud)

La infraestructura es dedicada exclusivamente a una sola organización. Puede estar físicamente en el data center de la empresa o alojada por un tercero.

●       **Uso crítico:** Gobiernos, bancos o industrias con regulaciones de privacidad extremas.

●       **Tecnología clave:** OpenStack o VMware vCloud.

###### C. Nube Híbrida (Hybrid Cloud)

Es la combinación de ambas, conectadas mediante tecnología que permite que los datos y las aplicaciones se compartan entre ellas.

●       Escenario común: Una empresa mantiene sus bases de datos sensibles en una Nube Privada por seguridad, pero despliega su aplicación web en la Nube Pública para manejar picos de tráfico.

La informática en la nube híbrida combina informática de nube pública con la infraestructura local o la nube privada en un entorno integrado. Esto permite que las aplicaciones, los datos y las cargas de trabajo se compartan entre las dos, lo que lleva a un mayor rendimiento.

**¿Cómo funciona la nube híbrida?**

La informática en la nube híbrida combina entornos de nube pública y privada, lo que permite compartir aplicaciones, servicios y cargas de trabajo entre ellos. Al adoptar el modelo híbrido, las organizaciones pueden elegir dónde ejecutar sus cargas de trabajo según sus necesidades comerciales, lo que resulta en mayor flexibilidad, escalabilidad y eficiencia de costos, todo mientras mantienen el control sobre recursos específicos.

Con la nube híbrida, las organizaciones pueden experimentar lo mejor de ambos mundos. Pueden confiar en la nube pública de terceros para escalar y optimizar sus recursos mientras siguen utilizando la nube privada local para gestionar cargas de trabajo más críticas que pueden requerir mayores niveles de seguridad o control.

Los entornos de nube híbrida se gestionan típicamente a través de una plataforma de administración de nube centralizada, que brinda a los usuarios visibilidad total sobre toda su infraestructura. Las herramientas de administración de nube permiten integrar y gestionar recursos entre ambos entornos de forma unificada, generalmente a través de APIs y herramientas de automatización y orquestación.

**¿Qué ventajas tiene la nube híbrida?**

Vamos a ver por qué muchas organizaciones eligen la nube híbrida para tener mayor flexibilidad y control.

**Flexibilidad:** Al adoptar el modelo híbrido, las empresas tienen la flexibilidad de elegir dónde ejecutar sus cargas de trabajo según sus necesidades específicas de seguridad o rendimiento.

**Rentabilidad:** La nube híbrida permite usar recursos de nube pública cuando se necesitan, manteniendo infraestructura privada para cargas específicas. Esto ayuda a optimizar costos.

**Escalabilidad:** La nube híbrida puede escalar y reducir verticalmente las cargas de trabajo durante los picos de demanda, todo ello sin tener que sobrecargar la infraestructura local adicional.

**Continuidad empresarial:** Al proporcionar copias de seguridad y recuperación ante desastres sin problemas entre nubes privadas y públicas, la nube híbrida permite a las organizaciones prepararse para la continuidad empresarial.

**Rendimiento mejorado:** Con su capacidad para optimizar la asignación de recursos entre nubes privadas y públicas, la informática en la nube híbrida es ideal para mejorar el rendimiento y la capacidad de respuesta de las aplicaciones.

**Seguridad y cumplimiento:** Al utilizar la nube privada para administrar datos sensibles, las organizaciones pueden cumplir con las regulaciones de datos y proteger mejor sus cargas de trabajo críticas.

**Innovación y agilidad:** La informática en la nube híbrida facilita un despliegue más rápido y el acceso a nuevas tecnologías, proporcionando a las empresas una ventaja competitiva.

**_Punto clave:_**

_La **Nube Híbrida** no es solo "usar dos nubes", requiere una conexión técnica sólida (como un túnel VPN o Direct Connect)._

  

#### Responsabilidad Compartida:

En la nube, la seguridad de la infraestructura es del proveedor, pero la seguridad en la nube (tus datos) es tuya.

En el mundo de la nube, el Modelo de Responsabilidad Compartida es la "letra chica" que evita desastres de seguridad y costos inesperados.

La regla de oro es simple: El proveedor (CSP) es responsable de la seguridad _de_ la nube, y tú eres responsable de la seguridad _en_ la nube**.**

###### El espectro de responsabilidad según el modelo

Dependiendo de qué tan "administrado" sea el servicio que contrates, tu carga de trabajo cambia. Aquí es donde muchos fallan al asumir que, por estar en la nube, "todo está respaldado y protegido".

| Capa de Tecnología       | On-Premise | IaaS (Infraestructura) | PaaS (Plataforma) | SaaS (Software) |
| ------------------------ | ---------- | ---------------------- | ----------------- | --------------- |
| Datos y Contenido        | Tú         | Tú                     | Tú                | Tú              |
| Identidad y Acceso (IAM) | Tú         | Tú                     | Tú                | Tú              |
| Aplicaciones             | Tú         | Tú                     | Tú                | Proveedor       |
| Sistema Operativo (OS)   | Tú         | Tú                     | Proveedor         | Proveedor       |
| Red y Virtualización     | Tú         | Proveedor              | Proveedor         | Proveedor       |
| Infraestructura Física   | Tú         | Proveedor              | Proveedor         | Proveedor       |

###### Los 3 puntos críticos que suelen olvidarse

**1. Los Datos siempre son tuyos**

No importa si usas AWS, Azure o Google Cloud; el proveedor nunca se hace responsable si borras accidentalmente tu base de datos o si un empleado filtra información sensible. La clasificación y el cifrado de los datos son 100% tu tarea.

**2. Configuración de Red (Firewalls)**

En un modelo IaaS (como una instancia EC2), el proveedor te da las herramientas (Security Groups), pero si dejas el puerto 22 (SSH) abierto a todo el mundo (0.0.0.0/0), la brecha de seguridad es tu responsabilidad, no del proveedor.

**3. Gestión de Identidades (IAM)**

El proveedor garantiza que nadie entrará físicamente al servidor, pero si tu contraseña es Admin123 y no tienes autenticación de dos factores (MFA), el acceso no autorizado es responsabilidad del cliente.  

_**Dato clave:** La mayoría de las fallas de seguridad en la nube no son por vulnerabilidades del proveedor, sino por **malas configuraciones** del usuario._


**¿Cómo saber si estás cumpliendo tu parte?**

Para no dejar cabos sueltos, te sugiero aplicar el principio de Mínimo Privilegio:

●       Nadie debe tener más acceso del estrictamente necesario.

●       Automatiza los respaldos (el proveedor te da la herramienta, tú debes activarla).

●       Monitorea los logs de acceso constantemente.

---

# Grabación de la Clase

**Clase Grabada**: https://drive.google.com/file/d/1mduQbK87IXD8soMmEU4a-bpMUIr10OQP/view?usp=sharing