# Planificación y diseño de un clúster de HPC

# 0. Glosario

- **HPC (High Performance Computing)**: cómputo de alto rendimiento. Usar muchas computadoras trabajando en paralelo para resolver problemas que a una sola le llevarían muchísimo tiempo.

- **Cluster**: conjunto de computadoras conectadas que funcionan como si fueran una sola máquina.

- **Nodo**: cada una de las computadoras que forman el cluster.

- **Socket**: la CPU física de un nodo. Un nodo puede tener uno o más.

- **Core (núcleo)**: cada unidad de procesamiento dentro de un socket. Un socket tiene varios.

- **NUMA**: organización de la memoria por la cual cada socket accede más rápido a la memoria que tiene al lado que a la del otro socket.

- **HPL (High Performance Linpack)**: el benchmark de la competencia. Resuelve un sistema de ecuaciones lineales muy grande y mide el rendimiento del cluster. Es el mismo que se usa para el ranking Top500.

- **Benchmark**: programa de prueba que sirve para medir el rendimiento de un sistema.

- **FLOPS / GFLOPS**: operaciones de punto flotante por segundo. Los GFLOPS son miles de millones por segundo. Es la unidad del puntaje.

- **Rpeak**: el máximo rendimiento teórico que podría dar el hardware.

- **Rmax**: el rendimiento que realmente se logra con HPL.

- **Eficiencia**: cuánto se le saca al hardware. Se calcula como Rmax dividido Rpeak.

- **Residual**: verificación de correctitud que hace HPL. Si da bien, la corrida es válida; si da mal, no cuenta aunque el puntaje sea alto.

- **MPI (Message Passing Interface)**: estándar con el que se comunican entre sí los procesos que corren en distintos nodos. OpenMPI y MPICH son implementaciones.

- **Rank**: cada proceso individual de MPI.

- **BLAS**: biblioteca que hace el cálculo pesado (multiplicar matrices). OpenBLAS, BLIS y MKL son implementaciones.

- **dgemm**: la operación central de la BLAS, la multiplicación de matrices en doble precisión.

- **Doble precisión**: formato numérico de mayor exactitud (64 bits). La competencia obliga a usarlo y prohíbe la precisión mixta.

- **InfiniBand**: red de alta velocidad y muy baja latencia, pensada para HPC, distinta del Ethernet común.

- **RDMA (Remote Direct Memory Access)**: técnica que permite que un nodo lea o escriba directamente en la memoria de otro sin molestar a su CPU ni a su sistema operativo. Es lo que hace tan rápida a InfiniBand.

- **Kernel bypass**: que la aplicación hable directo con la placa de red sin pasar por el sistema operativo en cada mensaje.

- **Zero-copy**: que los datos viajen sin copiarse de un buffer a otro.

- **Latencia**: el tiempo que tarda en llegar un mensaje. En HPL suele pesar más que el ancho de banda.

- **Ancho de banda**: la cantidad de datos que la red puede mover por segundo.

- **Subnet Manager (SM)**: componente que configura la red InfiniBand (descubre la topología, asigna direcciones y calcula las rutas). Suele ser el programa opensm.

- **UCX**: biblioteca que le permite a MPI elegir el mejor camino de comunicación: memoria compartida dentro de un nodo y RDMA sobre InfiniBand entre nodos.

- **IPoIB (IP over InfiniBand)**: interfaz de red con IP montada sobre InfiniBand, para servicios como SSH o NFS. Es más lenta que RDMA, así que se usa para gestión y no para el cálculo.

- **OFED / rdma-core**: conjunto de drivers y bibliotecas que habilitan InfiniBand y RDMA en Linux. rdma-core viene con la distro; MLNX_OFED es la versión del fabricante.

- **Filesystem compartido (NFS)**: almacenamiento que todos los nodos ven igual, para no copiar los binarios a mano en cada máquina.

