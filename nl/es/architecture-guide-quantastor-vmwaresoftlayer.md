---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Guía de arquitectura para QuantaStor

Puede solicitar y configurar la solución de almacenamiento compartido OSNexus QuantaStor para un entorno de VMware ESXi 5. Utilice la información siguiente junto con el cookbook de [Arquitectura avanzada de referencia de VMware de un solo sitio](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) para establecer una de estas opciones de almacenamiento en el entorno de VMware.

## Paso 1: Solicitud de almacenamiento compartido QuantaStor

Antes solicitar un pedido de almacenamiento, debe determinar las especificaciones que se ajustan a sus requisitos de capacidad y E/S. Estas especificaciones incluyen, a título enunciativo y no limitativo, el servidor RAM, el tipo y el número de unidades de disco, las SSD para almacenamiento en memoria caché, la configuración RAID y la configuración de red. Para obtener más información sobre cómo elegir la configuración correcta de QuantaStor en su entorno, consulte la [Guía de diseño de solución de QuantaStor para virtualización ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide#Server_Virtualization){: new_window}.

Para el entorno de ejemplo, se utiliza una configuración más pequeña que puede ofrecer suficiente capacidad y E/S necesarias para las máquinas virtuales (VM). Asegúrese de que conoce los requisitos de capacidad y E/S de las VM antes de realizar el pedido. Aunque el servidor QuantaStor es ampliable, es importante determinar el tamaño del hardware inicialmente para evitar retrasos en la configuración y el despliegue.

### Solicitud de QuantaStor

Efectúe los pasos siguientes para solicitar un servidor QuantaStor.

1. Inicie sesión en [{{site.data.keyword.slportal_full}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window} y pulse **Cuenta > Realizar un pedido**.
2. Seleccione {{site.data.keyword.baremetal_short}}, Mensual en la pantalla emergente.
3. En la página de lista de servidores, seleccione el servidor adecuado con capacidad para almacenar el número de discos que necesita para el entorno. [Para el entorno de ejemplo, se selecciona un sistema de 12 núcleos (es decir, dual hex core) con 12 bahías de unidad].
4. Especifique las opciones de configuración siguientes:
  * **Centro de datos:** ubicación de los hosts de VLAN y ESXi que se han creado previamente
  * **Servidor:** Dual Processor Hex Core Xeon
  * **RAM:** 64 GB
  * **Sistema operativo:** OSNexus QuantaStor 3.x (4 TB)
  * **Unidades de disco duro:**
    * Discos 1 y 2: 500 GB SATA en RAID 1
    * Plantilla de partición: Linux Basic
    * Discos 3-10: 600 GB SAS 15K en RAID-10
  * **Ancho de banda público:** Sólo red privada
  * **Velocidades de puerto de enlace ascendente:** Enlaces ascendentes a 10 Gbps de redes privadas redundantes
5. Pulse **Continuar su pedido**.

**Nota:** El servidor de almacenamiento está configurado con dos interfaces de red que no están vinculadas, de modo que se pueden utilizar dos subredes diferentes para equilibrar la carga del tráfico en la matriz de almacenamiento.

### Cómo finalizar la configuración

Ahora tiene un dispositivo QuantaStor en el carro de la compra. A continuación, debe asignar la VLAN privada, el nombre de host y el dominio al dispositivo para que se pueda suministrar correctamente.

1. Asigne las VLAN siguientes y cree nombres de host para los dispositivos: host de QuantaStor - VLAN de fondo: (1102 en el entorno)
2. Seleccione el método de pago, acepte los Términos y condiciones y pulse Finalizar el pedido.

**Nota** No continúe con el paso 3 hasta que el servidor se haya suministrado y se pueda acceder a él por VPN o servidor virtual.

## Paso 2: Habilitación del adaptador de software iSCSI en los hosts de gestión y capacidad

Se debe habilitar el adaptador de software iSCSI en cada host de gestión y se debe obtener su IQN (nombre calificado iSCSI) antes de montar los volúmenes iSCSI. Efectúe los pasos siguientes para habilitar el adaptador de software iSCSI:

1. Vaya a un host de capacidad o gestión de ESXi y seleccione Manage, Storage, Storage Adapters.
2. Pulse el signo más verde (+) y añada el adaptador de software iSCSI.
3. Pulse el vmhba que corresponda al adaptador de software iSCSI y registre el valor de iSCSI Name (Figura 1) en la sección Adapter Details una vez que esté habilitado.
4. Siga los pasos 1 a 3 para cada adaptador de software iSCSI en cada host de gestión y capacidad de ESXi.

## Paso 3: Configuración de QuantaStor

Una vez suministrado el servidor, puede configurar el dispositivo de almacenamiento compartido. Específicamente, configure la red y los volúmenes iSCSI, y asignar volúmenes a hosts. 

Por ejemplo, el volumen vmk3 tiene a vmnic0 que se conecta a la subred privada portátil A en la VLAN de almacenamiento. El volumen vmk4 tiene a vmnic2 que se conecta a la subred privada portátil B en la VLAN de almacenamiento. El servidor QuantaStor también tiene dos adaptadores de red privada, eth4 y eth6, que se conectan a la VLAN de almacenamiento.

### Configuración de redes

1. Abra un navegador web y vaya a la dirección IP de QuantaStor que aparece en la página **Dispositivos** en [{{site.data.keyword.slportal_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window}.
2. Indique el **Nombre de usuario administrativo** y la **Contraseña** (aparecen en el apartado Contraseñas de la página **Detalles de dispositivo**). Antes de continuar, observe los dispositivos de red privada que utiliza el servidor QuantaStor, como por ejemplo eth4.
3. Vaya a **Storage System > Network Ports**.
4. Seleccione el adaptador privado que esté activo (ejemplo: eth4) en la lista de adaptadores de red. Pulse con el botón derecho del ratón y seleccione **Modify Network Port** en el menú emergente.
5. Desmarque el recuadro de selección **iSCSI Enabled** para inhabilitar las conexiones de iSCSI a este adaptador y pulse **OK**.
6. Seleccione el adaptador privado que no esté activo, pero sí asignado a la red privada (por ejemplo, eth6).
7. Pulse con el botón derecho del ratón en el adaptador eth6 y seleccione **Modify Network Port** en el menú emergente.
8. Seleccione **Static** en **Config Type** en la pantalla **Modify Network Port**.
9. Especifique una dirección IP privada primaria, una subred y una pasarela para el adaptador. Utilice una dirección de la fila de almacenamiento si está utilizando la hoja de trabajo de VLAN del cookbook de [Arquitectura avanzada de referencia de VMware de un solo sitio](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html).
10. Desmarque el recuadro de selección **iSCSI Enabled** para inhabilitar las conexiones de iSCSI a este adaptador.
11. Pulse el adaptador privado y seleccione **Enable Network Port** para conectar el adaptador después de configurarlo con una dirección IP.
12. Pulse **OK** para habilitar el puerto una vez verificada la dirección IP.

### Cómo abrir una incidencia de soporte

Debe abrir una incidencia de soporte después de configurar un segundo adaptador con una dirección IP privada primaria. Abrir la incidencia permite garantizar que no se ocupe la dirección IP que ha utilizado si se suministra otra máquina en la VLAN.

1. Pulse **Soporte** > **Añadir incidencia** y especifique la siguiente información:
  * Asunto: pregunta de red privada
  * Título: Solicitud de reserva y asignación de dirección IP privada
  * Dispositivos asociados: 'Seleccione el servidor QuantaStor'
  * Detalles: Reserva y asignación de VLAN. Esta dirección IP se utiliza para el segundo adaptador en el servidor QuantaStor.

### Configuración de QuantaStor

Ahora que la matriz acepta conexiones de ambos adaptadores, se deben asignar las interfaces virtuales de los adaptadores que están en las subredes Storage Path A y Storage Path B.

  1. Pulse la interfaz de adaptador privado inicial (eth4) y seleccione **Create Virtual Interface** en el menú emergente.
  2. Especifique una dirección IP privada portátil y una subred para el adaptador en la pantalla emergente resultante, y asegúrese de que **iSCSI Enabled** esté marcado.
  3. Utilice una dirección de la fila Storage Path A si está utilizando la hoja de trabajo de VLAN.
  4. Anote la dirección IP que se utiliza en la sección de notas en la página de la dirección IP portátil.
  5. Seleccione la interfaz de adaptador privado inicial (eth4) para enlazar la interfaz virtual y pulse **OK**.
  6. Pulse la otra interfaz de adaptador privado (eth6) y seleccione **Create Virtual Interface** en el menú emergente.
  7. Especifique una dirección IP privada portátil y una subred para el adaptador y asegúrese de que **iSCSI enabled** esté marcado en la pantalla emergente resultante.
  8. Utilice una dirección de la fila Storage Path B si está utilizando la hoja de trabajo de VLAN.
  9. Anote esta dirección IP como utilizada en la sección de notas en la página de la dirección IP portátil.
  10. Seleccione la otra interfaz de adaptador privado (eth6) para enlazar la interfaz virtual y pulse **OK**.

Una vez que el servidor QuantaStor está configurado con las direcciones IP y las interfaces virtuales, debe configurar el direccionamiento para asegurarse de que el tráfico saliente utilice la interfaz correcta (porque hay dos NIC en subredes distintas).

1. Conéctese al servidor QuantaStor mediante SSH con sus credenciales de usuario root y añada las líneas siguientes a /etc/network/interfaces. Suponiendo que eth4 y eth6 sean los NIC de la red privada:
  * post-up ip route add 10.0.0.0/8 via dev eth4
  * post-up ip route add 10.0.0.0/8 via dev eth6 table eth6
  * post-up ip rule add from table eth6

### Creación de una agrupación de almacenamiento

A continuación, para poder crear volúmenes o comparticiones, debe crear una agrupación de almacenamiento que se utilice para asignar volúmenes.

1. Pulse el botón derecho del ratón en **Storage Pools** y seleccione **Create Storage Pool**.
2. Especifique la información siguiente en la pantalla **Create Storage Pool**:
  * Name: indique el nombre correspondiente a la agrupación de almacenamiento. Ejemplo: StoragePool-01
  * Pool Type: Default (zfs)
  * I/O Profile: Virtualization
  * Disks to Utilize for the Storage Pool: sdb
3. Pulse **OK**.

Si sdb no está disponible para añadir a una agrupación, se debe a que existe una partición que está etiquetada como arrancable. Debe utilizar gdisk en la consola de Quantastor para eliminar la partición y las entradas /etc/fstab. A continuación, debe crear volúmenes para ESXi.

### Creación de volúmenes de almacenamiento de iSCSI

Debe crear dos volúmenes de almacenamiento. Un volumen se utiliza para las VM de gestión en el clúster de gestión y el otro para las VM en el clúster de capacidad. Siga estos pasos para crear los volúmenes de almacenamiento de iSCSI:

1. Pulse el botón derecho del ratón en **Storage Volumes** y seleccione **Create Storage Volume** en el menú emergente.
2. Especifique la información para los volúmenes de almacenamiento. **Nota:** Aunque la configuración puede variar en función de la capacidad de almacenamiento y la carga de trabajo, el ejemplo muestra los valores en la Tabla 1 y la Tabla 2 para cada volumen de almacenamiento.

|Campo|Valor|
|---|---|
|Nombre|Mgmt-LUN0|
|Agrupación de almacenamiento|[Nombre de la agrupación de almacenamiento configurado en el paso anterior]|
|Tamaño|500 GB|
|% reservado|50|
|Compresión|Habilitada|
{: caption="Tabla 1. Volumen de gestión de iSCSI" caption-side="top"}

|Campo|Valor|
|---|---|
|Nombre|Capacity-LUN0|
|Agrupación de almacenamiento|[Nombre de la agrupación de almacenamiento configurado en el paso anterior]|
|Tamaño|3 TB|
|% reservado|50|
|Compresión|Habilitada|
{: caption="Tabla 2. Volumen de capacidad de iSCSI" caption-side="top"}

### Asignación de acceso de host a los volúmenes

Debe configurar QuantaStor para permitir el acceso desde los hosts de ESXi a través del IQN de cada host una vez configurados los volúmenes.

1. Vaya a la página de administración de QuantaStor, pulse con el botón derecho del ratón sobre el menú **Hosts** y seleccione **Add Host**.
2. Especifique la información siguiente en la pantalla **Add Host**:
  * Host Name: especifique un nombre de host adecuado. El nombre de host no tiene el FQDN (nombre de dominio totalmente calificado), pero debe describir el host. Ejemplo: MyESXiHostName
  * Operating System Type: VMware
  * Initator: botón de selección iSCSI Qualified Name (IQN)
  * iSCSI Qualified Name: el IQN del host correspondiente.
3. Pulse **OK**.

Siga estos pasos para cada host de gestión y capacidad del entorno de ESXi.

Una vez que haya añadido todos los hosts de los clústeres de gestión y capacidad, siga estos pasos:

1. Pulse con el botón derecho del ratón en el menú **Host Groups** y seleccione **Create Host Group…**.
2. Especifique 'ManagementCluster' en el campo **Name** y seleccione todos los hosts que haya en el clúster de gestión.
3. Pulse **OK**. Se creará un grupo de hosts que podremos asignar a un volumen determinado.

Repita este proceso para el clúster de capacidad.

1. Pulse el menú **Storage Volumes**.
2. Pulse con el botón derecho del ratón en el volumen **Mgmt-Lun0** y seleccione **Assign/Unassign Host Access**.
3. Confirme que **Mgmt-Lun0** es una opción en el menú desplegable y seleccione el grupo de hosts que ha creado en el paso anterior. Esta opción permite que cada host de ESXi del clúster de gestión pueda acceder al volumen Mgmt-Lun0. Haga lo mismo para **Capacity-LUN0**.

## Paso 4: Montaje de volúmenes en clústeres de gestión/capacidad

Inicie sesión en vSphere Web Client y vaya a **Hosts** en **vCenter Inventory Lists**.

Efectúe los pasos siguientes para montar el volumen en los hosts de ESXi:

1. Seleccione un host y pulse **Manage, Storage,** > **Storage Adapters**.
2. Seleccione **Targets** > **Dynamic Discovery** > **Add…**.
3. Especifique la dirección IP asignada al dispositivo de almacenamiento QuantaStor en Storage Path A en la pantalla **Add Send Target Server**.
4. Deje **3260** como puerto y pulse **OK**.
5. Pulse **Dynamic Discovery** > **Add…**. Repita los pasos 4 y 5 para Storage Path B.

El host de ESXI está listo para reescanear el adaptador de software iSCSI para descubrir el volumen Mgmt-Lun0.

1. Seleccione el icono **Rescan Storage Adapters** (Figura 9) en la pantalla **Storage Adapters**.
2. Deje la opción predeterminada en la pantalla emergente resultante y pulse **OK**.
3. Una vez descubierto el volumen, pulse **Actions, New Datastore** y formatéelo como **VMFS-5**.
4. Confirme que el formato finalice y pulse **Storage Devices, Device Details, Edit Multipathing…**.
5. Seleccione **Round Robin** en **Path Selection Policy** y pulse **OK**.

Ahora que el volumen Mgmt-Lun0 está conectado a un solo host, debe volver a los otros hosts de gestión del clúster y repetir el proceso para añadir el volumen. Sin embargo, no es necesario formatear el volumen, porque ya está formateado como VMFS-5 y se muestra así tras el descubrimiento.

## Paso 5: Inhabilitación del ACK retardado en los hosts de vSphere ESXi

Es necesario inhabilitar el ACK retardado una vez que los LUN de almacenamiento se han conectado a los hosts de gestión y capacidad.

1. Vaya al entorno de vSphere y seleccione **Storage Adapters** > **iSCSI Software Adapter** > **Advanced Options**.
2. Pulse **Edit** y desplácese al final de la pantalla Advanced Options.
3. Desmarque el recuadro de selección **DelayedAck** y pulse **OK**.

Para obtener más información sobre el ACK retardado en relación con VMware, consulte la [Base de conocimiento de VMware](https://kb.vmware.com/s/article/1002598).

Ahora puede volver al cookbook de [Arquitectura avanzada de referencia de VMware de un solo sitio](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) y completar la configuración del entorno.
