---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# Instalación de VMware Tools - Linux

VMware Tools es un conjunto de programas de utilidad que mejora el rendimiento del sistema operativo de invitado de la máquina virtual y mejora la gestión de la máquina virtual. Instalar VMware Tools en el sistema operativo de invitado es vital. Aunque el sistema operativo de invitado puede ejecutarse sin VMware Tools, perderá una funcionalidad importante y comodidad.

El servicio se denomina `vmware-guestd` en invitados Linux, FreeBSD y Solaris. El servicio `vmware-guestd` realiza las funciones siguientes dentro del sistema operativo de invitado:

* Pasa mensajes del sistema operativo de host al sistema operativo de invitado.
* Ejecuta mandatos en el sistema operativo para cerrar o reiniciar correctamente sistemas Linux, FreeBSD, o Solaris cuando se seleccionan operaciones de alimentación en la estación de trabajo.
* Sincroniza la hora del sistema operativo de invitado con la hora del sistema operativo de host.
* Ejecuta scripts que permiten automatizar las operaciones del sistema operativo de invitado. Los scripts se ejecutan cuando cambia el estado de alimentación de la máquina virtual.

El servicio se inicia cuando se inicia el sistema operativo de invitado.

Para instalar VMware Tools en un servidor Linux, pulse con el botón derecho del ratón en el servidor que corresponda en vSphere Client, pase el cursor por encima de **Guest** y pulse **Install/Upgrade VMware Tools**.

Este enlace monta una unidad de CD-ROM virtual que contiene el rpm de VMware Tools. Para instalar las herramientas después de montar la unidad de CD-ROM virtual, siga estos pasos:
1. Monte la unidad de CD-ROM mediante el mandato: `mount /dev/cdrom /mnt`.
2. Verifique que el archivo existe y que está montado correctamente mediante el mandato `ls /mnt` en el directorio montado. Verá el archivo `VMWareTools-4.0.0-208167.i386.rpm`. 
3. Ejecute el mandato `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm`.
4. Ejecute el mandato siguiente para configurar VMware Tools para el kernel en ejecución: `/usr/bin/vmware-config-tools.pl`.**Nota:** Se le solicitará que pulse **INTRO** una vez hacia la mitad de las actualizaciones de configuración.
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**Nota:** No es necesario reiniciar la VM después de instalar VMware Tools, aunque se recomienda.

Si VMware Tools se instala correctamente, aparecerá "OK" en la interfaz de vSphere Client.