- **Scheduler / Slurm**: planificador que encola y reparte las corridas entre los nodos.

- **Environment modules / Lmod**: sistema para tener varias versiones de compilador, MPI y BLAS y elegir cuál usar sin romper el sistema.

- **Infraestructura como código (IaC)**: describir la configuración de los nodos como archivos que se pueden repetir. Ansible es una de las herramientas.

- **Ansible**: herramienta de automatización que configura todos los nodos de forma repetible.

- **Spack / EasyBuild**: gestores de paquetes para HPC que compilan MPI, BLAS y HPL con versiones fijas y reproducibles.

- **Toolchain**: el conjunto de compilador, MPI y BLAS con el que se construye HPL.

- **HPL.dat**: archivo de configuración de HPL donde se ajustan los parámetros que afectan el puntaje.

- **N (tamaño del problema)**: tamaño de la matriz. Conviene que ocupe casi toda la memoria sin usar disco. Es el parámetro que más influye.

- **NB (tamaño de bloque)**: en qué tamaño de bloques se parte la matriz. Se prueban valores como 192, 224 o 256.

- **P × Q**: la grilla en que se acomodan los procesos. Conviene lo más cuadrada posible.

- **BCAST**: el algoritmo con que se difunden los bloques por la red. Depende de la red y se ajusta con el equipo de redes.

- **Pinning**: fijar cada proceso a un núcleo concreto para respetar la localidad de la memoria.


  
  
  
  
  
  
  
  
  
  
  
  
  

# 1. Contexto y objetivo

La competencia consiste en configurar y optimizar un cluster para que rinda lo más posible en HPL, que es el mismo benchmark que se usa para armar el ranking Top500 de las supercomputadoras más grandes del mundo. Cada equipo tiene al menos tres nodos, y del hardware se encarga la organización, así que nosotros nos ocupamos solo del software y la configuración.

El objetivo es sacar el puntaje más alto posible, que se mide en GFLOPS, pero hay tres reglas que condicionan todo. Primero, tenemos que compilar HPL nosotros desde el código fuente: no se puede usar el binario ya optimizado que da el fabricante ni versiones de precisión mixta, así que va en doble precisión. Segundo, hay que entregar un póster con los integrantes, las estrategias de optimización y las decisiones de diseño. Y tercero, algo que afecta a todo lo demás: participamos a distancia. No vamos a tocar las máquinas físicamente, todo se hace de forma remota, y si hay un problema de hardware o de cables lo tiene que resolver la gente que está en el centro de cómputo. Por eso la automatización y la reproducibilidad, que en otro contexto serían un lujo, acá son casi obligatorias.

Para ubicarnos, es la Student Cluster Competition que se hace dentro de la conferencia CARLA. Por lo que fue avisando la organización, la competencia dura dos días (en el último aviso quedaron el 22 y 23 de septiembre) y compite la mitad de los equipos cada día, así que a cada equipo le toca una sola jornada; los resultados los dan al día siguiente. Es mixta: hay equipos presenciales y equipos a distancia, y nosotros vamos a distancia. Un dato importante para organizarnos es que a los equipos les dan acceso al hardware la semana anterior para preparar los sistemas, y se quedan con ese mismo hardware el día que compiten. Esa semana de acceso es una ventana corta que conviene aprovechar bien, y es justo por eso que nos sirve tanto tener todo escrito como código.

# 2. Conceptos que conviene tener claros

Para que se entienda el resto, dejamos explicados los conceptos que aparecen, agrupados según para qué sirven.

Fundamentos. El cómputo de alto rendimiento (HPC) es usar muchas computadoras trabajando en paralelo para resolver problemas que a una sola le llevarían un montón de tiempo; la idea es partir el problema en pedazos y resolverlos al mismo tiempo. Al conjunto de computadoras conectadas que funcionan como si fueran una sola le decimos cluster, y a cada máquina, nodo. Adentro de un nodo conviene distinguir el socket (la CPU física), el core (cada núcleo de procesamiento, y un socket tiene varios) y la parte NUMA de la memoria, que básicamente dice que cada socket llega más rápido a la memoria que tiene al lado que a la del otro. Por eso conviene que cada proceso trabaje con la memoria que le queda cerca.

