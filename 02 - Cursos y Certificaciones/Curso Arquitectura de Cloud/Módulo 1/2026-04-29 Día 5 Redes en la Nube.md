**Páginas para virtualizar:**
https://killercoda.com/ terminal con laboratorios (Linux, grafana, ... ).
https://labex.io/ terminal con interfaz con laboratorios (Linux, cybersecurity, ....) dura una 1 hs y se va renovando.

# Fundamentos: VPN (Virtual Private Network)

Blindaje de Conexión: Crea un túnel cifrado entre tu dispositivo y un servidor remoto.
- Proteger Datos: Cifrado de información sensible.
- Trabajo Remoto: Acceso seguro a recursos internos.
- Evitar Rastreo: Oculta la Actividad e IP del ISP (proveedor).

# Fundamentos: Principios de la Nube

- Múlticuenta en un Tenant (empresas).
- Múltiples regiones en una cuenta para elegir virtualizar, cada una con distinta disposición de hardware.
- Múltiples zonas (datacenters) en una región, estarán entre ellas interconectadas para evitar que si un datacenter se prende fuego no se perderá los datos.

# Fundamentos: Red Virtual (Virtual Network Nube)

Se deben separar para mayor organización como departamentos en un edificio (*VPC Isolated Cloud Resources*) y se empezara a trabajar en el apartado de Red.
- Sección aislada de la nube donde tienes el control total del entorno.
- Control total sobre IPs, subredes y tablas de ruteo.

# Arquitectura: Pilares de Redes Cloud

Elementos vitales para que la infraestructura sea operativa.
- **CIDR**: Rango de direcciones IP.
- **Subnets**: Segmentación lógica.
- **Route Tables**: El "GPS" del tráfico.
- **Gateways**: Puertas de entrada y salida.

# Seguridad: Segmentación Crítica

Se debe separar lo público de lo privado, y tráfico interno controlado como vpn o cable para la comunicación entre ellas.
- Pública: Tráfico directo desde Internet, aloja lo que puede ser visible (Balancadores (distribuye el trafico de los varios servidores)y Servers Web).
- Privida: Accesible únicamente desde el interior de la red, aloja recursos críticos (Bases de datos RDS/SQL y Microservicios).

# Seguridad: Defensa en Profundidad

La seguridad se gestiona en capas concéntricas:
- **IAM**: Identidad como perímetro.
- **NACL**: Firewall a nivel Subred (Stateless).
- **Security Groups**: Firewall a nivel Instancia (Stateful)
![](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260506232858.png)

# Ejemplo de Lab Arquitectura en 2 capas

![](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260506233233.png)

---
# Material de Clase

### 1. Introducción

Empezamos a construir el "terreno" donde vivirán nuestras aplicaciones. Si la nube fuera una ciudad, las **VPC (AWS)** o **VNets (Azure)** serían las calles, los servicios de agua y las fronteras de seguridad.

#### El concepto de red virtual

Tanto en AWS como en Azure, el concepto base es una **Red Privada Virtual**. Es una sección aislada de la nube donde tú tienes el control total sobre el entorno de red.

Siguiendo a Azure (2026) podemos indicar que una red privada virtual (VPN) crea una conexión cifrada y segura entre tu dispositivo y un servidor remoto a través de internet. Al ocultar tu dirección IP y cifrar el tráfico de datos, protege la privacidad en línea, permite acceder a contenido restringido y asegura la información personal en redes Wi-Fi públicas. 

Estas son algunas razones comunes por las que podrías usar una VPN:

- **Proteger datos:** Los datos confidenciales, como los correos electrónicos profesionales, la información de pago y el etiquetado de ubicación, se transmiten constantemente en línea. Esta información es rastreable y fácil de aprovechar, especialmente en una red pública, donde cualquier persona que tenga acceso a la red puede acceder a los datos personales. Una conexión VPN cifra estos datos en código y los representa como ilegibles para cualquier persona sin una clave de cifrado. De este modo, se oculta la actividad de exploración para que nadie más pueda verla.

