---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Creación de una máquina virtual de VMware ESX

Para crear una nueva máquina virtual, siga estos pasos.
{:shortdesc}

1. Pulse con el botón derecho la dirección IP del nodo de host en el panel de inventario de vSphere Client.
2. Seleccione **Custom** en la ventana de configuración.
3. Dé a la máquina virtual un nombre adecuado y pulse **Next**.
4. Seleccione la ubicación de almacenamiento para los archivos de máquina virtual y pulse **Next**.
5. En **Virtual Machine Version**, seleccione **Virtual Machine Version 8**. <!-- since we are using vSphere instead of the Web Client to create it (in which case we would use version 11 instead).-->
6. Seleccione el **sistema operativo**.
7. Seleccione el número de procesadores virtuales (**página CPUs**) y la cantidad de **memoria** que desea para crear la máquina virtual. **Nota:** Puede cambiar el número de procesadores y la memoria posteriormente si los recursos están disponibles.
En la sección de red, tendrá que conectar dos NIC, el NIC 1 será la red privada y el NIC 2 la red pública. El tipo de adaptador será “Flexible”. Compruebe que **Connect at Power On** esté seleccionado.
8. En la pantalla **SCSI Controller**, deje el valor predeterminado "LSI Logic Parallel". En la pantalla **Select a Disk**, seleccione **Create a new virtual disk**. En las pantallas **Advanced Options** y **Ready to Complete** también debe dejar los valores predeterminados. A continuación, se habrá completado la creación de una nueva máquina virtual. 

Para empezar a cargar el soporte de instalación, pulse el nombre del servidor en la lista de inventario. A continuación, pulse **Edit Virtual machine Settings** bajo **Basic Tasks**.

9. Con **CD/DVD Drive 1** seleccionado, marque el recuadro de selección **Connect at power** en Device Status. Para especificar un archivo ISO ubicado en el almacén de datos, pulse **Browse**.
10. Los archivos ISO que se cargan en el almacén de datos predeterminado Storage1 se pueden seleccionar aquí. También verá las carpetas que contienen los archivos de configuración/registro (establecidas en el paso 3 en la sección **Datastore** del proceso de creación de una nueva máquina virtual) de todas las máquinas virtuales de servidor.

Después de seleccionar la imagen ISO, está listo para empezar el proceso de instalación del sistema operativo correspondiente.

Para obtener más información sobre cómo configurar una red de máquina virtual, consulte la página de [Configuración de una red de máquina virtual](/docs/infrastructure/virtualization/virtual-machine-network-setup.html){:new_window}.