El benchmark. El programa que nos miden, HPL, resuelve un sistema de ecuaciones lineales muy grande. Su rendimiento se mide en GFLOPS, que son miles de millones de operaciones por segundo, y ese número es el puntaje. Para leerlo bien conviene diferenciar el Rpeak, que es lo máximo que podría dar el hardware en teoría, del Rmax, que es lo que realmente logramos; si dividimos uno por otro tenemos la eficiencia, o sea cuánto le sacamos a la máquina. Que la eficiencia sea alta demuestra mejor trabajo que un número grande logrado con hardware más potente. Aparte del puntaje, HPL chequea que la solución esté bien (el residual): si da bien, la corrida vale, y si da mal no cuenta por más alto que sea el número.

Cómputo y comunicación. Los procesos que corren en distintos nodos se comunican con MPI, que es el estándar que usa HPL para repartir el trabajo; a cada proceso se le dice rank, y OpenMPI y MPICH son dos implementaciones. El cálculo pesado en sí, que es multiplicar matrices, lo hacen las bibliotecas BLAS (su operación principal en doble precisión es dgemm), y ahí entran OpenBLAS o BLIS. A diferencia de MPI, la BLAS trabaja adentro de cada nodo y no usa la red.

La red. La red que conecta los nodos es InfiniBand, que es muy rápida y de muy baja latencia, pensada para HPC, distinta del Ethernet común y con la particularidad de que no descarta paquetes cuando se congestionan. Lo que la hace tan rápida es una técnica que se llama RDMA, que le permite a un nodo leer o escribir directo en la memoria de otro sin molestar a la CPU ni al sistema operativo del otro nodo. Esto se apoya en dos ideas: que la aplicación habla directo con la placa de red sin pasar por el sistema en cada mensaje, y que los datos van sin copiarse de un lado a otro. Como la placa se encarga por hardware de que todo llegue bien y en orden, la CPU queda libre para calcular, que es lo que nos interesa.

Para que una red InfiniBand funcione hace falta un Subnet Manager, que es lo que descubre cómo está armada la red, le pone direcciones a cada placa y calcula las rutas; suele ser un programa que se llama opensm o venir dentro de un switch administrado, y si la red no anda lo primero que conviene revisar es que ese programa esté corriendo. Arriba de eso, una biblioteca llamada UCX es la que le permite a MPI elegir solo el mejor camino: memoria compartida si los procesos están en el mismo nodo, y RDMA sobre InfiniBand si están en nodos distintos. También existe IPoIB, que arma una interfaz de red normal (con IP) arriba de InfiniBand para las cosas que la necesitan, como el acceso remoto o el filesystem compartido; como pasa por el camino tradicional del sistema es más lenta que RDMA, así que se usa para gestión y no para el cálculo pesado. Todo este soporte se activa en Linux con OFED o rdma-core: rdma-core viene con la distro y aguanta bien las actualizaciones, y la versión del fabricante trae más cosas pero queda atada a versiones puntuales del kernel.

Servicios del cluster. Para manejar el cluster más cómodos se suman algunos servicios. Un filesystem compartido (normalmente NFS) hace que todos los nodos vean el mismo disco, así no tenemos que copiar los binarios a mano en cada máquina. Un planificador como Slurm se encarga de encolar y repartir las corridas entre los nodos, cosa que sirve un montón para trabajar a distancia y entre varios. Los environment modules, como Lmod, nos dejan tener varias versiones de compilador, MPI y BLAS instaladas y elegir cuál usar sin romper nada. Y por encima de todo, la idea de infraestructura como código con herramientas como Ansible nos deja describir la configuración de los nodos en archivos que se pueden repetir, así levantamos el cluster en minutos; y gestores como Spack o EasyBuild compilan MPI, BLAS y HPL con versiones fijas para que el resultado no dependa de la suerte.

  

