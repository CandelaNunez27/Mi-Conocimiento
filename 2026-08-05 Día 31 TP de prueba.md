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

## 9) ¿Qué elemento de configuración es indispensable para que una función Lambda tenga permisos de escribir logs en Clouf wrach ?
  
  - Falso (es el compilador/lenguaje de programación que se le cargara a nuestra lambda por ejemplo python)

## 5) En la configuración de una función de Lambda ¿El parámetro runtime se utiliza para elegir la distribución de Linux (como Ubuntu o Amazon Linux) sobre la que correrá el código?
  
  - Falso (es el compilador/lenguaje de programación que se le cargara a nuestra lambda por ejemplo python)

## 5) En la configuración de una función de Lambda ¿El parámetro runtime se utiliza para elegir la distribución de Linux (como Ubuntu o Amazon Linux) sobre la que correrá el código?
  
  - Falso (es el compilador/lenguaje de programación que se le cargara a nuestra lambda por ejemplo python)
  
  
  
  
  
  
  
  
  
  
  
  



---

# Grabación de la Clase

**Clase Grabada:** https://drive.google.com/file/d/1y9Mad3qyUuDOyRtQVmEacKPf3JbcIwUs/view
