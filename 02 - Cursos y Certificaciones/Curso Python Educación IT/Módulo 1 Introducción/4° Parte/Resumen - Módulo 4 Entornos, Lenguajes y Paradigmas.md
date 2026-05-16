# 1. Concepto y tipos de paradigmas

Un paradigma es un concepto abstracto; una forma particular de pensar y resolver un problema a la hora de escribir código. Un programa puede usar varios paradigmas al mismo tiempo.

- **Imperativo:** Instrucciones ejecutadas en un orden claramente definido.

- **Declarativo:** Se piden los resultados sin mostrar los pasos exactos para lograrlos.

- **Lógico:** Se basa en la teoría lógica del primer orden y consiste en aplicar reglas de lógica para que nuestros programas puedan inferir conclusiones a partir de los datos que provienen de algún ingreso.

- **Funcional:** más allá de tratarse de funciones,  lo que tiene es que las funciones se pueden enlazar entre sí y formar más complejas
 
- **Programación Orientada a Objetos (POO):** Modela el programa utilizando "objetos" cotidianos. Estos objetos se crean en una clase (simbolizada como una "fábrica"). Cada objeto posee **atributos** (variables, como el color o el tamaño) y **métodos** (funciones, como la acción de "picar" si el objeto es una pelota). Todos los objetos de la misma fábrica pueden tener atributos distintos, pero comparten los mismos métodos.


---

# 2. Tipos de lenguajes y características

Un lenguaje de programación tiene un vocabulario y reglas gramaticales (sintaxis) para dar instrucciones a la computadora. Se clasifican según:

### Su Nivel: 

-  **Bajo nivel:** Son muy cercanos al "idioma" de la máquina, lo que los hace rápidos pero muy difíciles de leer para un humano.

- **Alto nivel:** Utilizan palabras lógicas y cercanas al lenguaje humano, facilitando la escritura y lectura del código.

### Su Ejecución: 

- **Compilados:** Se convierten a lenguaje de máquina una sola vez (compilación) antes de ejecutarse. Son muy rápidos y gastan menos recursos, pero suelen tener tipado estático (obligan a declarar el tipo de variable) y requieren una compilación distinta para cada sistema operativo.

- **Interpretados:** El código es traducido en vivo por un programa llamado "intérprete". Tienen tipado dinámico, son de alto nivel y funcionan en cualquier sistema operativo que tenga el intérprete instalado. Como desventaja, consumen más recursos y son un poco más lentos porque corren dos programas a la vez.




---

# 3. Áreas y lenguajes actuales

### Áreas

El uso de un lenguaje depende del objetivo o área de desarrollo:
- **Front-End:** Es el desarrollo de la interfaz que ve el usuario (del lado del cliente). Utiliza **HTML** (para la estructura básica/paredes), **CSS** (para el diseño visual/terminaciones) y **JavaScript** (para la interactividad). _Dato importante:_ HTML y CSS no son lenguajes de programación, sino lenguajes de maquetado web, ya que no tienen sentencias de control.

- **Back-End:** Trabaja del lado del servidor, procesando la información y las bases de datos. Se utilizan lenguajes como **PHP, Python, C#, Node.js y SQL**.

- **Full Stack:** Es un programador senior integral que domina tanto el Front-End como el Back-End, y puede diseñar la arquitectura completa de los servidores.

- **Data Science:** Se encarga de analizar datos masivos (Big Data) e implementar Machine Learning (algoritmos que aprenden de los datos). Utiliza lenguajes como **Python, R** (ideal para estadística y gráficos) **Matlab, Octave, Julia y SQL**.

- **Desarrollo Mobile:** Creación de apps para teléfonos usando lenguajes como **Java** o **Kotlin** (este último reconocido oficialmente por Google y líder actual).

- **Bases de Datos:** Se emplea **SQL** para almacenar, manipular y consultar datos en bases relacionales (tablas).

- **QA Testing:** encargado de verificar la calidad de software, solucionar errores y mejora continua de la calidad. Debe conocer de **Python, HTML, Base de datos, análisis y herramientas de web, y experiencia de usuario (UX)**

- **Seguridad Informatica**: Proteger la información, rompiendo ellos mismos para ver vulnerabilidades. Conocen de **Linux, redes, protocolos de comunicación y desarrollar herramientoas con Python**

- **Desarrollo Mobile:** Más que nada en desarrollo de App y juegos, trabajan junto con marketing. Deben conocer **Kotlin, base de datos relacionales y no, servicios web, conocer tecnologias front-end y back-end

- **Desarrollo IoT:** internet de las cosas, conectar objetos cotidianos, para telemetría. Deben manejar  **Python, C, C++, Trabajar con front-end y back-end,  base de datos y servicios web.

### Lenguajes Actuales

- **Python:** lenguaje interpretado, multiplataforma y multiparadigma, tipado dinamico y sirve para muchas tareas. Simple y legible, popular en datos, machine learning, IA, aplicaciones, web, automatización, IoT, seguridad, etc.
- **R:** para ciencias de datos
- **Java:** Se utiliza mucho para desarrollar app en escritorio y mobile.
- **SQL:** consulta a bases de datos, consultar o guardar datos.
- **JavaScript:** Mejorar la navegacion desde el cliente, para paginas web
- **HTML y CSS:**  html es texto plano y trabaja con etiquetas, CSS mejora la presentacion de HTML
- **HTML, CSS y JavaScript:**:** el tridente del front-end, html y ccs no son lenguajes de programación, si son lenguajes de desarrollo y maquetadura.
- **PHP:** usado por back end , facil acceso y grandes herramientas.
- **Kotlin:** viene remplazando a java en el desarrollo de app mobiles
- **C#:** es una evolucion de C y C++. para ser empleado en un amplia gama de aplicaciones empresariales ejecutadas en el framework .NET.
- **C:**  fue credado por Dennis Ritchie, se puede usar en desarrollo en S.O, es complicado, y necesita compilacion.
- **C++:** evoluciono de C, orientado a objetos. Se lo utiliza en Hardware, y necesita ser compilados

---

# 4. Entornos y editores

Para programar, los editores básicos de las computadoras (como Notepad o TextEdit) son insuficientes porque carecen de funciones clave. Por ello, se utilizan editores de código especializados:
- **Visual Studio Code (VS Code):** Desarrollado por Microsoft, es un estándar en el ambiente de programación. Es gratuito, de código abierto, personalizable e incluye herramientas clave como autocompletado inteligente y control integrado de Git.

- **Sublime Text:** Es un editor multiplataforma, ligero y muy rápido. Su gran ventaja es que es increíblemente extensible mediante la instalación de _plugins_ para personalizarlo.

- **Atom:** Desarrollado por GitHub, también es de código abierto y gratuito. Aunque en sus inicios era más lento o inestable, ha madurado y es una excelente opción.