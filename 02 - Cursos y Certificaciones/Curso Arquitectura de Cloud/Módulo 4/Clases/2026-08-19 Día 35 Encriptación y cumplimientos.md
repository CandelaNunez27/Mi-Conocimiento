# Teoría: Encriptación y cumplimientos

# Fundamentos Criptografía aplicada y Cumplimiento en la nube

"De las Matemáticas del certificado a la física del hardware y la certificación ISO 21017"

La seguridad se basa en matemáticas porque la criptografía se usa exclusivamente los números primos


# Fundamentos La paradoja de la caja fuerte

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260822232558.png)

La paradoja de la caja fuerte: toda nuestra riqueza son nuestros datos por ende se deben proteger lo máximo posible.  Por lo que se necesita claves seguras por si se vulnera, se filtra o se roba la contraseña.

# Fundamentos Tipos de Cifrados

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260822233720.png)

- **Cifrado Simétrico:** única clave se comparte entre la gente para acceder a algo, ej si alguien dice la palabra secreta pasa. Su complicación es que como distribuimos esa clave secreta a las personas indicadas. 
  
- **Cifrado Asimétrico:** son dos claves una privada y una publica, usada para ssh. Se genera un cifrado generando una privada y una publica, se podria decir que para acceder se debe pasar por dos candados, primero la publica que es para que viaje cifrada y luego la privada para cuando llegue la publica se pueda descifrar con la privada. Ej tengo un malentin con doble candado y  viene una persona diciendo que el primer candado es 001 (la clave publica) por ende el candado abre, yo al ver que la persona puso correctamente la publica yo sin mostrarle la privada le abro el segundo candado con 002 (la clave privada)


# Fundamentos Ciclo de Vida de la Clave

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260822234918.png)

1. Se genera la clave, recomendada con algoritmos matemáticos.
2. Se distribuye de manera segura, se recomienda que no sea a través de mal, sino por algún software de tokens seguro
3. Almacenarla en la boveda de secretos.
4. Su uso debe tener restricciones estrictas, la primera para los usuarios deberían tener acceso mediante roles RBAC  y MFA, y la segunda para los servicios deberian tener acceso mediante las bovedas de secretos y de ahí puedan encontrar las rutas url que adjuntan los accesos.
5. Rotación de claves y de usuarios cada cierto tiempo por las dudas, por ejemplo que una clave expire cada 45 días
6. Renovación y destrucción ya de cuentas/servicios/claves obsoletas, para poder evitar más puntos vulnerables 

# Fundamentos Importancia de la gestión de claves

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260823015711.png)

Tenemos que cuidar las  claves cuando estan :
- en reposo: que  este almacenadas localmente en nuestro discos, base de datps y su contenido es legible. tiene que estas acegurada con algun idntificador.

- En tránsito: es cuando las claves las tenemos que ir pasando. por ejemplo las conexiones web a nuestra base de datos todo este proceso debe estar inscriptado para que el que consulta no vea datos que no deberia.

# Fundamentos Metodo de gestión KMS

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260823020618.png)

El método de gestión de clave se llama Servicio de Gestión de Claves (KMS) se basa en automatizar el ciclo de vida junto a políticas de acceso: 

- Capa de customer master key (CMK): es la capa de seguridad superior, siendo la llave maestra que encripta y desencripta la clave de datos, ej kms cuando le pedimos que genere una nueva clave es cmk la que le dara una clave incriptada sin que la podamos ver.
- Clave de datos: seria la que encripta ya si los datos reales. Ej kms cuando le pedimos la clave será la cmk la que nos de sin revelar la clave en forma incriptada, luego si ya la queremos ver nos pedira autenticarnos para ver si tenemos los suficientes permisos para darnos la clave de datos desencriptada.

También CMK va rotando periodicamente para tambien rotal la logica/patron de encriptación para más seguridad para que no sea adivinado nuestra logica de todas nuestras claves.

# Fundamentos Normas y cumplimientos

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260823181723.png)


Tenemos muchas  isos como estas:

- **ISO 27001 :** Seria como las normas generales de seguridad de la información, como manejar las password, como manejar los usuarios, como manejar los secretos...

- **ISO 27017 :** Centrada en la seguridad de los servicios de cloud. es la adapptaciṕn de la iso 27001 a la nube.

- **ISO 27018 :** Basada en la protección de datos personales en la nube pública (más protección por lo que es la nube póblica) 

- **GDPR :** esta ya es una ley europea de protección de datos. En europa si hay datos de europeos no pueden salir de eiropa, por ende hay aws con regiones en ialenabia y otros lugares,


# Fundamentos El checklist ISO

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260823193000.png)

1. Gobernanza de password y datos: esa documentación es accesible? quienes pueden accedes? 
2. Donde estan los activos= don de eastan alojados los datos, 
3. accessos mediante iam, como se accede? que cierta gente no tenga acceso por rol
4. criptofradia, rotas cmk? que logica utiliza ? esa logica es de la más segirax?
5. Los logs donde se almacenan? los logs puieden estar ostrando controseñas sin encriptar y por ende pueden ser culneradas,

# Fundamentos HW Security Modules (HSM)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260823193619.png)

Cual es la seguridad de los aparatos físicos que son los que generan almacena y procesan claves sensibles?

1. Se busca el aislamiento absoluto, ya que se necesita una gran cantidad de computo para generar claves seguras, por ende se busca tener hardware dedicado solo a esta tarea
2. ASICs integrados son estos los que genereran la gran carga de computo
3. 





#  48 min





















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

**Clase Grabada:** https://drive.google.com/file/d/1ODsuAElBhDVwlyabGiDsqapwGKNvf_PT/view
