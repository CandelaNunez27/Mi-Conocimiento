# Fundamentos: ¿Nube si o no?

Depende, si necesito arrancar y no tengo los dispositivos físicos, entonces si. Sino hibrida. evaluando el contexto de la empresa. El arquitecto de la nube moderno no se casa con un proveedor, se casa con la eficiencia, a resiliencia y el costo-beneficio del negocio.

# Comparativa: Proveedores
#### Los tres grandes

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260506235915.png)

#### Dominio y especialización

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507000159.png)

#### Perfiles y fortalezas

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507000419.png)

#### Infraestructura base

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507000757.png)

#### Modelos IA generativa

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507001341.png)

#### FinOps (Técnicas para ser lo más eficiente económicamente)

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507002004.png)

# Multicloud: Caso de Uso

El marketing de compras tuyo analizando tus interacciones para mostrarte otro contenido que te pueda interesar.
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260507002336.png)

---
# Práctica

Se ingreso ha *aws* y se configuro un *VPC* y se vieron conceptos de la clase pasada en la web.
Viene una VPC (red virtual aislada, primera instancia de separación lógica) por defecto que recomienda no borrarla ni usarla. Contiene un mapa de de recursos con subredes y tablas de conexión que están totalmente abiertas al gateway, por ende no es recomendable usar esta como vpc porque esta toda expuesta.


#### Crear VPC



- Crear VPC:
	- Nombre: mi-vpc
	- CIDR IPv4: 10.0.0.0/16
  ![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602232926.png)
- Crear Subred Pública:
	- Nombre: public-subnet-1
	- Seleccionar zona: EEEUU
	- Bloque de CIDR de VPC IPv4: 10.0.0.0/16
	- Bloque de CIDR de la subred IPv4: 10.0.1.0/24
	- Se puede agregar tags como "ventas" como autor

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602233505.png)

- Crear Subred Privada:
	- Nombre: private-subnet-1
	- Seleccionar zona: EEEUU
	- Bloque de CIDR de VPC IPv4: 10.0.0.0/16
	- Bloque de CIDR de la subred IPv4: 10.0.2.0/24
	- Se puede agregar tags como "data" como autor
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602233159.png)


#### Crear Servicios Instancia EC2

- Nombre: ec2-1
- ISO: (Ubuntu, Amazon Linux, macOS, Windows, Red Hat, SUSE Linux, Debian)
- Seleccionar hardware disponible:  64 bit, CPU 2 Nucleos, 4GB RAM
- Se puede poner contraseña a la maquina
- Network Settings:  
	- Seleccionar vpc:  mi-vpc
	- Subnet: public-subnet-1
	- Auto asignacion de ip pública: activado
	- Customizar que ip o quienes pueden conectarse con la maquina
