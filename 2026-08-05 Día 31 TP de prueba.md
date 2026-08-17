# Quiz para prepararnos al TP 2 

## 1) ¿Es correcto afirmar que el recurso aws_s3_bucket en Terraform es el encargado de instanciar servidores virtuales en el ecosistema de AWS?
  
  - Falso (aws_ec2_instance seria lo correcto, aws_s3_bucket se limita al almacenaje de objetos)

## 2) ¿Requiere una función AWS Lambda la asociación de un aws_iam_role a pesar de ser una tecnología Serverless de ejecución temporal?
  
  - Verdadero (lambda necesita permisos explícitos definidos en un rol de IAM para interactuar de forma segura con otros servicios de AWS)

## 3) ¿El comando terraform plan realiza modificaciones directas y permanentes en los recursos activos de la infraestructura de nube?
  
  - Falso (Solo muestra una vista previa de lo que se realizara, la ejecución reali se hace con terraform apply )

## 4) ¿Es Ansible una herramienta que opera bajo un modelo agentless, utilizando conexiones ssh para gestionar nodos remotos?
  
  - Verdadero (no requiere de software propietario instalado en los servidores de destino, facilitando la automatización mediante protocolos estándar de comunicación)

## 5) En la configuración de una función de Lambda ¿El parámetro runtime se utiliza para elegir la distribución de Linux (como Ubuntu o Amazon Linux) sobre la que correrá el código?
  
  - Falso (es el compilador/lenguaje de programación que se le cargara a nuestra lambda por ejemplo python)
  
## 6) Al ejecutar "docker build -t mi-imagen.v1 ." ¿El punto final indica que el archivo Dockerfile y los archivos necesarios están en el directorio actual?
  
  - Verdadero (el punto actúa como la ruta del contexto de construcción, indicandole a Docker dónde buscar el Dockerfile y los recursos para la imagen)

## 7) ¿Es el formato .zip un estándar aceptado para empaquetar el código fuente de una función Lambda cuando se despliega mediante infraestructura como Código?
  
  - Verdadero (quedo como sucesor del .rar, y el .zip sirve para subirlo en lamba para subirle varios códigos empaquetados)
  
  
## 8) Si se desea almacenar modelos de inteligencia artificial entrenados de fomra persistente en AWS mediante terraform ¿Qué recurso es el más apropiado?
  
  - aws_s3_bucket (aws_s3_bucket almacena, aws_iam_policy no es porque es para definir permisos de seguridad, aws_instance no es porque se usa para proporcionar capacidad de computo a las EC2, no es aws_lambda_functio porque esta se encarga de ejecutar lógica de código)

## 9) ¿Qué elemento de configuración es indispensable para que una función Lambda tenga permisos de escribir logs en Cloudwatch o leer de una base de datos?
  
  - aws_iam_role (el rol de IAM actúa como la identidad que asume la función para obtener los permisos necesarios durante la ejecución, terraform_data no es porque es para almacenar información temporal en el estado, aws_s3_bucket_objet este recurso se refiere a un archivo especifico dentro de s3, no es docker_container porque docker gestiona la virtualización a nivel de sistema operativo y no los permisos de identidad nativos de la nube de aws)

## 10) En la configuración de una función de Lambda ¿El parámetro runtime se utiliza para elegir la distribución de Linux (como Ubuntu o Amazon Linux) sobre la que correrá el código?
  
  - Falso (es el compilador/lenguaje de programación que se le cargara a nuestra lambda por ejemplo python)

## 11) ¿Cuál es el comando correcto para crear una imagen a partir de un Dockerfile y asignarle un nombre identificativo?
  
  - docker build -t nombre-imagen . (porque no es la opcion docker run -p nombre-imagen . porque -p es para puertos, no es docker pull -t nombre-imagen . porque es para escalar, no es docker commit -m nombre-imagen . porque ese comando es para generar una imagen de un contenedor pero en caliente)
  
## 12) Un administrador necesita verificar qué recursos se destruirán antes de aplicar los cambios en terraform ¿Qué comando proporciona ese análisis?
  
  - terraform plan 

## 13) ¿Qué característica define principalmente a Ansible en comparación con otras herramientas de automatización de IT?
  
  - Su arquitectura sin agentes agentless (utiliza ssh)

## 14) Al configurar un recurso aws_lamba_funtion ¿ Cuál es la función de la propiedad handler?
  
  - Indicar el nombre del archivo y el método que inicia la ejecución (es el es archivo de punto de entrada el archivo para arrancar, dato de color si un proceso dura más de 15 min no utilices lambda porque esta muere)


## 15) Deseas crear una red (VPC) y luego instalar un servidor web Nginx ¿Qué combinación de herramientas es la más eficiente?
  
  - Terraform para la red y Ansible para el software (porque docker no tiene forma de llegar a la VPC ya que es una función de AWS)

## 16) ¿Cuál de los siguentes es un valor válido para la propiedad "runtime" en Terraform al configurar una lambda?
  
  - python3.9 (runtime es donde declaramos el lenguaje de programación, t2.micro no es porque es una familia ec2, ubuntu-22.04 es un sistema operativo, bash-script es un lenguaje de programación pero porque lambda no lo accepta bash en el runtime nativo directamente el la configuración estandar)

## 17) ¿Para qué se utiliza el bloque environment dentro de una definición de recursos Lambda en Terraform?
  
  - Para pasar variables de configuración dinámica al código (permite inyectar valores como claves de API o nombres de bases de datos sin harcodearkis en el código fuente)

## 18) En el flujo de trabajo de Docker ¿El parámetro runtime se utiliza para elegir la distribución de Linux (como Ubuntu o Amazon Linux) sobre la que correrá el código?
  
  - Falso (es el compilador/lenguaje de programación que se le cargara a nuestra lambda por ejemplo python)
  
## 19) En la configuración de una función de Lambda ¿El parámetro runtime se utiliza para elegir la distribución de Linux (como Ubuntu o Amazon Linux) sobre la que correrá el código?
  
  - Falso (es el compilador/lenguaje de programación que se le cargara a nuestra lambda por ejemplo python)
  
  
  
  
  
  
  
  
  
  



---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1y9Mad3qyUuDOyRtQVmEacKPf3JbcIwUs/view
