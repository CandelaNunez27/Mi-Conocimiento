# Teoría: Gestión de configuraciones Ansible

# Fundamentos Ansible

**Ansible:** (Automatización Sistémica) desmitificando Ansible de la configuracion manual a la intraestructura como documentacion legible. Se ve mucho en infraestructuras hibridas, busca que las configuraciones no sean manuales sino por código automatizadas. Automatiza los despliegues masivos con configuraciones yaml o json, instala y orquesta servicios automaticamente, 

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260622173146.png)

# Fundamentos Diferencia y complemento

Para teerraform es trabajo grueso y ansible trabaja en fino. Terraform podes crear y cargar los recursos en intraestructura y servicios, aunque se pueda hacer configuraciones pero se le complica las configuraciones más avanzadas como indicarle que instale un antiviris (tendria que ir descargarlo, instalarlo, configurarlo. seria mucho trabajo y perderia si gran potencial de rapidez). 
Pero Ansible complementa siendo el ejecutor de configuraciones (s.o listo, configurar, instalar) solo necesitando la ip de la architectura donde trabajara, y en cambio crear infraestructura no es lo ideal hacerlo con ansible ya que no se expecializa en eso.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260622173456.png)

# Fundamentos Ventajas

Arquitectura sin agentes, no hace falta instalar ningún agentes en las maquinas y el controlador es unidireccional conectando con ssh o modelo push en windows. También se podria configurar routers o switch configurables que entiendan Python.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260622175430.png)

# Fundamentos Idempotencia

Es desplegar uno o miles debe ser la misma con el mismo archivo de configuración, como multiplicar con cero siempre es cero. O sea que si desplegamos siemple el mismo archivo de configuración siempre desplegara iguales.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260622175607.png)

# Fundamentos Los pilares de Ansible

Ansible es open source y de código abierto, sin necesidad de gastar recursos instalando agentes, configuración simple con curva de aprendizaje fácil si ya estas familiarizado  con los archivos yaml/json, se puede complementar con APIs como API de aws permitiendo configuraciones de servidores en nube, idempotencia para deslegar n configuraciones sobre n servidores.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260622180500.png)

# Fundamentos Conceptos necesarios

Explicación del funcionamiento Ansible:
- Dónde?: Contiene un inventariado que es un archivo que contiene las IP, DNS, o grupos de los servidores
- Con qué?: Con modulos son herramientas que se elijen segun la necesidad, por ejemplo el modulo de apache porque sera un servidor web. estos modulos van a descargarlos.
- Cómo?: Con Playbook que es el archivo yaml/json que es la receta de como se procesara las acciones deseadas. 

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260622181216.png)

# Ejemplo La receta Palaybook (yaml)

Se muestra el inventario junto la receta porque es solo uno, pero si hay muchas direcciones se necesita un archivo aparte para buena practica.
Definimos la tareas con el name, llamamos al modulo que es la herramienta apt (herramienta para instalar cosas en ubuntu). El estado present le indica que simpre tiene que esta presente por lo que ayuda a la idempotencia en los 10 servidores.

![](04%20-%20Otros/Imagenes/Pasted%20image%2020260622181343.png)

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** 
PARTE A: https://drive.google.com/file/d/1AoSZhOXa84f3YQbpy-W1nfYdmiUmJNVD/view?usp=sharing
PARTE B https://drive.google.com/file/d/1OI3tA-8F1qUPwozQsL25rooUsqd-dwDZ/view?usp=sharing