# 3. Cómo lo encaramos

La decisión más importante de todas es tratar el armado del cluster como un proyecto de software y no como algo que se configura a mano. Todo lo que tocamos queda escrito como código: se automatiza con Ansible, se versiona con Git y se prueba antes de pasar a la capa siguiente.

Esto nos da tres cosas. Una, que es reproducible: el entorno se levanta siempre igual, así cometemos menos errores cuando sumamos nodos. Dos, que va quedando registrado: el historial de decisiones que anotamos es, sin trabajo extra, buena parte del contenido del póster. Y tres, que es lo más importante siendo a distancia, que si algo se rompe lo podemos rearmar de forma remota, porque como no podemos ir a arreglar nada físicamente, tener todo como código nos salva.

# 4. Requerimientos

Con todo esto ya podemos escribir los requerimientos, o sea las cosas que si las cumplimos nos llevan al objetivo. Les pusimos un código a cada uno para poder nombrarlos, y separamos lo que es obligatorio de lo recomendado y de lo que todavía falta confirmar con la organización.

En lo funcional, es obligatorio correr HPL repartido entre los nodos que nos den (RF-01), compilarlo nosotros desde el código fuente sin usar el binario del fabricante (RF-02), correrlo en doble precisión (RF-03) y chequear que cada corrida pase la validación del residual (RF-04); además, MPI tiene que usar la red InfiniBand y no TCP ni Ethernet para el cálculo (RF-05). Como recomendados están usar un planificador (RF-06), tener los binarios y datos en todos los nodos con un filesystem compartido (RF-07) y manejar las versiones del toolchain con modules (RF-08).

En lo no funcional, damos por obligatorias la reproducibilidad (RNF-01), buscar buen rendimiento y buena eficiencia (RNF-02), poder manejar todo de forma remota sin tocar nada físico (RNF-03), poder escalar a los nodos que nos toquen sin reconfigurar a mano (RNF-04) y dejar registradas las decisiones de diseño (RNF-05). Como recomendados sumamos la mantenibilidad y el trabajo en equipo apoyado en el versionado (RNF-06) y poder medir la red y revisar cada capa (RNF-07).

Después están las restricciones, que son cosas que ya vienen dadas: el hardware lo pone y mantiene la organización (RES-01), cada equipo tiene al menos tres nodos con InfiniBand (RES-02), están prohibidos el binario de HPL del fabricante y la precisión mixta (RES-03) y participamos a distancia, con acceso al hardware la semana anterior a la competencia (RES-04). Falta confirmar si hay un tope de potencia o si van a tomar otros benchmarks (RES-05), algo que retomamos más abajo. Y como entregables tenemos que hacer el póster con integrantes, estrategias y decisiones (RE-01), dejar el cluster andando y reproducible con los resultados documentados (RE-02) y mandar un logo del equipo para mostrar en nuestra estación (RE-03).

# 5. Arquitectura del sistema

El sistema lo pensamos como una pila de capas donde cada una se apoya en la de abajo, y cada elección que hacemos es una decisión de diseño que después anotamos. Abajo de todo está el sistema operativo, que tiene que ser la misma distro de Linux, y la misma versión, en todos los nodos. Arriba va la red InfiniBand con sus drivers y su gestor de subred, que es la capa que más pesa en el rendimiento. Después vienen los servicios del cluster (el filesystem compartido, el planificador y los modules), después el toolchain, que es el compilador más MPI más la BLAS, y arriba de todo la aplicación, que es HPL compilado por nosotros contra ese MPI y esa BLAS.

# 6. La red

