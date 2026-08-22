# Práctica: sawkl
### Preparación

1. AWS web:
	Ingresar a nuestro usuario administrador de aws, y nos vamos a IAM y veremos los usuarios, y se aconsoja crear un usuario diferente a root. Iam > iam users > creater user > nombre > provide user access > custom assword (sin tildar que la cambien en la siguente secion) > Set permisos > add user to grup >  crear grupo > databasaseadminiostrator > desplegar sus permisos >  le colocamos nombre DBAs2 > creat user.
	
	Con el usuario creado ingresamos a este, y ya vemos que hay cosas que no nos muestra hasta en panel iam. 
	
	Volviendo al administrador vamos a ver el usuario en iam > iam user > usuario que creamos > add permisions > create goup > administraAccess se vera que dice que admite todo a todo> colocamos el nombre admin > add
	
	Volvimos al usuario creado y ya nos muestra lo que antes no mostraba. pero si se lo borramos desde el administrador volvera a no mostrar nada casi
	
	Volvemos al administrador iam > iam users > create user> developer_aws como nombre > provide user access > contraseña > user must create a new > attach policies directly > amazonec2readonlyaccess > vemos que tiene de código > create user
	
	Entramos a developer_aws > nos pedira cambiar la clave > al ingresar no mostrara casi nada > se trata de lanzar una ec2 y no nos deja 
	
	Volvemos al administrador iam > iam users > developer_aws > security credentials > create access key > command line interface (CLI) > confirmar > descripcion: developer aws > create access key > copiamos la publica y la secret que solo se muestra una unica vez. Luego en iam > iam users > el otro usuario> assign mfa device > nombre: cel-google > autenticatos app > scanear el qr en pantalla con el celular y colocar los codigos que nos apareceran en el celular   
	

1. Códing:
	Usaremos el main.tf, output.tf, providers.tf, variables.tf de modulos > extra > repaso 3. 
	
	Y la carpeta .github/workflows tendremos deploy_lambda.yml y primer-actions.yaml. En deploy comentamos la linea 27 terraform init  working-directory: ./modulos/extras/repaso3 con esta linea comentada nos dara error
	
	Nos vamos al github donde nos metemos al settings del repositorio > secret an variables > actions > new repository secret > Name: AWS_ACCESS_KEY_ID_DEVELOPER > Secret: y copiamos la key publica que antes generamos. Luego creamos otra > 
	
	
	
	
	
	
	
	

---
# Guía del Profesor

  
---

# Material de Clase




---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/18ZveHczZqMWJJwKfTstwMQL8nccWy5K5/view
