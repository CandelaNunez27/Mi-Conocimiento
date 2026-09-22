
### **Fase Preliminar: Conexión al Bastión**

A las 09:15, una vez recuperado el acceso a los clústeres, conéctate a través de la VPN de Tailscale hacia el nodo bastión:

  `sudo tailscale up

```
ssh scct-2613@bastion.tail263e10.ts.net
```

### **Paso 1: Restauración del BIOS (Obligatorio)**

Dado que la organización restableció la configuración de la BIOS a los valores de fábrica antes de la final, debes cargar obligatoriamente el perfil optimizado (HPC, Hyperthreading desactivado, etc.) que respaldaste previamente.

  

Ejecuta los siguientes comandos desde el bastión para restaurar los tres nodos:

 

```
# Nodo 1
ilorest login 10.1.13.1 -u scct-2613 -p '<PASS_BMC>'
ilorest load -f bios-nodo-1.json
ilorest reboot
ilorest logout

# Nodo 2
ilorest login 10.1.13.2 -u scct-2613 -p '<PASS_BMC>'
ilorest load -f bios-nodo-2.json
ilorest reboot
ilorest logout

# Nodo 3
ilorest login 10.1.13.3 -u scct-2613 -p '<PASS_BMC>'
ilorest load -f bios-nodo-3.json
ilorest reboot
ilorest logout
```

_Verificación:_ Comprueba con `ilorest get` en cada BMC que los parámetros de rendimiento se hayan aplicado correctamente. _(Nota: Dale unos minutos a los nodos para que completen el reinicio físico)._

es la contraseña proporcionada por correo.
  

### **Paso 2: Verificación Post-Reinicio del Sistema (`check.sh`)**

Accede al `nodo-1` para comprobar que la red, el almacenamiento NFS, InfiniBand y los servicios se levantaron de manera autónoma:

  

Bash

```
ssh nodo-1
cd /shared/hpl-run/
./scripts/check.sh
```

_Verificación esperada:_

  

- Interfaces de red con IP activa.

- Directorio `/shared` montado correctamente en los tres nodos.

- Dispositivo InfiniBand `mlx5_0` en estado **Active** a **100 Gb/s**.

- Binario local `xhpl` presente en `/opt/hpl/bin/`.

- 36 núcleos detectados por nodo (Hyperthreading deshabilitado).

### **Paso 3: Corrida Corta de Confirmación (Sanity Check)**

Antes de lanzar la corrida pesada, ejecuta una prueba matemática pequeña para asegurar de punta a punta que el sistema responde y genera un resultado válido:

  

```
cd /shared/hpl-run/
./gen_dat.sh 40320 384 1 2 > confirmacion.dat
BIOS=tuneado ./run.sh confirmacion.dat nodo-1,nodo-2,nodo-3 2 18
```

_Verificación:_ La salida en consola debe finalizar obligatoriamente con el estado **PASSED**. Si el residual falla, detén la ejecución y revisa los logs.

  

### **Paso 4: Ejecución de la Corrida Final de Alto Rendimiento (Fase F)**

Utiliza la configuración ganadora de la sesión de sintonización previa ($N = 161280$, tamaño de bloque $NB = 192$, grilla de procesos $P = 9, Q = 12$, con 36 procesos por nodo y 1 hilo por proceso).

Como esta ejecución tomará más de 20 minutos, **desacóplala por completo de la sesión SSH** usando `setsid` y `nohup` para evitar que se interrumpa si se cierra la terminal:

 
```
cd /shared/hpl-run/
./gen_dat.sh 161280 192 9 12 > f-final.dat
setsid nohup ./run.sh f-final.dat nodo-1,nodo-2,nodo-3 36 1 > f-final.out 2>&1 &
```

(Opcional) Monitoreo en tiempo real de la frecuencia real del procesador bajo instrucciones AVX-512 desde otra terminal:

  

```
ssh nodo-2 sudo turbostat --quiet --show Busy%,Bzy_MHz --interval 30
```

_Verificación:_ Una vez finalizada la corrida, revisa el archivo de salida o el registro acumulativo para confirmar que el resultado final indique **PASSED**. El puntaje objetivo de referencia para este hardware ronda los **2136.7 GFLOPS**.

  

### **Paso 5: Preparación de Entregables para la Organización**

Antes del límite de las **18:00**, asegúrate de empaquetar y tener listos los archivos correspondientes a tu mejor rendimiento:

  

1. **Archivo de entrada:** `HPL.dat` (ubicado dentro de la carpeta generada en `/shared/hpl-run/corridas/<sello>/`).
  
2. **Archivo de salida:** `salida.txt` o `HPL.out`.
  
3. **Scripts de ejecución y metadatos:** `run.sh`, `gen_dat.sh` y `comando.txt`.

4. **Script de compilación:** `scripts/06-build-hpl.sh` (para certificar el cumplimiento estricto de la regla de compilar desde el código fuente de netlib).