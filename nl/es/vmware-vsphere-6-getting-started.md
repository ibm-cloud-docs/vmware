---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a VMware vSphere 6 

Efectúe los pasos siguientes para empezar a trabajar con vSphere 6.

## Entorno y configuración

Para optimizar la solución de VMware, se recomienda que utilice una red VLAN privada y un puerto público (opcional, el puerto público se puede inhabilitar si no es necesario) para el entorno de VMware vSphere. Este perfil de suministro permite los límites siguientes de tráfico de segmento de Capa 2:

|Ejemplo de ID de VLAN|Descripción|Tipo|Detalle adicional|
|---|---|---|---|
|VLAN1 - **1101**|Gestión, VxLAN|BCR privado|VLAN nativa sin etiquetas, VLAN nativa original en la que se despliegan los hosts de VMWare en el momento del pedido|
|VLAN4 - **2200**|DMZ de acceso a Internet público|FCR público|VLAN nativa sin etiquetas, VLAN nativa original en la que se despliegan los hosts de VMWare en el momento del pedido|
{: caption="Tabla 1. Ejemplos de VLAN pública y privada" caption-side="top"}

## Cómo realizar un pedido de servidores de vSphere
1. Inicie sesión en el [{{site.data.keyword.slportal_full}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window}.
2. Pulse **Cuenta > Realizar un pedido**.
3. En la sección **Servidor nativo**, pulse **Mensual**.
4. Seleccione los servidores. Consulte los requisitos mínimos en las publicaciones de soporte de VMware:
  * Los servidores siguientes se han seleccionado para el ejemplo. **Nota:** Tener enlaces ascendentes duales públicos y privados no vinculados es un requisito para la redundancia. Confirme que el centro de datos donde ha creado las VLAN tiene enlaces ascendentes no vinculados.  
  * Clúster de capacidad (Cantidad: 2)
    * Configuración de servidor: seleccione un servidor Intel Xeon v3 de la sección 'Servidores de varios núcleos de procesador dual'
    * Software: SO = vSphere Enterprise Plus 6
    * Almacenamiento de SO: 2 x SATA de 1 TB (configurado como RAID 1)
    * Almacenamiento de datos: se recomienda SATA de 2 TB o SSD de 1,2 TB o almacenamiento SAN NFS de Resistencia/Rendimiento
      * Si está interesado en otros tipos de almacenamiento, consulte [Almacenamiento para utilizar con sistemas VMware](select-storage-option-use-vmware.html)
      * Velocidades de puerto de enlace ascendente: redes públicas y privadas duales a 1 Gbps (desvinculadas)
        * Para las soluciones VMware vSAN, se recomiendan enlaces ascendentes de 10 Gbps
5. Si va a crear un nuevo despliegue en un nuevo centro de datos de IBM Cloud, continúe con el paso 6. Si se trata de una expansión o un despliegue en un centro de datos existente, seleccione la VLAN de BCR de fondo y la VLAN de FCR frontal que prefiera. Para el ejemplo, la VLAN de BCR de fondo es 1101 y la VLAN de FCR frontal es 2200. **Nota:** Si se trata de un nuevo despliegue o un nuevo despliegue en un nuevo DC, las VLAN BCR de fondo y FCR frontal se crean cuando se solicita el servidor.
6. Escriba un **Nombre de host** y un **Dominio**.
7. Revise el pedido y pulse **Finalizar el pedido** para iniciar el proceso de suministro.

## Cómo realizar el pedido de vCenter Server

vCenter es un complemento de Windows Server. Esta configuración se amplía hasta 20 hosts de vSphere. Para mayores implementaciones, se recomienda el despliegue de vCenter Server Appliance (vCSA) [Desplegar y configurar vCenter Server Appliance (vCSA)](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html) directamente en un clúster de vSphere.

Efectúe los pasos siguientes para solicitar un servidor virtual con vCenter instalado:

1. Inicie sesión en el {{site.data.keyword.slportal_short}}.
2. Pulse **Cuenta > Realizar un pedido**.
3. Solicite una instancia de nodo público/privado de servidor virtual (VSI) o un servidor nativo **Mensual** en Servidores virtuales.
  1. Para que una VSI (instancia de servidor virtual) de SoftLayer cumpla los requisitos para vCenter 6.0, debe desplegar en un mínimo de **4 x núcleos de 2,0 GHz** y **4 GB de RAM**
  2. Para obtener un listado de recomendaciones de despliegue de vCenter, consulte la [Guía de despliegue de VMware vCenter Server&trade; 6.0 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}.
4. Especifique la información siguiente:
  * Con base en la configuración de servidor mínima recomendada
    * Configuración de núcleo de vCPU: 4 x núcleos de 2,0 GHz
    * Configuración de RAM: 12 GB de RAM
    * Software: SO = Windows Server 2012 R2 Standard Edition (64 bits)
    * Complemento específico de SO: vCenter 6
    * Primer disco: 1 x 100 GB (SAN)
    * Segundo disco: 1 x 50 GB (SAN)
    * Velocidades de puerto de enlace ascendente: enlaces ascendentes de red pública y privada a 1 Gbps

5. Si se trata de un nuevo despliegue en un nuevo centro de datos de IBM Cloud, continúe con el paso 6. Si es despliegue es una expansión o un despliegue en un centro de datos existente, seleccione la VLAN de BCR de fondo y la VLAN de FCR frontal que prefiera. Para nuestro ejemplo, la VLAN de BCR de fondo es 1101 y la VLAN de FCR frontal es 2200. (Si se trata de un nuevo despliegue o un nuevo despliegue en un nuevo DC, las VLAN BCR de fondo y FCR frontal se crean cuando se solicita el servidor).
6. Escriba un **Nombre de host** y un **Dominio**.
7. Revise el pedido y pulse **Finalizar el pedido** para iniciar el proceso de suministro.

## Solicitud de direcciones IP/subredes portátiles públicas y privadas

**Nota:** No continúe si las VLAN no se han suministrado completamente.

Las subredes se utilizan para direccionar el tráfico basado en kernel de host de VMware y máquina virtual (VM) de invitado de VMware.

1. En el portal de control, pulse **Red > Gestión de IP > Subredes**.
2. Pulse **Pedir direcciones IP** en la parte superior derecha de la pantalla.
3. Seleccione **Privada portátil**.
4. Seleccione la VLAN apropiada (ejemplo: bcr01.wdc04: 1101)
5. Pulse **Continuar**.
6. Rellene el formulario de **solicitud de dirección IP**.
7. Pulse **Pedir direcciones IP** en la parte superior derecha de la pantalla.
8. Pulse **Realizar pedidos**.
9. Siga este proceso para cada VLAN aplicable (ej.: 1101, 2200)
  1. Para obtener más información sobre las VLAN, consulte [Iniciación a VLAN](/docs/infrastructure/vlans/getting-started.html).

|Tipo de subred|Tamaño de subred|Vlan enlazada|Uso de host de vSphere|
|---|---|---|---|
|Privada - portátil|dirección /27 32|**1101**|VM de gestión|
|Privada - portátil|dirección /27 32|**1101**|Puertos de kernel de VM para iSCSI y vMotion|
|Privada - portátil|dirección /27 32|**1101**|IP privadas para VM de invitado|
|Pública - portátil|dirección /27 32|**2200**|IP públicas para VM de invitado (opcional)|
{: caption="Tabla 2. Subredes" caption-side="top"}

### Opcional: Inhabilite la interfaz pública en el host de vSphere

Puede inhabilitar las interfaces públicas de vSphere con fines de seguridad si no va a utilizarlas.

1. En el portal de control, pulse **Dispositivos > Lista de dispositivos**.
2. Pulse el nombre del host de vSphere.
3. Pulse la tabla de configuración y desplácese hasta la sección de red.
4. Seleccione **Desconectar** para cada par de hosts eth1 y eth3 de vSphere aplicable para todos los hosts.

Esta acción también se puede realizar mediante la [{{site.data.keyword.slapi_full}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window}.

## Creación y configuración de clúster de centro de datos de vSphere <!-- create and configure should be separate tasks-->

Ahora puede iniciar sesión en el servidor de vCenter Server y configurar el clúster de vSphere.

1. En el portal de control, pulse **Dispositivos > Lista de dispositivos**.
2. Busque el dispositivo de vCenter y pulse su nombre.
3. Desplácese por la pantalla **Detalles de dispositivo** hasta la sección **Red** del servidor y anote la **Dirección IP privada**.
4. Desplácese por la pantalla **Detalles de dispositivo** y anote las **Contraseñas** para el sistema operativo Windows y el software vCenter.
5. Abra una sesión de Microsoft Remote Desktop (RDP) y conéctese a su servidor de vCenter Server a través de su dirección IP pública.
6. Inicie sesión con las contraseñas obtenidas en el paso 4. **Nota:** Será necesario tener una conexión VPN activa con IBM Cloud si se utiliza la dirección IP privada para acceder a vCenter. Para obtener más información sobre el acceso de VPN, consulte cómo [Habilitar el acceso a la red privada de la infraestructura de IBM Cloud](/docs/customer-portal/getting-started.html#enable-private-network).
7. Descargue e instale la versión tradicional de [vSphere Client ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window} o utilice vSphere Web Client a través del enlace `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/`.
8. Inicie sesión en vCenter con la dirección IP y las contraseñas que ha obtenido en los pasos 3 y 4.
9. Pulse con el botón derecho del ratón en el nombre de servidor de vCenter Server en el panel izquierdo y seleccione **New Datacenter**.
10. Especifique un nombre adecuado para el centro de datos.
11. Pulse con el botón derecho del ratón en el centro de datos y seleccione **New Cluster**.
12. Especifique un nombre de clúster. NO active las características de clúster, HA de vSphere ni DRS de vSphere en este momento.
13. Pulse **Next**.
14. Deje **EVC** inhabilitado y pulse **Next**.
15. Acepte los _valores predeterminados para almacenar el archivo de intercambio en el mismo directorio que la máquina virtual_ y pulse **Next**.
16. Pulse **Finish** para completar el clúster.
17. Pulse el nuevo clúster que acaba de crear y seleccione **Add Host**.
18. Especifique la dirección IP o el nombre de host de uno de los hosts de vSphere e indique **Root** en el campo **Username** y la contraseña para el host en el campo **Password**.
19. Pulse **Next** en las pantallas Host Summary, Assign License y Lockdown Mode y pulse **Finish** para acabar de añadir el host al clúster.
20. Repita los pasos 18 y 19 para cada uno de los demás hosts de vSphere en el clúster. Cuando acabe, verá todos los hosts de vSphere bajo el nuevo clúster.

### Configuración de la construcción de red básica para los hosts de vSphere

Efectúe los pasos siguientes para configurar la construcción básica para los hosts de vSphere en el clúster.

1. Seleccione el primer host de vSphere y pulse el separador **Configuration**.
2. En **Hardware**, seleccione **Networking**. Debe tener vSwitch0 con vmnic0; pulse **Properties** junto a vSwitch0.
3. Seleccione **Network Adapters** en la ventana **vSwitch Properties** y pulse el botón **Add**.
4. Seleccione vmnic2 para añadirlo a vSwitch0 y pulse **Next**.
5. Asegúrese de que ambos aparecen como **Active Adapters** y pulse **Next**.
6. Pulse **Finish**.
7. Pulse el separador **Ports** y asegúrese de que vSwitch está resaltado; pulse **Edit**.
8. Pulse el separador **General** y cambie **MTU** a 9000 (trama de gran tamaño).
9. Pulse el separador **NIC Teaming**, cambie el equilibrio de carga al hash **Route Based on IP** y pulse **OK**.
10. Efectúe los pasos 1 a 8 para configurar los vmnics para los demás hosts de vSphere del clúster.

Ahora es necesario añadir un grupo de puertos para vMotion. El grupo se puede crear como Virtual Standard Switch (VSS) o Virtual Distributed Switch (VDS). Para el propósito de nuestro ejemplo, crearemos un conmutador VSS.

1. Seleccione el separador **Configuration** y seleccione **Networking**.
2. Pulse **Properties...** en vSwitch0.
3. Pulse **Add...** para crear un grupo de puertos.
4. Seleccione **VMkernel** y pulse **Next**.
5. Rellene Port Group Properties con la información siguiente:
  * **Network Label:** un nombre adecuado para el grupo de puertos.
  * **VLAN ID (Optional):** el ID de VLAN para el tráfico vMotion (1101 para nuestro ejemplo). El ID de VLAN permitirá que VMware etiquete el tráfico para la VLAN específica.
  * Seleccione **Use this port group for vMotion**.
6. Pulse **Next**.
7. Especifique una **dirección IP portátil** para la VLAN. (Puede obtener la dirección IP del puerto en el portal de SoftLayer, **Red > Gestión de IP > VLAN**. Seleccione la VLAN, y bajo **Subredes**, verá un rango de direcciones IP portátiles. Si no hay ninguna dirección IP portátil disponible o si ha agotado la agrupación actual, siga los pasos de la sección 'Solicitud de direcciones IP/subredes' privadas para solicitar más direcciones IP portátiles).
8. Pulse **Next** y luego **Finish** para finalizar.

Efectúe los pasos siguientes para crear un grupo de puertos para el tráfico de datos de VM.

1. Pulse **Properties...** en vSwitch0 y seleccione **Add, Virtual Machine**.
2. Rellene **Port Group Properties** con la información siguiente:
  * **Network Label:** especifique el nombre del grupo de puertos, por ejemplo, VM Data.
  * **VLAN ID (Optional):** especifique un ID de VLAN; para nuestro ejemplo, hemos utilizado 1101. El ID de VLAN permite a VMware etiquetar el tráfico para la VLAN.

### Opcional: Instale licencias de complementos de VMware (NSX, vRealize, vSAN, etc.)

Ahora que el entorno de VMware está listo, puede continuar con el despliegue de configuraciones adicionales, VM de invitado o complementos de VMware. Las licencias para los complementos de VMware también se pueden adquirir a través del portal de control de IBM Cloud y se pueden añadir a través de la consola de vCenter. Para obtener más información sobre la solicitud y la gestión de licencias de complementos de VMware, consulte [Solicitud y gestión de licencias de VMware vSphere 6](vmware-vsphere-6-ordering-and-managing-licenses.html).

## Pasos siguientes
Ya tiene un entorno básico de VMware de un solo sitio que se ejecuta en un centro de datos de IBM Cloud. La configuración básica sólo tiene un almacén de datos local, por lo que se trata de una configuración simplificada que no contiene características como DRS de VMware, HA o DRS de almacenamiento, ni cortafuegos.

Para obtener más información, consulte [Preguntas frecuentes: VMware](vmware-faq.html). 