- **Trabajar desde casa:** En la actualidad, el trabajo remoto está más extendido que nunca. Con una VPN, quienes trabajan desde casa pueden acceder a los recursos de la empresa a través de una conexión privada desde cualquier lugar, siempre y cuando tengan acceso a Internet. Esto proporciona a los empleados una mayor flexibilidad, a la vez que garantiza que los datos de la empresa permanecen protegidos, incluso en una red Wi-Fi pública.

- **Acceder a contenido regional, o trasmitirlo, desde cualquier lugar:** Algunos sitios y servicios restringen su contenido multimedia en función de la ubicación geográfica, lo que supone que puede no tener acceso a determinados tipos de contenido. Una VPN oculta o suplanta la ubicación del servidor local para que aparezca como si estuviera en otro lugar (por ejemplo, en otro país).

- **Omitir el censo y la vigilancia:** Es posible que algunas regiones no tengan acceso a determinados sitios o servicios debido a restricciones gubernamentales, censo o vigilancia. La suplantación de ubicación ofrece a estos usuarios la capacidad de eludir firewalls, ver sitios web bloqueados y moverse libremente por Internet.

- **Evitar el proveedor de acceso a Internet (ISP) y el rastreo de terceros:** Los proveedores de servicios de Internet o ISP registran y realizan un seguimiento del historial de exploración a través de la dirección IP única del dispositivo. Esta información podría venderse a anunciantes de terceros, proporcionarse al gobierno o dejar al usuario vulnerable ante un riesgo de seguridad. Al enrutar a un servidor VPN remoto, en lugar de a los servidores del ISP, una VPN enmascara la dirección IP, impide el seguimiento del ISP y mantiene los datos personales privados.

#### Tipos comunes de VPN:

| Nombre                                                              | Tipo                      | Método de conexión                                                                             | Caso de uso                                                                                                                                                                                                                       |
| ------------------------------------------------------------------- | ------------------------- | ---------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| VPN de acceso remoto (también conocida como VPN de cliente a sitio) | Página principal          | Conexión a una red privada o a un servidor de terceros a través de SSL/TSL                     | Para los trabajadores remotos que necesitan acceder a los archivos y recursos de la empresa a través de una conexión privada, o para los usuarios que desean explorar la red pública de Internet a través de una conexión cifrada |
| VPN de sitio a sitio                                                | Privado                   | La red se conecta a otra red a través de LAN, WAN                                              | Para organizaciones de gran tamaño que necesitan vincular sus redes internas entre varios sitios en distintas ubicaciones, al tiempo que mantienen una conexión segura                                                            |
| Aplicaciones de VPN                                                 | Para dispositivos móviles | Conexión a una red privada a través de una aplicación VPN en un dispositivo móvil o smartphone | Para los usuarios móviles que deseen aprovechar las ventajas de una VPN mientras se desplazan o mientras experimentan una conexión a Internet inestable                                                                           |

#### VPN de acceso remoto (también conocida como VPN de cliente a sitio)

Uno de los tipos de VPN más usados, una VPN de acceso remoto, ofrece a los usuarios fuera del sitio la capacidad de conectarse a la red de una organización, o a un servidor remoto, desde el dispositivo personal. Esto se puede lograr escribiendo las credenciales de autenticación a través de una página de inicio de sesión, que le autoriza a realizar la conexión a través del explorador web.

Los usuarios pueden conectarse a la VPN de acceso remoto mediante un cliente o aplicación instalada en su dispositivo, que también se conecta a una red o servidor después de escribir sus credenciales. Un cliente proporciona a sus usuarios una interfaz sencilla con la que trabajar, información de conectividad y la capacidad de alternar entre las distintas características de la VPN.