- Se puede generar el script para que se crea la maquina automáticamente (como una receta).
- Todo esto se puede hacer por consola, o se puede ejecutar ese script receta en consola. (profesor lo mostrara en la siguiente clase con el usuario con permisos).
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602234519.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602234601.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602234629.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602234714.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260602234743.png)
en formato de código la creacion de esta ec2
```

AWSTemplateFormatVersion: '2010-09-09'
Description: 'CloudFormation template generated from AWS CLI commands - Creates EC2 security group and instance with RDP access'

Parameters:
  VpcId:
    Type: String
    Default: 'vpc-0e2fcaa2b65edae04'
    Description: 'VPC ID for the security group'
  
  SubnetId:
    Type: String
    Default: 'subnet-0ee7132f1dbf8fddf'
    Description: 'Subnet ID for the EC2 instance'
  
  KeyName:
    Type: String
    Default: 'Cande'
    Description: 'EC2 Key Pair name for SSH access'
  
  ImageId:
    Type: String
    Default: 'ami-091138d0f0d41ff90'
    Description: 'AMI ID for the EC2 instance'
  
  AllowedRDPCidr:
    Type: String
    Default: '38.51.28.45/32'
    Description: 'CIDR block allowed for RDP access'

Resources:
  # Security Group - launch-wizard-1
  # Creates a security group in the specified VPC to control inbound/outbound traffic
  LaunchWizardSecurityGroup:
    Type: 'AWS::EC2::SecurityGroup'
    Properties:
      GroupName: 'launch-wizard-1'
      GroupDescription: 'launch-wizard-1 created 2026-06-03T02:36:34.018Z'
      VpcId: !Ref VpcId
      # Security group ingress rule for RDP access (port 3389)
      # Allows RDP connections from specific IP address
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: 3389
          ToPort: 3389
          CidrIp: !Ref AllowedRDPCidr
          Description: 'Allow RDP access from specific IP'
      Tags:
        - Key: Name
          Value: 'launch-wizard-1'
        - Key: ManagedBy
          Value: 'CloudFormation'

  # EC2 Instance - ec2-1
  # Creates a t3.micro instance with Windows AMI and custom configurations
  EC2Instance:
    Type: 'AWS::EC2::Instance'
    DependsOn: LaunchWizardSecurityGroup
    Properties:
      # Instance configuration
      ImageId: !Ref ImageId
      InstanceType: 't3.micro'
      KeyName: !Ref KeyName
      
      # Network configuration
      # Associates public IP and attaches to specified subnet and security group
      NetworkInterfaces:
        - AssociatePublicIpAddress: true
          DeviceIndex: 0
          SubnetId: !Ref SubnetId
          GroupSet:
            - !Ref LaunchWizardSecurityGroup
      
      # Block device mapping configuration
      # Configures root volume with gp3 storage type, encryption, and performance settings
      BlockDeviceMappings:
        - DeviceName: '/dev/sda1'
          Ebs:
            VolumeSize: 30
            VolumeType: 'gp3'
            Iops: 3000
            Throughput: 125
            DeleteOnTermination: true
            Encrypted: false
      
      # CPU Credits configuration for T3 instance
      # Sets unlimited mode for burstable performance
      CreditSpecification:
        CPUCredits: 'unlimited'
      
      # Instance metadata service configuration
      # Enforces IMDSv2 for enhanced security
      MetadataOptions:
        HttpEndpoint: 'enabled'
        HttpPutResponseHopLimit: 2
        HttpTokens: 'required'
      
      # Private DNS name options
      # Configures hostname type and DNS record settings
      PrivateDnsNameOptions:
        HostnameType: 'ip-name'
        EnableResourceNameDnsARecord: false
        EnableResourceNameDnsAAAARecord: false
      
      # Instance tags
      Tags:
        - Key: Name
          Value: 'ec2-1'
        - Key: ManagedBy
          Value: 'CloudFormation'

Outputs:
  SecurityGroupId:
    Description: 'ID of the created security group'
    Value: !Ref LaunchWizardSecurityGroup
    Export:
      Name: !Sub '${AWS::StackName}-SecurityGroupId'
  
  InstanceId:
    Description: 'ID of the created EC2 instance'
    Value: !Ref EC2Instance
    Export:
      Name: !Sub '${AWS::StackName}-InstanceId'
  
  InstancePublicIp:
    Description: 'Public IP address of the EC2 instance'
    Value: !GetAtt EC2Instance.PublicIp
    Export:
      Name: !Sub '${AWS::StackName}-PublicIp'
  
  InstancePrivateIp:
    Description: 'Private IP address of the EC2 instance'
    Value: !GetAtt EC2Instance.PrivateIp
    Export:
      Name: !Sub '${AWS::StackName}-PrivateIp'


```

luego se elimino todo, pero para ello hay que ir eliminando por partes

#### Crear privilegios con usuario 

- En IAM users
- En security credentials
- En Access Keys:
	- Crear access keys
	- Permitir que use la CLI (Línea de Comandos)
	- Descripción: Acceso a consola
	-  Se mostrara el access key y el secret access key que este solo se mostrara una sola vez.

![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260603000218.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260603000251.png)
![](../../../../04%20-%20Otros/Imagenes/Pasted%20image%2020260603000414.png)



---

# Material de Clase

### 1. Introducción

Esta clase está diseñada para proporcionar una visión estratégica y técnica sobre el ecosistema de los "Tres Grandes" (AWS, Azure y Google Cloud).
En 2026, la decisión ya no es "si ir a la nube", sino "cómo orquestar múltiples nubes" para maximizar la eficiencia y la innovación.

#### El panorama estratégico en 2026

El mercado de la nube ha madurado hacia un modelo de **soberanía digital** y **especialización**. Aunque AWS mantiene el liderazgo en cuota de mercado, la brecha se ha cerrado debido a la verticalización de servicios.

