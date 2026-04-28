# Módulo 3

### El Rol del Administrador y el Entorno (3.1 - 3.3)

- **El Administrador de Sistemas:** Es el puesto de TI más demandado. Para ser eficaz, debes dominar Linux usándolo como tu escritorio diario (para ganar experiencia y entender al usuario final).

- **Modo Gráfico (Escritorio):** Usa ventanas, menús y ratón. Ideal para el usuario final y para administrar remotamente usando múltiples terminales a la vez.

- **Modo No Gráfico (Consola):** Solo texto. Es el **estándar para servidores** (ahorra recursos). Al iniciar sesión, puedes ver el MOTD (_Mensaje del día_). Todo se maneja a través de la línea de comandos (_shell_).

- **La Terminal:** Si estás en modo gráfico, usas un "shell gráfico" (como _terminal_ o _x-term_) que básicamente envuelve la consola de texto en una ventana manejable.


---

###  Virtualización y Cloud Computing (3.4)

Para evitar que un usuario acapare todos los recursos de un servidor físico en el entorno multiusuario clásico, se utiliza la virtualización.

- **Virtualización:** Dividir un servidor físico en múltiples servidores virtuales.
    
    - _Host (Anfitrión):_ El equipo físico real.
    
    - _Hipervisor:_ El software que reparte la CPU, RAM y disco.
    
    - _Invitados (Guests):_ Las máquinas virtuales aisladas.
    
    - _Ventajas:_ Ahorro gigante en hardware físico, energía y espacio.

- **Cloud Computing (La Nube):**
    
    - Virtualización a escala global. Alquilas máquinas virtuales o almacenamiento en centros de datos remotos de terceros.
    
    - **Pago por uso:** Solo pagas los recursos (GB, CPU) que consumes al mes.
    
    - **El motor:** Linux es el sistema operativo dominante que hace funcionar la infraestructura de la nube.


---

###  Herramientas de Trabajo en Linux (3.5)

Linux cuenta con soporte de primer nivel para tareas de oficina.

- **Ofimática (LibreOffice):** _Writer:_ Procesador de textos.
    
    - _Calc:_ Hoja de cálculo avanzada (soporta fórmulas y gráficos).
    
    - _Impress:_ Presentaciones.
    
    - _Ventaja:_ Gran compatibilidad con MS Office y exportación directa a PDF.

- **Navegadores Web:** **Firefox** y **Google Chrome** tratan a Linux como ciudadano de primera clase, recibiendo actualizaciones y mejoras al mismo tiempo que otros sistemas operativos.


---

### Seguridad del Equipo y Privacidad Personal (3.6 - 3.7)

#### Proteger el Equipo (Local y Red)

1. **Contraseñas:** Únicas y fuertes (usa gestores como **KeePassX** para recordar solo una clave maestra).
2. **Actualizaciones:** Configura el sistema para buscar parches diariamente (vital para cerrar brechas de seguridad).
3. **Firewall (Cortafuegos):** Bloquea conexiones entrantes no deseadas. Linux usa **iptables** (complejo, en consola), pero en escritorio se maneja fácilmente con la interfaz gráfica **gufw**.

#### Proteger al Usuario (Navegación)

- **Las Cookies:** Las "propias" son buenas (recuerdan tu sesión). Las **"de terceros"** (píxeles de anunciantes, botones de redes sociales) son un riesgo para la privacidad porque te rastrean por todo internet para armar un perfil sobre ti.

- **Estrategias en el Navegador:** Configura tu navegador para enviar la señal de "No rastrear", bloquea las cookies de terceros y haz que borre el historial al cerrarse.

- **Anonimato Extremo:** Si necesitas máxima privacidad, usa el navegador **Tor** (_The Onion Router_). Oculta tu origen rebotando tu conexión por el mundo, aunque puede hacer que algunas páginas modernas no se visualicen correctamente por razones de seguridad.