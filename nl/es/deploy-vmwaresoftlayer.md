---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Uso de cookbooks para despliegues de VMware

Los administradores de VMware pueden aprovechar rápidamente las rentables características de la nube híbrida desplegando en la nube global de nivel empresarial de {{site.data.keyword.BluSoftlayer_full}}. Se pueden suministrar catálogos y cargas de trabajo de vSphere en entornos de VMware vSphere en centros de datos de {{site.data.keyword.cloud_notm}} sin modificar invitados ni VM de VMware. Estos despliegues son posibles gracias al uso de una plataforma de gestión/orquestación y un hipervisor de vSphere común. Las implementaciones de vSphere también pueden aprovechar otros componentes de la suite de VMware vCloud: vCloud Automation Center, vCenter Operations Management Suite, vSAN, vCloud Network & Security, Site Recovery Manager, vCenter Orchestrator y NSX.

El objetivo principal de la serie de cookbooks de VMware es ayudar a los administradores de vSphere con el despliegue de entornos de VMware vSphere dentro de una infraestructura de IBM Cloud. Los cookbooks no están destinados a servir como formación sobre cómo administrar vSphere. Para obtener más información sobre la administración de vSphere, consulte la [Formación de VMware ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}.

{{site.data.keyword.cloud_notm}} tiene varias funciones específicas que dan a los administradores de VMware la flexibilidad de utilizar instancias nativas y construcciones de copia de seguridad y recuperación, red y almacenamiento en forma de autoservicio. Puede utilizar estas construcciones para desplegar implementaciones de vSphere totalmente funcionales, que se pueden crear para ampliar o sustituir las implementaciones de vSphere locales (VMware@Home).

Los cookbooks siguientes están disponibles para los administradores:

* [Crear un entorno de VMware de un solo sitio](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html): como administrador de vSphere, se explican los pasos para crear el entorno, incluido el uso de QuantaStor o del almacenamiento en bloque de Resistencia o Rendimiento.
* [Migrar cargas de trabajo de vSphere ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window}: presenta casos de ejemplo para ayudarle a migrar las cargas de trabajo [máquinas virtuales (VM)] a VMware una vez que la implementación de vSphere está desplegada en un centro de datos de IBM Cloud.
* [Aprovechar NSX® ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window}: puede utilizar VMware NSX para proporcionar construcciones de SDN (redes definidas por software) a despliegues de VMware@SoftLayer.
* [ECX de Catalogic ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window}: puede gestionar y analizar datos de copia en una infraestructura de TI híbrida. La infraestructura se despliega en la infraestructura de IBM Cloud mediante ECX, la plataforma inteligente de gestión de datos de copia de Catalogic Software, y mediante infraestructura de VMware vSphere y NetApp Private Storage.
* [Copia de seguridad de VMware ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window}: este cookbook describe enfoques alternativos para la copia de seguridad, la recuperación y el archivado de cargas de trabajo basadas en VMware (VM) que se ejecutan en un despliegue de VMware.
* [Recuperación tras desastre de VMware ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window}: en este cookbook se detallan dos casos prácticos que establecen una solución de recuperación tras desastre (DR) mediante VMware. El primero trata sobre un entorno de VMware local que permite recuperar una carga de trabajo local, o viceversa. El segundo es la recuperación de cargas de trabajo de VMware en un segundo centro de datos de {{site.data.keyword.cloud_notm}}.
* [Cifrado de Vormetric de VMware ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window}: casos prácticos que ilustran cómo Vormetric protege las cargas de trabajo de VMware cifrando los datos de las VM.
* [Desplegar una solución de nube fiable con IBM, VMware y HyTrust ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window}: puede integrar los diversos elementos arquitectónicos para crear una cadena de confianza desde el hardware hasta el hipervisor y las aplicaciones de gestión.


**Nota:** Los cookbooks están destinados a administradores experimentados de vSphere. En algunos de los temas que se tratan se presupone que el lector tiene conocimientos básicos de despliegue para instalar y configurar vSphere y vCenter.