Vale insistir en que la red no es un detalle: en HPL es una de las cosas que definen el puntaje. Mientras corre, los procesos pasan bloques de la matriz por la red todo el tiempo; si la red es lenta o tiene mucha latencia, los núcleos se quedan esperando datos en vez de calcular y la eficiencia se cae. Y como en muchas de esas comunicaciones pesa más la latencia que el ancho de banda, cada microsegundo que ahorramos se nota en el puntaje.

El trabajo sobre la red lo vamos haciendo de a poco. Primero descubrimos qué hardware de red hay y armamos el mapa de cómo está conectado; después instalamos los drivers y ponemos a andar el gestor de subred hasta que los enlaces quedan activos; después probamos que la comunicación directa entre nodos funcione sin errores y medimos una línea base de latencia y ancho de banda. Recién ahí lo integramos con MPI, cuidando que de verdad use InfiniBand, y al final ajustamos los parámetros de red que afectan el puntaje. La parte de integrar con MPI es la más delicada y es donde nos cruzamos con el equipo de software: si por una mala configuración MPI termina usando TCP en vez de InfiniBand, la latencia pasa de microsegundos a milisegundos y el puntaje se desploma sin que se entienda por qué, así que verificar esto con mediciones no lo podemos saltear.

# 7. Plan de trabajo

El plan lo pensamos por partes, sumando complejidad sobre algo que ya funciona. Arrancamos con un solo nodo, con HPL compilado y corriendo, que nos sirve de línea base. Después sumamos un segundo nodo y comprobamos que MPI y la red anden entre máquinas. Más adelante llegamos a los tres nodos, con el filesystem compartido y el planificador en su lugar y todo levantado con automatización. La cuarta parte es ajustar los parámetros de HPL y armar la curva de puntaje. Y por último, en la semana anterior a la competencia, cuando nos den acceso al hardware definitivo, replicamos todo ahí (que con la automatización es cuestión de minutos) y cerramos el póster y el logo.

# 8. El equipo y los riesgos

El trabajo lo dividimos en dos frentes que van en paralelo. El de software se ocupa del sistema operativo, la automatización, las compilaciones, el planificador y el ajuste de HPL; el de redes se ocupa de InfiniBand, o sea los drivers, el gestor de subred, el diagnóstico, verificar la comunicación directa y el rendimiento de la red. Los dos frentes se juntan en la integración con MPI, que es donde hay que asegurarse de que la comunicación viaje por la red rápida.

En cuanto a los riesgos, el más propio de esta modalidad es que la ventana para preparar el hardware definitivo es corta (la semana anterior), así que perder tiempo rearmando a mano nos saldría caro; teniendo todo como código lo desplegamos en esa semana en minutos y usamos el resto del tiempo para medir y ajustar. Que no podamos tocar las máquinas lo compensamos hablando seguido con la gente que está en el centro de cómputo. Si se nos cae la conexión o tenemos franjas de acceso limitadas, lo resolvemos coordinándonos y dejando corridas encoladas en el planificador. Tampoco queremos perseguir un número alto a costa de que la corrida no sea válida: si el residual no da, no sirve, así que validamos siempre. Además conviene confirmar cuanto antes que vamos a estar disponibles el día que nos asignen, para avisarle a la organización con tiempo si hubiera algún lío. Y para que el conocimiento no dependa de una sola persona, dejamos todo en el repositorio y documentado.

# 9. Cómo optimizamos HPL

El puntaje sale de ajustar los parámetros de configuración de HPL y también la forma en que estructuramos la ejecución, y la idea es ir cambiando una cosa por vez y anotando cada resultado para armar una curva que se pueda seguir.

