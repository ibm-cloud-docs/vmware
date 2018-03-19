---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-10"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Creación de una máquina virtual con VMware vSphere 6 

1. Pulse con el botón derecho la dirección IP del nodo de host en el panel de inventario de vSphere Client.
2. En la ventana de configuración, seleccione **Custom**.
3. Dé a la máquina virtual un nombre adecuado y pulse **Next**.
4. Seleccione la ubicación de almacenamiento para los archivos de máquina virtual y pulse **Next**.
* El menú de Virtual Machine Version le ofrece la opción de utilizar diferentes tipos de clúster. Puesto que este es un nuevo clúster y no necesita compatibilidad con versiones anteriores, seleccione **Virtual Machine Version 8**. **Nota:** Si utiliza el cliente web para crear un clúster, utilice la versión 11.
5. Seleccione el tipo de **sistema operativo**.
6. Establezca el número de procesadores virtuales (en la página CPUs) y pulse **Next**.
  1. **Nota:** Puede cambiar el número de CPU posteriormente si los recursos están disponibles.
7. Defina la cantidad de memoria que desea para la máquina virtual. Pulse **Next**.
  1. **Nota:** Puede cambiar la cantidad de memoria posteriormente si los recursos están disponibles.
8. En la sección de red, tiene que conectar dos NIC. El NIC 1 es para la red privada y el NIC 2 es para la red pública. El id del tipo de adaptador es “Flexible”. Compruebe que el recuadro de selección “Connect at Power On” esté marcado.
9. En la pantalla SCSI Controller, deje el valor predeterminado "LSI Logic Parallel". En la pantalla Select a Disk, seleccione **Create a new virtual disk**. Mantenga los valores predeterminados en las pantallas **Advanced Options** y **Ready to Complete**. La nueva máquina virtual ya se ha creado. Para empezar a cargar el soporte de instalación, pulse el nombre del servidor en la lista de inventario y pulse **Edit Virtual machine Settings** en Basic Tasks.
<!--* false-->
10. Con CD/DVD Drive 1 seleccionado, seleccione **Connect at power** en Device Status. Para especificar un archivo ISO ubicado en el almacén de datos, pulse **Browse**.
* Los archivos ISO que se cargan en el almacén de datos predeterminado Storage1 se pueden seleccionar aquí. También verá las carpetas que contienen los archivos de configuración/registro (establecidas en el paso 3 en la sección Datastore del proceso de creación de una nueva máquina virtual) de todas las máquinas virtuales de servidor.
11. Después de seleccionar la imagen ISO, está listo para empezar el proceso de instalación del sistema operativo correspondiente.
* Una vez que la máquina virtual invitada esté en funcionamiento, instale [VMWare Tools ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://kb.vmware.com/s/article/1014294){: new_window}, si es compatible.
* Para obtener más información sobre las instrucciones de redes, consulte la página de [Configuración de una red de máquina virtual](/docs/infrastructure/virtualization/virtual-machine-network-setup.html).
