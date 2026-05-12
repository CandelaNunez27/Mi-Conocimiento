
**Aula Virtual**: https://aulavirtualipap.mendoza.gov.ar/moodle/ (Usuario: 27464734568, Contraseña: 46473456)
# Fundamentos

## La Era On-Premise

Es el modelo tradicional donde la empresa es dueña de toda la tecnología. Se tendría que gestionar el hardware, con rigidez escalable y responsabilidad de mantenimiento.

## Virtualización 

El motor: Virtualización 
-  Hipervisor (VMM): Es la capa de software que separa los recursos físicos del sistema operativo. Permite ejecutar múltiple máquinas virtuales aisladas simultáneamente.
- Impacto: consolida servidores y reduce drásticamente los costos de infraestructura.

![274](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260415084103.png)

####  Tipo Hipervisores

- *Bare Metal*: Se instala directamente sobre hardware físico, para servidores y empresas.
	- VMware ESXi, Hyper-V, KVM.

 ![128](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260415085443.png)

- *Hosted*: Se instala como una app en el S.O anfitrión.
	- VirtualBox, Workstation.

 ![123](../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260415085455.png)

---

# Material de Clase

### 1. Introducción

En este Módulo 1 vamos a entender cómo pasamos de un servidor físico que hacía una sola tarea, al uso de virtualización.
La nube no apareció de la nada: para entenderla, tenemos que mirar cómo manejábamos —y seguimos manejando— los fierros en casa.

### Infraestructura On-Premise (Local)

Es el modelo tradicional donde la empresa es dueña de todo el "stack" tecnológico. Imagina una habitación llena de racks, cables y aire acondicionado a tope.

●       **Gestión de Hardware:** Tú eres responsable del ciclo de vida completo: compra, instalación, mantenimiento de energía, refrigeración y reparaciones.

●       **Desafío Principal:** La **infraestructura rígida**. Si necesitas más potencia, debes comprar un servidor físico, esperar a que llegue y configurarlo (proceso que puede tardar semanas).

Siguiendo a Cooper (2025) podemos pensar que, cuando se trata de gestionar software e infraestructura, las empresas a menudo enfrentan una elección crítica: soluciones locales o basadas en la nube. Los sistemas locales, o "on-prem", ofrecen ventajas únicas como el control total sobre los datos, seguridad mejorada y opciones de personalización, lo que los convierte en una opción preferida para muchas industrias. 

Vamos a explorar qué significa realmente "on-premises", profundizar en sus pros y contras, y ver cómo se compara con otras opciones como las soluciones fuera de las instalaciones y en la nube.

**¿Qué significa instalación local?**

On-premises (a menudo abreviado como "on-prem") se refiere a software e infraestructura alojados dentro de las instalaciones o centro de datos de una empresa. A diferencia de las soluciones basadas en la nube, los sistemas locales brindan a las empresas un control completo sobre sus datos, hardware y configuraciones de software. Esta configuración es ideal para organizaciones que priorizan la seguridad de los datos, requieren soluciones personalizadas o operan en industrias altamente reguladas donde el cumplimiento es crítico. 

Por ejemplo, las soluciones locales se utilizan comúnmente en industrias como la salud y las finanzas, donde el cumplimiento estricto de las leyes de protección de datos como HIPAA o RGPD es obligatorio. Al gestionar todo internamente, las empresas pueden asegurar que los datos permanezcan seguros y dentro de su jurisdicción. 

**¿Qué es el software local?**

El software local es aquel que se instala y ejecuta en servidores propios de la empresa, dentro de su infraestructura física, en lugar de estar alojado en la nube. La empresa es responsable de gestionar el software, los servidores y todo el mantenimiento asociado. Este enfoque ofrece un mayor control sobre los datos y la seguridad, pero a menudo requiere más recursos de TI para respaldarlo.

**Ejemplos de Software On-Premises** 

Las soluciones on-premises se utilizan ampliamente en diversas industrias e incluyen: 

1. **Servidores de archivos locales:** utilizados para almacenar y compartir archivos dentro de una organización. 
2. **Sistemas de planificación de recursos empresariales (ERP):** los sistemas ERP como SAP u Oracle a menudo se implementan localmente para integrar y gestionar los principales procesos de negocio y, al mismo tiempo, garantizar un control total sobre los datos confidenciales de la empresa. 
3. **Software de gestión de relaciones con el cliente (CRM):** muchas empresas todavía optan por software de CRM local, como Microsoft Dynamics, para personalizar los flujos de trabajo y mantener un control estricto sobre los datos de los clientes. 

Al mantener estos sistemas en el sitio, las empresas pueden garantizar la accesibilidad sin depender de conexiones a internet externas o proveedores de servicios de terceros. 

