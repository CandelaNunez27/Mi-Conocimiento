# Teoría: Gestión de Configuración Avanzada Cierre modulo 3

# Fundamentos Arquitectura de Infraestructura

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806110030.png)

La idea de esto es dejar de conectarnos directamente a nuestros servidores, que no haya necesidad de conexión, sino que lo tengamos declarado en código, siendo arquitectura estructurado en còdigo.

# Fundamentos El antes

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806110449.png)

Antes conectarse a los servidores se necesitaba configurarlo manualmente para el acceso, permitir ssh, telnet o escritorios remotos, teniendo key de ssh o para remeto. Por ende si alguien entra a nuestra pc o por alguna razón acceden a nuestro certificado de ssh corremos el riesgo de que puedan acceder.

# Fundamentos El después

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806111152.png)

Hoy la idea es tener la arquitectura como código, que lo tenemos respaldado en un git. Quien tiene la llave segura la tiene git y no mi pc en local, entonces si me roban la pc no pasa nada. Ya no esta todo centralizado en un archivo  completo de configuración que si se perdia era un problema, ahora esta todo en recetas tipo yaml listas para usar en un lugar resguardado como git. Y lo que se busca es llegar a la Gestión de Configuración.

# Fundamentos Gestión de Configuración

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806111845.png)

Se busca llegar a este proceso, como la desplegas y la replicas, se menciona Auditoria de procesos que suele tener una empresa para tener gestionada el despliegue y poder replicarlo sin problemas. Para ello hay que tener documentación de estos procesos para los cambios o escalamientos que puedan ocurrir.


# Fundamentos ITIL

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806114007.png)

Son buenas practicas de nuestras empresa. Planificar objetivos, relevamiento de activos y servicios, gestión de cambios como nos manejamos ante ellos, Registros de estados y  Auditoria de seguridad


# Fundamentos Idempotencia

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806115101.png)

Idempotencia es algo que siempre va a dar el mismo resultado.  Contemplar los primeros inconvenientes de preparación (permisos, accesos, backend) que tienen que ser documentadas para que luego se hagan pasos metódicamente las veces que sea.

# Fundamentos Herramientas

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806225831.png)

Para esto nos sirve:
- **Terraform:** nos sirve para la arquitectura como código agnóstico al entorno donde lo despleguemos.  Se desplegaba y ansible ayudaba. Su alternativa en el mercado seria a chef más robusto. 
- **Ansible:** Nos construía los servicios y las acciones que queríamos tener en la arquitectura desplegada por terraform. Su alternativa en el mercado seria a puppet más robusto. 

Ejemplo descargamos de github o con git actions de manera automáticamente, el código de terraform, lo corremos y se despliega una arquitectura sin servicios( casa vacía) y luego con ansible le indicamos que configure como usuarios, servicios, etc (casa amueblada). 

# Fundamentos Puppet - Chef las otras Herramientas

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806230943.png)

- **Chef:** Es imperativo se le indica que tiene que hacer y cómo, para desarrolladores ya que el lenguaje que usa es el ruby. Su codigo eran como recetas. Usada para entornos elásticos, (ahora kubernetes puede usarse para entornos elásticos ).
- **Puppet:** Es declarativo se le explica que es lo que quiero obtener, para administradores de sistemas porque su lenguaje era propio DSL, parecido a yaml parecido a terraform. Su código era más manifiestos como yml. Usada para entornos escalables, (ahora se usa terraform porque es más fácil que puppet).

# AWS OpsWorks Engine

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260806234822.png)

AWS ofrece OpsWorks Engine que es un servicio para hacer la gestión de todo lo que es instancias de administración/configuración. Aca como tenemos instancias corriendo  chef y puppet se pueden sincrinizar con OpsWorks para que sea más centralizado en la nube. y con eso podemos dirigirlo a CI/CD.

# Cierre Estadio Ideal

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260807000007.png)

Se busca:
- Código de infraestructura
- Ese código tenerlo centralizado y respaldado. idempotente (siempre da un resultado idéntico)
- La gestión de configuración, o sea la documentación de como despegarlo y gestionarlo, la tenemos en una base de datos accesible y modificable. importante para la ahora que se hacen las auditorias.
- El motor usar la herramienta que queramos (terraform, ansible, puppit, chef.....)
- La escalabilidad se puede usar aws openWorks o Kubernetes o cual sea mi soluciona a la escalabilidad y modificación de la arquitectura.

La arquitectura deja de ser un hardware que se configura y se convierte en un software que se compila.







  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1FnLGOpA2MYRGe1gGxmwfjffXrANTFnUA/view