| Característica            | Amazon Web Services (AWS)                                           | Microsoft Azure                                             | Google Cloud (GCP)                                                      |
| ------------------------- | ------------------------------------------------------------------- | ----------------------------------------------------------- | ----------------------------------------------------------------------- |
| Cuota de Mercado (aprox.) | ~31%                                                                | ~25%                                                        | ~13%                                                                    |
| Perfil Ideal              | Empresas que buscan un catálogo más amplio y escalabilidad extrema. | Corporaciones con ecosistema Microsoft y enfoque híbrido.   | Startups nativas digitales, IA generativa y análisis de datos masivos.  |
| Fortaleza Técnica         | Madurez de servicios e infraestructura global (Regiones/Zonas).     | Integración nativa con Active Directory, M365 y SQL Server. | Liderazgo en Kubernetes (GKE), IA (Vertex AI) y redes de baja latencia. |

#### Comparativa técnica por dominios

Te dejamos material para profundizar:
![Comparativa de nubes](https://youtu.be/oK1bdIHMCQo?si=luEV10KTSgyMsO0N)

#### A. Cómputo (Compute)

Es el motor de cualquier arquitectura. La tendencia actual es el uso de procesadores propios (ARM) para optimizar el costo/rendimiento.

●       **AWS (EC2):** Ofrece la mayor variedad de instancias. Sus chips **Graviton4** (lanzados recientemente) permiten un ahorro de hasta el 40% frente a los x86 tradicionales.

●       **Azure (Virtual Machines):** tiene una fuerte integración con entornos Windows. Su ventaja estratégica es **Azure Arc**, que permite gestionar VMs en otras nubes o localmente como si fueran de Azure.

●       **GCP (Compute Engine):** permite crear instancias personalizadas, definiendo una cantidad específica de CPU y RAM, evitando pagar por recursos no utilizados.

#### Almacenamiento y bases de datos

| Servicio   | AWS                              | Azure                              | GCP                  |
| ---------- | -------------------------------- | ---------------------------------- | -------------------- |
| Objetos    | S3 (El estándar de la industria) | Blob Storage                       | Cloud Storage        |
| Relacional | RDS / Aurora                     | Azure SQL / Cosmos DB (PostgreSQL) | Cloud SQL / Spanner  |
| NoSQL      | DynamoDB                         | Cosmos DB                          | Firestore / BigTable |


_**Nota:** Google **Cloud Spanner** sigue siendo el referente para bases de datos relacionales con escalabilidad horizontal global y consistencia fuerte, ideal para transacciones financieras globales._

  

#### Inteligencia artificial y datos

En 2026, la IA es el principal motor de migración a la nube.

●       **Google Cloud:** Es el líder indiscutido en innovación de modelos. **Gemini** integrado en **Vertex AI** ofrece herramientas de entrenamiento y despliegue que suelen ser más ágiles para equipos de Data Science.

●       **Microsoft Azure:** Su alianza con OpenAI le da exclusividad sobre los modelos GPT más avanzados mediante **Azure OpenAI Service**, lo que lo hace imbatible para aplicaciones empresariales de lenguaje natural integradas en Teams/Office.

●       **AWS:** Apuesta por la "democratización" con **Amazon Bedrock**, una plataforma que permite elegir entre múltiples modelos (Claude, Llama, Mistral) sin gestionar infraestructura.

#### Criterios para la toma de decisiones estratégicas

Para decidir qué proveedor (o combinación de ellos) utilizar, se deben evaluar los siguientes vectores:

1. **Vendor Lock-in (Dependencia):** ¿Qué tan fácil es salir? El uso de contenedores (**Kubernetes**) facilita la portabilidad.
2. **Estructura de Costos (FinOps):**

- **AWS:** ofrece descuentos mediante reservas y compromisos de uso. Puede generar ahorros importantes, aunque su estructura es compleja.
- **Azure:** Ventaja Híbrida (si ya tienes licencias Windows/SQL Server locales, el ahorro es enorme).
- **GCP:** descuentos automáticos por uso sostenido y facturación por segundo.

4. **Cumplimiento y Regulación:** En la UE y Latinoamérica, la residencia de datos es clave. Azure suele tener una ligera ventaja en certificaciones gubernamentales específicas.

_**Ejemplo:** Una empresa de retail utiliza AWS para su e-commerce global por su estabilidad, pero procesa toda su analítica de marketing en BigQuery (GCP) debido a su velocidad superior en consultas masivas de datos._

---
# Grabación de la Clase

**Clase Grabada**: https://drive.google.com/file/d/1YZODY4eklbJaPUicdFIWvrWA1DU-G5e6/view?usp=sharing
