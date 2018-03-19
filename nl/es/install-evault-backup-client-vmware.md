---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Instalación del cliente de copia de seguridad de EVault para VMware

Se puede instalar el cliente de copia de seguridad de EVault en un servidor VMware mediante una serie de mandatos en el shell o terminal del servidor ESX de destino. Este procedimiento describe los pasos necesarios para instalar el cliente de copia de seguridad de EVault en el servidor VMware:
{:shortdesc}

Para instalar el agente, descargue y copie el paquete `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` en el servidor ESX de destino utilizando el mandato siguiente:

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**Nota:** Debe realizar los pasos siguientes localmente en el servidor ESX de destino.

1. Extraiga los archivos del paquete. Para ello, utilice este mandato (en el que “PACKAGENAME” puede ser "Agent-VMware-ESX-Server-6.71"):<br/>`tar xvfz PACKAGENAME.tar.gz`
2. Vaya al directorio donde ha extraído el paquete.
3. Ejecute el script de instalación:<br />`# ./install.sh`<br/><br/>
**Nota:** El script de instalación le solicitará de forma interactiva la información de configuración, como el registro web (dirección, número de puerto y autenticación) y el nombre del archivo de registro.

Especifique el nombre de usuario de WebCC para este servidor.

4. Especifique el **nombre de usuario de copia de seguridad de EVault** en la solicitud del nombre de usuario de WebCC. Consulte cómo [Ver los detalles de almacenamiento de copia de seguridad de EVault](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal) para obtener las instrucciones para ver el nombre de usuario de la copia de seguridad de EVault.
5. Especifique la contraseña de copia de seguridad de EVault en la solicitud de la contraseña de WebCC.
6. Cuando finalice la instalación, aparecerá un mensaje de finalización y se ejecutará el daemon del agente.


Otras notas de instalación:<br/>
Si la instalación se realiza correctamente, el archivo Install.log estará en el directorio de instalación.<br/>
Por ejemplo: `/opt/BUAgent/Install.log`

Si la instalación falla y se retrotrae, el registro de instalación estará en `<Installation Failure directory>.`<br/>
Si la instalación falla y no se retrotrae, el registro de instalación estará en `<Installation Kit directory>`.<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
Conéctese a la VPN de {{site.data.keyword.BluSoftlayer_full}} para ver el enlace anterior. Para obtener más información sobre cómo conectarse a la VPN de IBM Cloud, consulte cómo [Habilitar el acceso a la red privada de la infraestructura de IBM Cloud](/docs/customer-portal/getting-started.html#enable-private-network)).