De los parámetros, el que más influye es el tamaño del problema: conviene que ocupe más o menos entre el 85% y el 90% de la memoria total sin llegar a usar el disco, y eso se calcula a partir de la memoria que hay. El tamaño de bloque en que se parte la matriz lo probamos entre valores como 192, 224, 256 o 384, y en procesadores modernos lo mejor suele estar entre 192 y 256. La grilla de procesos la elegimos lo más cuadrada posible, con la primera dimensión menor o igual a la segunda y su producto igual a la cantidad de procesos. El algoritmo con que se difunden los bloques, que depende de la red, lo ajustamos junto con el equipo de redes; el mecanismo de anticipación lo dejamos en el valor más común para solapar comunicación y cálculo; y el método de factorización del panel lo probamos hasta dar con el más rápido.

De la forma de ejecución, lo que mejor suele andar es un esquema híbrido: un proceso de MPI por cada dominio de memoria, con la BLAS trabajando en varios hilos sobre los núcleos de ese dominio, y los procesos fijados a sus núcleos. Como respeta la localidad de la memoria, esto suele rendir mejor que poner un proceso por núcleo con una BLAS de un solo hilo.

# 10. Qué sistema operativo usar

Que el sistema operativo va a ser Linux no está en discusión, porque es el único con soporte de verdad para HPC e InfiniBand; lo que hay que decidir es qué distro. Para elegir miramos tres cosas: que sea compatible con el software de HPC y los drivers de la red, que sea estable para poder repetir todo, y en menor medida qué tan cómodos estamos con ella.

La que recomendamos es una de la familia de Red Hat en su versión gratis: Rocky Linux o AlmaLinux. La razón principal es que esta familia es el estándar en los centros de supercómputo, así que el software del área (los drivers de InfiniBand, el planificador, los sistemas de archivos) se prueba primero contra ella, y en la práctica eso significa menos sorpresas y documentación que coincide con lo que uno encuentra. Aparte es muy estable, con un kernel que no cambia de golpe y soporte por muchos años, que en un cluster es una ventaja. Rocky y AlmaLinux son copias fieles de Red Hat Enterprise Linux sin costo de licencia, así que tenemos esa compatibilidad sin pagar nada. Lo único en contra, que trae paquetes de base algo viejos, casi no nos afecta porque el software importante lo compilamos aparte con versiones fijas.

Ubuntu Server, en su versión de soporte largo (la que dice LTS), también es una opción que sirve, y seguramente la segunda más usada. Tiene una comunidad enorme, los drivers de red están tanto en sus repositorios como en los paquetes oficiales del fabricante, y es más fácil para el que viene del escritorio. Sus contras son chicas: es menos común en los centros más tradicionales y a veces el soporte de algunos fabricantes llega un poco después que en Red Hat. Si la usamos, tiene que ser la LTS y no las versiones intermedias. Hay una tercera opción, la familia de SUSE para empresas, que está en varias supercomputadoras (sobre todo en equipos de HPE y Cray); es sólida pero menos común por acá y menos conocida para nosotros.

Lo que sí conviene evitar son las distros de actualización continua, como Arch, Fedora o la variante Tumbleweed de openSUSE. Su kernel cambia seguido, y como el soporte de InfiniBand del fabricante suele estar atado a versiones puntuales del kernel, una actualización nos puede romper la red de un día para el otro; además va en contra de la reproducibilidad que buscamos en todo el proyecto.

Igual, lo que manda por sobre todo esto es alinearnos con la distro que soporte o traiga el hardware de la organización. Como el acceso a ese hardware es la semana anterior, conviene averiguar antes qué imagen o distro traen esos nodos y acomodarnos a eso. Mientras tanto, para ir practicando con lo nuestro, la recomendación concreta es Rocky Linux o AlmaLinux en su versión 9; si después la organización dice otra cosa, cambiar es rápido porque tenemos todo escrito como código.

# 11. Por qué usamos estas bibliotecas

Las bibliotecas no dan lo mismo: cada una influye en el rendimiento o en la reproducibilidad, así que las elegimos con un motivo. Para la comunicación entre procesos vamos por una implementación abierta y madura de MPI, como OpenMPI, porque soporta bien InfiniBand a través de la capa de transporte, tiene mucha documentación y es un estándar que no nos ata a ningún fabricante, lo cual va con las reglas de la competencia y con la reproducibilidad. MPICH es una alternativa igual de válida, y de hecho es la base de muchas variantes optimizadas.

