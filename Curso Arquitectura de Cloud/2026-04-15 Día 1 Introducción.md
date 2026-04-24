# Fundamentos

## La Era On-Premise

Es el modelo tradicional donde la empresa es dueña de toda la tecnología. Se tendría que gestionar el hardware, con rigidez escalable y responsabilidad de mantenimiento.

## Virtualización 

El motor: Virtualización 
-  Hipervisor (VMM): Es la capa de software que separa los recursos físicos del sistema operativo. Permite ejecutar múltiple máquinas virtuales aisladas simultáneamente.
- Impacto: consolida servidores y reduce drásticamente los costos de infraestructura.

![[Pasted image 20260415084103.png|274]]

####  Tipo Hipervisores

- *Bare Metal*: Se instala directamente sobre hardware físico, para servidores y empresas.
	- VMware ESXi, Hyper-V, KVM.
 ![[Pasted image 20260415085443.png|128]]

- *Hosted*: Se instala como una app en el S.O anfitrión.
	- VirtualBox, Workstation.
 ![[Pasted image 20260415085455.png|123]]
 