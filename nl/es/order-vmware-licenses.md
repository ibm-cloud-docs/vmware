---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Solicitud de licencias de VMware

Los administradores de VMware saben que pueden aprovechar rápidamente las rentables características de la nube híbrida desplegando en {{site.data.keyword.BluSoftlayer_full}}. Una de esas características es que los catálogos y las cargas de trabajo de vSphere se suministran en entornos de VMware vSphere en centros de datos de {{site.data.keyword.cloud_notm}} sin modificar invitados ni VM de VMware. El uso de una plataforma de gestión/orquestación y un hipervisor de vSphere común hace posible estos despliegues.
{:shortdesc}

La implementación de vSphere también permite utilizar otros componentes. La tabla 1 contiene una lista de los productos de VMware que están disponibles por medio del {{site.data.keyword.slportal}}. La información de precios se puede encontrar en [Soluciones IBM Cloud for VMware](http://www.softlayer.com/vmware-solutions).

|Nombre de producto|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard Tier 1 (0 - 20 TB)|
|Virtual SAN Standard Tier 2 (21 - 64 TB)|
|Virtual SAN Standard Tier 3 (65 - 124 TB)|
|VMware Site Recovery Manager (SRM)|
{: caption="Tabla 1. Productos de VMware disponibles en el Portal de clientes" caption-side="top"}

Efectúe los pasos siguientes para solicitar licencias para los productos de VMware que se listan en la Tabla 1:
1. Inicie sesión en el [{{site.data.keyword.slportal_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://control.softlayer.com/){: new_window}.
2. Pulse **Dispositivos > Gestionado > Licencias de VMware**.
3. Pulse **Pedir licencias de VMware** en la esquina superior derecha.
4. Pulse la lista desplegable bajo **Añadir licencia** para listar los productos de VMware y el número de CPU para las licencias que desea solicitar.
  * **Nota:** VMware vSphere Enterprise Plus (ESXi 6.0) no se solicita mediante este proceso. Se pide como un sistema operativo solicitado al pedir el servidor nativo.
5. Puede ver el precio del producto de VMware que ha seleccionado en la parte más a la derecha de la pantalla.
6. Pulse **Continuar** para pedir las licencias o pulse **Añadir licencia** para añadir más licencias.
  * Cuando pulse **Continuar**, se le dirigirá a la página **Licencias de VMware**, que muestra los productos de VMware y las claves de licencia.
7. Descargue los **archivos de instalación** desde el enlace que se proporciona. Debe tener una conexión SSL a la red privada de IBM Cloud para acceder a la página de descarga.
8. Descargue los productos de VMware correctos e instálelos manualmente en el entorno de vSphere.
