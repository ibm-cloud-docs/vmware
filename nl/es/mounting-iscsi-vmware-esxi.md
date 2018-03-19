---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Montaje de iSCSI en VMWare ESXi

El montaje de iSCSI en VMWare ESXi puede realizarse con pocos pasos y los detalles del nodo de almacenamiento y del servidor.
{:shortdesc}

1. Inicie sesión en vSphere utilizando la dirección IP privada primaria, el usuario **root** y la contraseña de root.
* En la página de bienvenida, pulse el separador **Configuration**.
* Pulse **Storage Adapters** y luego **Add…**.
* Pulse **OK** para añadir el adaptador de software iSCSI.
* Pulse **OK** para confirmar.
* Después de actualizar, verá el nuevo adaptador de iSCSI en la lista.
* Pulse **Properties** en el panel inferior.
* En la ventana Properties, pulse **Configure** cerca de la parte inferior y defina el valor de **Name** en el IQN del servidor (que se encuentra en la página del dispositivo de almacenamiento en hosts autorizados).
* Pulse el separador **Dynamic Discovery** y luego **Add...**.
* El servidor iSCSI será la IP de destino del dispositivo de almacenamiento. A continuación, pulse el botón **CHAP...**.
* Seleccione **Use CHAP** y deseleccione **Inherit from Parent**. Especifique el **nombre de usuario** (que se encuentra en la página del dispositivo de almacenamiento en hosts autorizados) y su contraseña.
* Seleccione **Do not use CHAP** en la sección Mutual CHAP y pulse **OK**.
* Verá el dispositivo en la ventana Dynamic Discovery; pulse **Close**.
* Confirme el nuevo escaneo de los dispositivos de almacenamiento.
* A continuación, verá el dispositivo en el panel inferior, en gris y con el valor 'unmounted'.
* Pulse el botón derecho del ratón en el nombre de dispositivo y seleccione **Attach**.
* Pulse el menú **Datastore** en la columna de la parte izquierda y pulse **add storage**; seleccione **Disc/LUN**.
* Pulse el dispositivo con el valor 'iqn'.
* Seleccione la versión del sistema de archivos que desea, pulse **next** y luego continúe con el asistente.
* Una vez completado, puede utilizar el iSCSI según sea necesario en el host y las VM que cree.



Para adjuntar un dispositivo de iSCSI de servicio de transferencia de datos, el proceso es el mismo, pero necesitará obtener el IQN del servidor. Efectúe los pasos siguientes desde la consola de ESXi:

En primer lugar, debe obtener el dispositivo:

`esxcfg-scsidevs -a | grep iSCSI`

A continuación, deberá obtener el IQN (en este caso, vmhba33 es el dispositivo de iSCSI):

`vmkiscsi-tool -I -l vmhba33`