La biblioteca que más pesa en el puntaje, igual, es la de álgebra lineal (la BLAS). El cálculo de HPL es básicamente multiplicar matrices, así que el rendimiento del benchmark queda casi limitado por lo rápida que sea esa biblioteca; usar una BLAS optimizada para el procesador que nos toque no es un lujo, es lo que hace la diferencia entre una buena eficiencia y una mala. Las opciones típicas son OpenBLAS, que es muy buena y anda en cualquier lado; BLIS (o su versión AOCL), que rinde muy bien en procesadores AMD; y MKL, que es excelente en procesadores Intel. Acá hay un detalle importante sobre las reglas: lo que está prohibido es el binario de HPL del fabricante, no la BLAS, así que enlazar nuestro HPL contra una BLAS de fabricante es totalmente válido. Por eso cuál usamos va a depender del procesador que nos den, y por eso también nos importa conocer las specs del hardware.

La capa de transporte de la comunicación merece un párrafo aparte: usar una biblioteca como UCX hace que MPI aproveche RDMA sobre InfiniBand y use memoria compartida cuando los procesos están en el mismo nodo, evitando que el tráfico se vaya por la red lenta. Buena parte del ajuste fino de la red lo hacemos a través de ella. Por último, el resto de las herramientas las elegimos con el mismo criterio, que es la reproducibilidad y el control: Slurm para encolar y repartir las corridas de forma ordenada y en equipo; Spack o EasyBuild para compilar MPI, BLAS y HPL con versiones fijas, así el resultado no depende de en qué máquina lo armó cada uno; y Lmod para cambiar entre distintas combinaciones de compilador, MPI y BLAS sin romper el sistema. Todas estas decisiones tienen menos que ver con la moda que con ser coherentes con la forma en que encaramos el proyecto.

# 12. Cosas que faltan confirmar con la organización

Hay algunas cosas que todavía no están definidas y que igual afectan la estrategia, así que conviene despejarlas cuanto antes. La más importante es si hay un tope de potencia, porque si lo hay el objetivo deja de ser el máximo puntaje y pasa a ser el máximo puntaje por energía, y eso cambia cuántos nodos prendemos y a qué frecuencia. También nos interesa saber si van a tomar otros benchmarks además de HPL, porque cambiaría la preparación, y conocer las specs exactas del hardware (procesador, memoria por nodo y velocidad de la red), que necesitamos para dimensionar el problema y estimar el máximo teórico, y cómo pesa HPL frente al póster. Todavía falta que nos avisen los requisitos y la fecha de entrega del póster y las specs del logo, cosas que la organización va a comunicar en las próximas semanas.

Como referencia de estrategias y configuraciones, los pósters de los equipos de ediciones anteriores suelen ser la mejor fuente, porque ahí cuentan lo que usaron. No pusimos resultados numéricos de años anteriores porque no tenemos datos confirmados; conviene mirarlos directamente en los materiales oficiales de la competencia.

# 13. Conclusión

La estrategia junta la forma de trabajar de la ingeniería de software (todo como código, reproducible y registrado) con lo específico de HPC, tanto en cómo se arma el stack como en la optimización de HPL y el ajuste de la red. Que sea a distancia, más que una traba, nos obliga a un nivel de automatización y reproducibilidad que en el fondo es una ventaja y que además nos da contenido para el póster. Los próximos pasos son crear el repositorio y el tablero de tareas, definir la distro y las versiones del toolchain, levantar un primer nodo para compilar y validar HPL, escribir el primer procedimiento automatizado del nodo base y arrancar el registro de decisiones que va a alimentar el póster; con eso ya dejamos encaminado el primer hito.