
### **Fase Preliminar: Conexión al Bastión**

A las 09:15, una vez recuperado el acceso a los clústeres, conéctate a través de la VPN de Tailscale hacia el nodo bastión:

  `sudo tailscale up` 

```
ssh scct-2613@bastion.tail263e10.ts.net
```

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922114521.png)

Prender los nodos por interfaz gráfica
`ssh -L 8000:10.1.13.1:443 scct-2613@bastion.tail263e10.ts.net`
`ssh -L 8001:10.1.13.2:443 scct-2613@bastion.tail263e10.ts.net`
`ssh -L 8002:10.1.13.3:443 scct-2613@bastion.tail263e10.ts.net`

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922224627.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922224914.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922225006.png)
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
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922225114.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922225152.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922225237.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922225302.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922225332.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922225529.png)

Se agrego los usuarios en ~/ssh/config en los tres, con su script

```
Host nodo-1
  HostName 10.2.13.1
  User zonda-hpc1
Host nodo-2
  HostName 10.2.13.2
  User zonda-hpc2
Host nodo-3
  HostName 10.2.13.3
  User zonda-hpc3


```

```
#!/bin/bash
# Paso 3 del plan - SSH sin contraseña entre los 3 nodos. Correr en nodo-1.
# Nota (18/09): esto se hizo a mano por bloqueo del clasificador de permisos de
# Claude Code sobre acciones de acceso persistente entre maquinas. Se deja el
# script para referencia/repetibilidad, pero en la practica se corrio paso a paso.
# Requiere que ~/.ssh/config en nodo-1 tenga "User zonda-hpcN" explicito por host
# (si falta, ssh-copy-id intenta entrar con el usuario local en vez del remoto).
set -e
[ -f ~/.ssh/id_ed25519 ] || ssh-keygen -t ed25519 -N "" -f ~/.ssh/id_ed25519
grep -qf ~/.ssh/id_ed25519.pub ~/.ssh/authorized_keys 2>/dev/null || cat ~/.ssh/id_ed25519.pub >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
grep -q "Host nodo-\*" ~/.ssh/config 2>/dev/null || printf "Host nodo-*\n\tStrictHostKeyChecking accept-new\n" >> ~/.ssh/config
chmod 600 ~/.ssh/config
for n in nodo-2 nodo-3; do
	ssh-copy-id $n
	scp ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub ~/.ssh/config $n:.ssh/
done
for a in nodo-1 nodo-2 nodo-3; do
	for b in nodo-1 nodo-2 nodo-3; do
		ssh $a "ssh $b hostname" || echo "FALLA $a -> $b"
	done
done


```
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922232405.png)

### **Paso 2: Correr los script (hacer lo mismo en los tres, cada integrante uso un nodo para hacer los mismos pasos)** 


 `[scct-2613@carlanga ~]$ ssh zonda-hpc1@10.2.13.1 `
 `mkdir scripts`
 `cd scripts
 `TERM=xtern ssh zonda-hpc1@10.2.13.1
 `nano 01-base.sh

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922230107.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922230206.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922230333.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922230559.png)

```
#!/bin/bash
# Paso 4 del plan - base comun. Correr en cada nodo:
#   ssh nodo-N 'bash -s' < scripts/01-base.sh
set -e
curl -sI https://dl.rockylinux.org | head -1
sudo dnf -y update
sudo dnf -y groupinstall "Development Tools"
sudo dnf -y install wget git tar rsync numactl numactl-devel hwloc pciutils environment-modules chrony nfs-utils tuned kernel-tools python3
for h in "10.2.13.1 nodo-1" "10.2.13.2 nodo-2" "10.2.13.3 nodo-3"; do
	grep -q "$h" /etc/hosts || echo "$h" | sudo tee -a /etc/hosts
done
echo "PermitRootLogin no" | sudo tee /etc/ssh/sshd_config.d/10-noroot.conf
sudo systemctl restart sshd
sudo systemctl enable --now chronyd
sudo firewall-cmd --permanent --zone=trusted --add-source=10.2.13.0/24 || true
sudo firewall-cmd --reload
# memlock para RDMA/UCX (encontrado en la practica el 18/09, no estaba en la receta original)
printf "* soft memlock unlimited\n* hard memlock unlimited\n" | sudo tee /etc/security/limits.d/99-hpc-memlock.conf
echo "Falta: sudo reboot (kernel nuevo de dnf update)."

```

`chmod 777 01-base.sh
`./01-base.sh ` 
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922232552.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233212.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233233.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233301.png)![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233334.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233357.png)

reboot en los tres

para comprobar usamos `lscpu; numactl -H; free -g; grep MemTotal /proc/meminfo; lspci | grep -i -E "mellanox|infiniband"`
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233656.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233720.png)

 `nano scripts/02-nfs.sh
`chmod 777 02-nfs.sh
`./02-nfs.sh 

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922233903.png)

```
#!/bin/bash
set -e
if [ "$(hostname -s)" = "nodo-1" ]; then
	sudo mkdir -p /shared
	sudo chown $USER: /shared
	echo "/shared 10.2.13.0/24(rw,sync)" | sudo tee /etc/exports
	sudo systemctl enable --now nfs-server
	sudo exportfs -ra
else
	sudo mkdir -p /shared
	grep -q "nodo-1:/shared" /etc/fstab || echo "nodo-1:/shared /shared nfs defaults,_netdev 0 0" | sudo tee -a /etc/fstab
	sudo mount -a
fi
mkdir -p /shared/registros /shared/hpl-run /shared/src

```

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234254.png)

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234117.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234141.png)

`su -c "echo 'zonda-hpc1 ALL=(ALL) NOPASSWD: ALL' > /etc/sudoers.d/hpc"`
`./02-nfs.sh 
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234439.png)


