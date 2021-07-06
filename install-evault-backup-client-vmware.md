---

copyright:
  years: 1994, 2021
lastupdated: "2018-11-15"

keywords: install evault backup client

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Installing EVault Backup client for VMware
{: #install-evault-client}

Installing the EVault Backup client on a VMware&reg; server can be done through a series of commands in the shell or terminal within the target ESX server. Use the following steps are to install the EVault Backup client on your VMware&reg; server.
{:shortdesc}

To install the Agent, download and copy the `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` package onto the target ESX Server by using the following command:

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**Note:** You must perform the following steps locally on the target ESX Server.

1. Extract the files from the package. To do so, use this command (in which “PACKAGENAME” might be “Agent-VMware-ESX-Server-6.71”):<br/>`tar xvfz PACKAGENAME.tar.gz`
2. Go to the directory where you extracted the package.
3. Run the installation script:<br />`# ./install.sh`<br/><br/>
  The installation script prompts you for configuration information such as web registration (address, port number, and authentication) and log file name.
  {:note}

Enter the WebCC username for this server.

4. Enter the **EVault Backup username** for the WebCC username. For more information about viewing your EVault Backup name, see [Accessing and viewing IBM Cloud Backup storage details in the Console](/docs/infrastructure/Backup?topic=Backup-GettingStarted#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal).
5. Enter the EVault Backup Password as the input for the prompt that requests the WebCC password.
6. When the installation finishes, a completion message appears, and the Agent daemon runs.


Other Installation Notes:<br/>
The _install.log_ is in the installation directory if the installation is successful.<br/>
For example, `/opt/BUAgent/Install.log`

If the installation fails and rolls back, the installation log is in the `<Installation Failure directory>.`<br/>
If it fails and does not roll back, the installation log is in the `<Installation Kit directory>`.<br/>

Make sure that you are connected to the {{site.data.keyword.BluSoftlayer_full}} VPN to view the User Guide. For more information about connecting to the IBM Cloud VPN, see [Getting started with IBM Cloud Virtual Private Networking](/docs/iaas-vpn?topic=iaas-vpn-getting-started)).
