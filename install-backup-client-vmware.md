---

copyright:
  years: 1994, 2019
lastupdated: "2018-12-14"

keywords: EVault Backup Client, installation script, VMware server, VMware client

subcollection: vmware

---
{:new_window: target="_blank"}
{:tip: .tip}
{:note: .note}
{:pre: .pre}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}

# Installing {{site.data.keyword.backup_notm}} Client for VMware
{: #install-vmware-client}

Installing the {{site.data.keyword.backup_full}} client on a VMware server can be done through a series of commands in the shell or terminal within the target ESX server.

1. Download and copy the `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` package onto the target ESX Server by using the following command.
   ```
   wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz
   ```
   {: pre}

   You must perform the following steps locally on the target ESX Server.
   {: important}

2. Extract the files from the package. Replace the `PACKAGENAME` with `Agent-VMware-ESX-Server-6.71`.<br/>
   ```
   tar xvfz PACKAGENAME.tar.gz
   ```
   :{pre}

3. Go to the directory where you extracted the package.
4. Run the installation script.

   ```
   ./install.sh
   ```
   {: pre}

   The installation script interactively prompts you for configuration information such as web registration (address, port number, and authentication) and log file name.
   {: note}

5. Enter the {{site.data.keyword.backup_notm}} user name as the input for the prompt requesting the WebCC user name. Refer to the [Accessing and viewing IBM Cloud Backup storage details](https://{DomainName}/docs/infrastructure/Backup/index.html#accessing-and-viewing-ibm-cloud-backup-storage-details) procedure for instructions to view the user name that is associated with the {{site.data.keyword.backup_notm}} service.

6. Enter the EVault Backup Password as the input for the prompt requesting the WebCC password.

7. When the installation finishes, a completion message appears, and the Agent daemon starts running.


If the installation was successful, the `Install.log` is in the installation directory.
For example: `/opt/BUAgent/Install.log`

If the installation fails and rolls back, the installation log is in the `<Installation Failure directory>`.

If it fails and does not roll back, the installation log is in the `<Installation Kit directory>`.

## Downloading the user guide
{: #download-user-guide}

Connect to the {{site.data.keyword.BluSoftlayer_full}} network with {{site.data.keyword.BluVPN}} so that you can access and download the user guide from [Downloadable {{site.data.keyword.backup_notm}} Documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window}