Una VPN de acceso remoto se puede usar tanto para uso profesional como personal, por lo que es una de las formas más comunes de VPN. Ofrece a los trabajadores remotos la capacidad de acceder a los archivos y recursos de la empresa sin tener que estar en la oficina, y protege los datos privados de las empresas remotas para que permanezcan privados. En cuanto a los usuarios individuales que simplemente desean explorar la red pública de Internet con mayor autonomía y anonimato, una VPN de acceso remoto es integral para evitar bloqueos de contenido, firewalls y seguimiento del ISP.

#### VPN de sitio a sitio

Las grandes organizaciones que necesitan una solución personalizada más sólida pueden optar por VPN de sitio a sitio. Una VPN de sitio a sitio es una red interna privada formada por varias redes dentro de una organización, que están conectadas entre sí a redes de área local (LAN) a través de la red pública de Internet. Esta configuración permite a los usuarios de dos redes independientes, tanto dentro como adyacentes a la organización, compartir recursos entre sí, a la vez que limita el acceso total a todos los recursos, lo que garantiza que la comunicación dentro de la empresa siga siendo lo más privada y segura posible. Debido a la escala y complejidad de las VPN de sitio a sitio, este tipo de conexión es más adecuado para empresas de nivel empresarial con departamentos en varias ubicaciones.

Dentro de las VPN de sitio a sitio, hay dos tipos de red:

**Intranet**

Una VPN de sitio a sitio de intranet vincula varios sitios de la misma organización mediante LAN. Esto resulta útil cuando varios departamentos de varias ubicaciones necesitan colaborar entre sí dentro de una red privada y cerrada. A través de una conexión de sitio a sitio, estos departamentos pueden intercambiar recursos de forma segura y eficaz entre sí.

**Extranet**

Una VPN de sitio a sitio de extranet vincula varios sitios de diferentes organizaciones mediante LAN. Una organización que colabora con frecuencia con proveedores, socios o proveedores empresariales de terceros puede necesitar la capacidad de formar esta red. Las organizaciones también pueden personalizar el ámbito de acceso entre cada red, de modo que solo se comparten algunos recursos, mientras que otros permanecen privados.

#### VPN para dispositivos móviles

Aunque los proveedores de VPN de larga duración suelen atender a los usuarios de escritorio, los smartphones han provocado un enorme aumento en el crecimiento de las VPN para dispositivos móviles; y por un buen motivo. Para los usuarios de smartphones que buscan mayor seguridad y protección mientras se desplazan, una VPN móvil es una necesidad.

Las VPN móviles no solo proporcionan las ventajas de una VPN tradicional, sino que también siguen protegiendo los datos cuando la conectividad a Internet es puntual o inestable, o al alternar entre datos móviles y Wi-Fi. Mientras la aplicación se esté ejecutando, la conexión VPN permanecerá segura y el dispositivo permanecerá protegido. Debido a la flexibilidad, una VPN móvil es ideal para los usuarios que viajan o para aquellos que no tienen acceso a una conexión a Internet confiable.

#### Componentes fundamentales

Para que una red funcione, necesitamos definir cuatro elementos clave:

1. Rango de direcciones IP (CIDR): Definimos cuántas IPs tendrá nuestra red.

- _Ejemplo:_ 10.0.0.0/16 (65,536 direcciones).

3. Subredes (Subnets): Dividimos la red grande en pedazos más pequeños para organizar recursos.
4. Tablas de Enrutamiento (Route Tables): El "GPS" que le dice al tráfico hacia dónde ir.
5. Gateways (Puertas de Enlace):

- Internet Gateway (AWS) / Azure Gateway: Para que la red tenga salida a internet.
- NAT Gateway: Para que las bases de datos internas descarguen actualizaciones sin ser visibles desde afuera.

