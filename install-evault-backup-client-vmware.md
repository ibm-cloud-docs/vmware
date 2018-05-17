---
copyright:
  years: 1994, 2017
lastupdated: "2018-05-17"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Installing EVault Backup Client for VMware

Installing the EVault Backup client on a VMware server can be done through a series of commands in the shell or terminal within the target ESX server. This procedure outlines the steps required to install the EVault Backup client on your VMware server:
{:shortdesc}

To install the Agent, download and copy the `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` package onto the target ESX Server using the following command:

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**Note:**  You must perform the following steps locally on the target ESX Server.

1. Extract the files from the package. To do so, use this command (in which “PACKAGENAME” could be “Agent-VMware-ESX-Server-6.71”):<br/>`tar xvfz PACKAGENAME.tar.gz`
2. Go to the directory where you extracted the package.
3. Run the installation script:<br />`# ./install.sh`<br/><br/>
**Note:**  The installation script will interactively prompt you for configuration information such as web registration (address, port number, and authentication) and log file name.

Enter the WebCC username for this server.

4. Enter the **EVault Backup Username** as the input for the prompt requesting the WebCC username. Refer to the [View EVault Backup Storage Details](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal) procedure for instructions to view the EVault Backup Username.
5. Enter the EVault Backup Password as the input for the prompt requesting the WebCC password.
6. When the installation finishes, a completion message will appear, and the Agent daemon will be running.


Other Installation Notes:<br/>
The Install.log will be in the installation directory if the installation has succeeded.<br/>
For example: `/opt/BUAgent/Install.log`

If the installation fails and rolls back, the installation log will be in the `<Installation Failure directory>.`<br/>
If it fails and does not roll back, the installation log will be in the `<Installation Kit directory>`.<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
Be sure that you are connected to the {{site.data.keyword.BluSoftlayer_full}} VPN to view the User Guide. For more information about connecting to the IBM Cloud VPN, see [Enable access to the IBM Cloud infrastructure private network](/docs/customer-portal/getting-started.html#enable-private-network)).
