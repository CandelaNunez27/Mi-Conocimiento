# Teoría: Gestión de Identidades (IAM)

# Introducción El ID el nuevo perímetro

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260818012304.png)

El ID es para detectar quién es alguien o que proceso es para permitir acciones a las aplicaciones, software o quién lo necesite.

# Fundamentos Antes - Ahora

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260818012628.png)

Antes. usualmente cuando todo era on premise, teníamos la primera barrera era la red, no permitiendo conexión al exterior desde un firewall pero adentro no tenía una gestión de IDs porque si ingresaba alguna vulnerabilidad se haría dueño de todo pasando la barrera. 
Ahora se busca primero identificar para permitir acceso o modificación y cada uno de los usuarios estarán aislados en ciertos permisos. El administrador de identidades le asignara puntualmente sobre algún servicio limitadamente.

# Fundamentos Identidad vs Privilegios

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260818093019.png)

- AurthN : sirve para identificar quién es, tratando de probar que seas quien dice ser, esto se verifica con Contraseñas, MFA, Biometría, Claves Públicas 

- AuthZ : sirve para permitir o acceso a realizar acciones, tratando de probar que tengas un rango para realizarlo, esto se verifica con RBAC, ABAC, Politicas, OAuth.

Siempre es como una cadena de primero identificate para luego date permisos.

# Fundamentos Métodos de ID

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260818094616.png)

Para validar identidad el más común es la contraseña aunque pueda ser vulnerada por contraseñas débiles, robos o ataques de fuerza bruta. Segundo los Certificados de Clave Pública que tiene un cifrado asimétrico, es como ssh trabajando con encriptaciones. Y la última la más fiable, la biometría que es que no haya unos caracteres digitalizados sino que directamente el usuario sea la clave con su cara o huella.

# Fundamentos MFA (Múltiple Factor de Autenticación)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260818095451.png)

Si se recibe un ataque tiene varias barreras gracias al MFA que contiene una contraseña, luego pasa a una segunda autenticación con tokens, o ya pasar a datos biométricos. O sea consiste en no solo quedarse con la contraseña sino validar con un segundo paso si realmente sos vos y no te robaron la contraseña.

# Fundamentos Reglas AuthZ

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260818101714.png)

Siendo ya un usuarios Verificado que reglas podes tener:
- Permisos basado en Roles (RBAC): Se puede dar reglas / permisos según el rol o cargo del usuario, o sea se me permite todas acciones según un estándar de lo que debería hacer.
  
- Permisos basados en Atributos (ABAC): Se puede dar reglas / permisos según atributos, usualmente asociada con la anterior donde cada rol tiene permisos distintos con atributos de accesos distintos, pero usualmente en rol es como un estándar y esto puede ser más dinámico y flexible.
  
- Permisos Globales: Se puede dar reglas / permisos que globalmente se suele aplicar a todos los usuarios estrictamente siendo como se dice la policy, hay excepciones con algunos usuarios como el administrador de sistema tiene que tener una policy aparte porque se le permite borrar.
  
- OAuth: es el que te permite acceder a los servicios luego de haberte identificado una vez. Ejemplo si me logueo en una cuenta de gmail en google ya se me abra logueado en el resto de aplicaciones asociadas.

# Fundamentos Mínimos Privilegio (POLP)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260819003847.png)

Si es vulnerable alguna cuenta es importante que el usuario tenga el menos privilegio posible y ya en distintos casos de va desbloqueando de a pocos, aunque sea medio tedioso para eso viene el siguiente punto

# Fundamentos Administración IAM

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260819004026.png)

Acá podemos ver que esta segmentado en usuarios, grupos y roles:
- usuario: la persona que se identifica, una persona en expecifico con un rol, ej Juan el desarrollador
- grupos: pero si tengo muchos como juan el desarrollador me conviene colocarlos en un grupo Los Desarrolladores con el privilegio de ver el código fuente, pero el grupo financias no lo debería ver
- Rol: es cuando ya se identifico como juan el desarrollador, entro al grupo de desarrolladores y por ende ahora ya tiene el rol que le permite trabajar, por eso l



# Práctica: sawkl
### Preparación

1. sdssdf:
	sdsld

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1a2eFcawGdo8jmCxbPSDVeZh5wkO0Fpfm/view