**Ejemplo:** Una universidad que mantiene sus propios servidores en el sótano para gestionar las notas de los alumnos. Si el servidor se rompe un domingo, alguien del equipo técnico debe ir físicamente a cambiar el disco.

### Virtualización: el corazón del Cloud

Antes, si tenías un servidor físico potente pero solo usabas el 10% de su capacidad, el otro 90% se desperdiciaba. La virtualización llegó para permitirnos ejecutar múltiples "computadoras virtuales" (VMs) dentro de una sola máquina física.

Para profundizar sobre este tema y los siguientes te invitamos a consultar esta fuente:

##### [¿Qué es la virtualización?](https://www.ibm.com/es-es/think/topics/virtualization)


**El Hipervisor (Hypervisor)**

Es la capa de software que hace posible la magia. Separa los recursos físicos (CPU, RAM, Disco) del sistema operativo.

Un hipervisor (o monitor de máquina virtual - VMM) es un software que permite a un único equipo físico (host) ejecutar múltiples máquinas virtuales (MV) aisladas, compartiendo recursos como CPU, memoria y almacenamiento. Actúa como capa de abstracción, facilitando la virtualización y la consolidación de servidores, lo cual es fundamental para la computación en la nube y la reducción de costos de infraestructura

Existen dos tipos:

1. **Tipo 1 (Bare Metal):** Se instala directamente sobre el hardware. Es el más eficiente y usado en centros de datos.

- _Ejemplos:_ VMware ESXi, Microsoft Hyper-V, KVM.

3. **Tipo 2 (Hosted):** Se instala como una aplicación sobre un sistema operativo (como Windows o Linux).

- _Ejemplos:_ Oracle VirtualBox, VMware Workstation.

Te dejamos un material para profundizar:

![](https://aulavirtualipap.mendoza.gov.ar/moodle/pluginfile.php/75589/mod_book/chapter/1364/video.jpg)  

  

**Optimización de recursos locales**

La virtualización permite:

● **Consolidación:** Meter 10 servidores virtuales en 1 físico.

● **Aislamiento:** Si una VM falla o tiene un virus, no afecta a las demás.

● **Elasticidad Inicial:** Clonar una máquina virtual es cuestión de clics, no de meses de compra.

Al decidir entre [soluciones basadas en la nube](https://www.splashtop.com/es/blog/what-is-cloud-computing) y sistemas on-premises, las empresas deben evaluar sus necesidades y analizar qué ofrece cada modelo.

A continuación, se presenta una comparación para ayudar a aclarar las diferencias clave: 

| Aspecto                 | En la nube                                                                                        | On-Premises                                                                                                   |
| ----------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- |
| Infraestructura         | Alojado en servidores de terceros; no se necesita hardware físico.                                | Requiere servidores internos y equipos de red.                                                                |
| Costos                  | Basado en suscripción con tarifas mensuales predecibles.                                          | Alta inversión inicial; potencialmente menores costos a largo plazo.                                          |
| Mantenimiento           | Gestionado por el proveedor (actualizaciones, parches, copias de seguridad).                      | Manejado por equipos internos de TI, requiriendo experiencia y recursos.                                      |
| Control de Datos        | Los datos son almacenados y gestionados por un proveedor externo.                                 | Control total sobre los datos, con almacenamiento en servidores locales.                                      |
| Seguridad               | El proveedor implementa la seguridad, pero existen riesgos de brechas o acceso no autorizado.     | Medidas de seguridad personalizadas adaptadas a las necesidades del negocio, pero requiere esfuerzo continuo. |
| Escalabilidad           | Altamente escalable; los recursos se pueden ajustar rápida y fácilmente.                          | Escalabilidad limitada; requiere hardware adicional y tiempo para la expansión.                               |
| Accesibilidad           | Accesible desde cualquier lugar con una conexión a internet.                                      | Limitado a la ubicación física o a una red segura a menos que se utilicen soluciones de Acceso remoto.        |
| Personalización         | Personalización limitada dependiendo de la plataforma y ofertas del proveedor.                    | Alto potencial de personalización para satisfacer necesidades específicas del negocio.                        |
| Cumplimiento            | El proveedor debe cumplir con los estándares regulatorios; las empresas tienen menos supervisión. | Más fácil de mantener el cumplimiento con regulaciones y políticas específicas de la industria.               |
| Tiempo de Configuración | Configuración rápida; los servicios están listos para desplegarse una vez suscritos.              | Configuración que consume mucho tiempo, incluyendo la instalación de hardware y la configuración de software. |

---

# Grabaciónde la Clase

**Clase Grabada**: https://drive.google.com/file/d/12GFY5a6z0tpkgzZ0pDZXv-5yjh55dHpK/view?usp=sharing