Para profundizar te dejamos la siguiente fuente:
 [¿Qué es una red privada virtual o VPN?](https://azure.microsoft.com/es-es/resources/cloud-computing-dictionary/what-is-vpn)

  

#### Segmentación de red: pública vs. privada

Este es el concepto más importante de la semana. **Nunca** debes poner una base de datos en una subred pública.

| Tipo de Subred | Propósito                     | Ejemplo de Recurso                        |
| -------------- | ----------------------------- | ----------------------------------------- |
| Pública        | Accesible desde internet.     | Balanceadores de carga, Servidores Web.   |
| Privada        | Aislada, sólo acceso interno. | Bases de Datos (RDS/SQL), Microservicios. |

#### Conectividad y seguridad (El "muro")

La seguridad y conectividad en la nube ("el muro") se basa en un modelo de responsabilidad compartida, donde proveedores como [AWS](https://www.google.com/url?sa=i&source=web&rct=j&url=https://aws.plainenglish.io.en2es.search.translate.goog/the-5-pillars-of-cloud-computing-essentials-explained-8eaebdb20a45&ved=2ahUKEwifvrz-zPWSAxVOHLkGHQwZIJQQy_kOegQIARAB&opi=89978449&cd&psig=AOvVaw0e-atvrRXuTvWr2_sgcxIM&ust=1772141853179000) protegen la infraestructura, mientras el usuario asegura datos y accesos. El "muro" moderno ya no es solo perimetral; se centra en la identidad (IAM), [cifrado](https://www.google.com/search?q=cifrado&client=opera-gx&hs=nr6&sca_esv=b7a78c7db20616cf&ei=dmufaZjNFNLa5OUPlL2LsAM&biw=1325&bih=620&ved=2ahUKEwifvrz-zPWSAxVOHLkGHQwZIJQQgK4QegQIARAC&uact=5&oq=Conectividad+y+seguridad+%28El+%22muro%22%29+en+la+nue+%28cloud%29&gs_lp=Egxnd3Mtd2l6LXNlcnAiNkNvbmVjdGl2aWRhZCB5IHNlZ3VyaWRhZCAoRWwgIm11cm8iKSBlbiBsYSBudWUgKGNsb3VkKTIFECEYnwVIhl1QiQhY7lVwA3gBkAEAmAGcAaABtg-qAQQ1LjEzuAEDyAEA-AEBmAIVoAKfEsICChAAGEcY1gQYsAPCAgUQIRigAcICBRAAGO8FwgIIEAAYgAQYogSYAwCIBgGQBgiSBwQzLjE4oAeBRLIHBDAuMTi4B-8RwgcGMi00LjE3yAfTAYAIAQ&sclient=gws-wiz-serp) y [Confianza Cero](https://www.google.com/search?q=Confianza+Cero&client=opera-gx&hs=nr6&sca_esv=b7a78c7db20616cf&ei=dmufaZjNFNLa5OUPlL2LsAM&biw=1325&bih=620&ved=2ahUKEwifvrz-zPWSAxVOHLkGHQwZIJQQgK4QegQIARAD&uact=5&oq=Conectividad+y+seguridad+%28El+%22muro%22%29+en+la+nue+%28cloud%29&gs_lp=Egxnd3Mtd2l6LXNlcnAiNkNvbmVjdGl2aWRhZCB5IHNlZ3VyaWRhZCAoRWwgIm11cm8iKSBlbiBsYSBudWUgKGNsb3VkKTIFECEYnwVIhl1QiQhY7lVwA3gBkAEAmAGcAaABtg-qAQQ1LjEzuAEDyAEA-AEBmAIVoAKfEsICChAAGEcY1gQYsAPCAgUQIRigAcICBRAAGO8FwgIIEAAYgAQYogSYAwCIBgGQBgiSBwQzLjE4oAeBRLIHBDAuMTi4B-8RwgcGMi00LjE3yAfTAYAIAQ&sclient=gws-wiz-serp) para proteger recursos en entornos híbridos y multinube. 

**Componentes claves del "muro" de seguridad y conectividad:**

**Identidad y acceso (IAM):** La gestión de identidades es el nuevo "muro" principal, crucial para controlar quién accede a los recursos.

**Seguridad de red (El muro perimetral):** Uso de firewalls, sistemas de detección de intrusiones (IDS) y redes privadas virtuales (VPN) para proteger el tráfico.

**Conectividad segura:** Plataformas unificadas que permiten conexiones rápidas y seguras, incluyendo [Secure Web Gateways (SWG)](https://www.google.com/url?sa=i&source=web&rct=j&url=https://www.zscaler.com/mx/resources/security-terms-glossary/what-is-secure-web-gateway&ved=2ahUKEwifvrz-zPWSAxVOHLkGHQwZIJQQy_kOegQIAxAD&opi=89978449&cd&psig=AOvVaw0e-atvrRXuTvWr2_sgcxIM&ust=1772141853179000) para filtrar accesos maliciosos.

**Defensa en profundidad:** Implementación de cifrado de datos (en reposo y tránsito), parches automatizados y monitorización continua.

**Modelo de responsabilidad compartida:** Los proveedores gestionan la seguridad _de_ la nube (física, hardware), y los usuarios gestionan la seguridad _en_ la nube (datos, configuración, aplicaciones). 

La implementación de una arquitectura de [Confianza Cero](https://www.google.com/search?q=Confianza+Cero&client=opera-gx&hs=nr6&sca_esv=b7a78c7db20616cf&ei=dmufaZjNFNLa5OUPlL2LsAM&biw=1325&bih=620&ved=2ahUKEwifvrz-zPWSAxVOHLkGHQwZIJQQgK4QegQIBBAB&uact=5&oq=Conectividad+y+seguridad+%28El+%22muro%22%29+en+la+nue+%28cloud%29&gs_lp=Egxnd3Mtd2l6LXNlcnAiNkNvbmVjdGl2aWRhZCB5IHNlZ3VyaWRhZCAoRWwgIm11cm8iKSBlbiBsYSBudWUgKGNsb3VkKTIFECEYnwVIhl1QiQhY7lVwA3gBkAEAmAGcAaABtg-qAQQ1LjEzuAEDyAEA-AEBmAIVoAKfEsICChAAGEcY1gQYsAPCAgUQIRigAcICBRAAGO8FwgIIEAAYgAQYogSYAwCIBgGQBgiSBwQzLjE4oAeBRLIHBDAuMTi4B-8RwgcGMi00LjE3yAfTAYAIAQ&sclient=gws-wiz-serp&mstk=AUtExfAg3Yswa6dW9etuepsh7AqW2R_pvjLnfPXXiB5UjuGfuwx92Eq4TPzoJrV6whEhZDB3HQ2eUFmK-j0WEEkntmqorlyMFWe5WElNokG5duewg1RJRafHv2wxpL6FoTpY5VU&csui=3) (Zero Trust) y la visibilidad unificada de la postura de seguridad (CSPM) son prácticas esenciales para reducir el riesgo en el entorno de la nube

En la nube, la seguridad de red se maneja en capas (defensa en profundidad):

●       Grupos de Seguridad (Security Groups / NSG): Actúan como un firewall a nivel de instancia/tarjeta de red. Son "Stateful" (si dejas entrar, dejas salir).

●       NACL (Network ACL - Solo en AWS): Un firewall a nivel de subred. Es la primera línea de defensa "Stateless".

**_Ejemplos_**

_Caso A: Arquitectura de 2 Capas (AWS)_

_Imagina que tienes una web en WordPress._

_●       Subred Pública: Aloja la instancia EC2 con el servidor web. Tiene un Internet Gateway._

_●       Subred Privada: Aloja la base de datos MySQL. Solo acepta tráfico que venga desde la IP del servidor web (Subred Pública)._

_Caso B: Azure VNet Peering_

_Si tu empresa compra otra compañía, puedes conectar sus redes usando VNet Peering. Esto permite que las máquinas virtuales de ambas redes se comuniquen usando IPs privadas, como si estuvieran en la misma red local, sin pasar por el internet público._

---

# Grabación de Clase

https://drive.google.com/file/d/15Ck5ZFR4TvNEgqXuhTc0Vh2UQ4SfeUXl/view?usp=sharing 
