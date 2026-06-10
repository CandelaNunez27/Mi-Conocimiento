# Utilidades de Red y Configuración en Linux

## 1. Conceptos y Servicios Básicos

* **DHCP (Dynamic Host Configuration Protocol):** Servicio que asigna automáticamente direcciones IP, máscara, puerta de enlace y DNS a los dispositivos que se conectan a la red.

* **DNS (Domain Name System):** Sistema que traduce nombres de dominio legibles para humanos (ej. `www.google.com`) a direcciones IP legibles por máquinas.

* **Comandos de diagnóstico:**
    * `ip addr show`: Muestra las direcciones IP e interfaces. El estado `UP` significa que la interfaz está activada por software, y `RUNNING` significa que tiene conexión física (el cable está conectado).
    * `ping`: Verifica la conectividad de red con otro equipo enviando paquetes de prueba (ICMP).

## 2. Configuración de Red en Linux (Laboratorio)

### Ubuntu (Usando Netplan)
A partir de las versiones modernas, Ubuntu usa `netplan` con archivos YAML (generalmente en `/etc/netplan/`).

* **Aplicar IP Estática:**
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      addresses:
        - 10.10.10.2/24
      routes:
        - to: default
          via: 10.10.10.1
      nameservers:
	    search: [mydomain, otherdomain]
        addresses: [10.10.10.1, 1.1.1.1]
```
* **Aplicar IP Dinámica:**
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp3s0:
      dhcp4: true
```
* **Comando para aplicar:** `sudo netplan apply`
### Alpine Linux

Las distribuciones ligeras o basadas en sistemas más tradicionales usan `/etc/network/interfaces`.

- **Aplicar IP por DHCP:**
``` Bash
auto eth0
iface eth0 inet dhcp
```

- **Aplicar IP Estática:**
```Bash
auto eth0
iface eth0 inet static
    address 192.168.1.100
    netmask 255.255.255.0
    gateway 192.168.1.1
    dns-nameservers 8.8.8.8 8.8.4.4
```
- **Comando para aplicar:** `sudo /etc/init.d/networking restart`