`nano scripts/04-ib.sh
`chmod 777 02-nfs.sh
`./02-nfs.sh 


![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234631.png)


```
#!/bin/bash
set -e
sudo dnf -y install rdma-core infiniband-diags perftest libibverbs-utils ucx ucx-ib
ibstat
ibv_devinfo | grep -E "hca_id|state|active_mtu"

```

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923002651.png)


![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234758.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234832.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922234947.png)



`nano scripts/05-mkl-mpi.sh

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003025.png)

```
#!/bin/bash
set -e
sudo tee /etc/yum.repos.d/oneAPI.repo >/dev/null <<EOF
[oneAPI]
name=Intel oneAPI repository
baseurl=https://yum.repos.intel.com/oneapi
enabled=1
gpgcheck=1
repo_gpgcheck=1
gpgkey=https://yum.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB
EOF
sudo dnf -y install intel-oneapi-mkl-devel
sudo dnf -y install openmpi openmpi-devel
sudo tee /etc/profile.d/hpc.sh >/dev/null <<'EOF'
export MKLROOT=/opt/intel/oneapi/mkl/latest
export PATH=/usr/lib64/openmpi/bin:$PATH
export LD_LIBRARY_PATH=/usr/lib64/openmpi/lib:$MKLROOT/lib:$LD_LIBRARY_PATH
EOF

```
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923002957.png)


`chmod 777 05-mkl-mpi.sh
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003037.png)

`./05-mkl-mpi.sh
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003100.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003118.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003140.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003349.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003414.png)![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003439.png)![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003524.png)![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003601.png)![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003620.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003651.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003717.png)![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003732.png)



### **Paso 3: Verificación Post-Reinicio del Sistema (`check.sh`)**

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
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923003839.png)

desde aqui lo hizo pedro
  

### **Paso 4: Ejecución de la Corrida Final de Alto Rendimiento (Fase F)**

Si el equipo dispone de tiempo antes de la entrega final y quiere comprobar si existe una combinación superior a la base, ejecute las siguientes tandas de pruebas de forma controlada (registrando cada resultado en `resultados.csv`):

- **A. Barrido de Procesos vs. Hilos (Fase C):** Prueba diferentes distribuciones de paralelismo para verificar si se mantiene la eficiencia con la configuración de 36 procesos por nodo y 1 hilo ($P=9, Q=12$):
    
    
    ```
    ./gen_dat.sh 80640 384 9 12 > c-36x1.dat
    BIOS=tuneado ./run.sh c-36x1.dat nodo-1,nodo-2,nodo-3 36 1
    ```
- **B. Barrido de Tamaños de Bloque ($NB$ - Fase D):** Evalúa si un tamaño de bloque alternativo exprime mejor la caché del Skylake (por ejemplo, probando $NB = 192$ o $256$ en una sola corrida):
    
    Bash
    
    ```
    ./gen_dat.sh 80640 "192 256 336 384" 9 12 > d-nb.dat
    BIOS=tuneado ./run.sh d-nb.dat nodo-1,nodo-2,nodo-3 36 1
    ```

- **C. Verificación de Red y Escalabilidad (Sanity Check a 3 Nodos):** Comprueba que el factor de escala entre 1 y 3 nodos mantenga una eficiencia superior al 90% en la red InfiniBand:
 
    
    ```
    ./gen_dat.sh 40320 384 2 3 > n3.dat
    BIOS=tuneado ./run.sh n3.dat nodo-1,nodo-2,nodo-3 2 18
    ```


Utiliza la configuración ganadora de la sesión de sintonización previa ($N = 161280$, tamaño de bloque $NB = 192$, grilla de procesos $P = 9, Q = 12$, con 36 procesos por nodo y 1 hilo por proceso).

Como esta ejecución tomará más de 20 minutos, **desacóplala por completo de la sesión SSH** usando `setsid` y `nohup` para evitar que se interrumpa si se cierra la terminal:

 
```
cd /shared/hpl-run/
./gen_dat.sh 161280 192 9 12 > f-final.dat
setsid nohup ./run.sh f-final.dat nodo-1,nodo-2,nodo-3 36 1 > f-final.out 2>&1 &
```

(Opcional) Monitoreo en tiempo real de la frecuencia real del procesador bajo instrucciones AVX-512 desde otra terminal y tambien lo guarda en un log:

  

```
ssh nodo-2 sudo turbostat --quiet --show Busy%,Bzy_MHz --interval 30 | tee turbostat_avx512.log
```

_Verificación:_ Una vez finalizada la corrida, revisa el archivo de salida o el registro acumulativo para confirmar que el resultado final indique **PASSED**. El puntaje objetivo de referencia para este hardware ronda los **2136.7 GFLOPS**.

  

### **Paso 5: Preparación de Entregables para la Organización**

Antes del límite de las **18:00**, asegúrate de empaquetar y tener listos los archivos correspondientes a tu mejor rendimiento:

  

1. **Archivo de entrada:** `HPL.dat` (ubicado dentro de la carpeta generada en `/shared/hpl-run/corridas/<sello>/`).
  
2. **Archivo de salida:** `salida.txt` o `HPL.out`.
  
3. **Scripts de ejecución y metadatos:** `run.sh`, `gen_dat.sh` y `comando.txt`.

4. **Script de compilación:** `scripts/06-build-hpl.sh` (para certificar el cumplimiento estricto de la regla de compilar desde el código fuente de netlib).
   
   
   ![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260922142410.png)



# Resultados final

Se llego a 4811 gbflops

`[scct-2613@carlanga submission]$ cat README.md
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923004119.png)

![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923004136.png)
![](../../04%20-%20Otros/Imagenes/Pasted%20image%2020260923004141.png)
