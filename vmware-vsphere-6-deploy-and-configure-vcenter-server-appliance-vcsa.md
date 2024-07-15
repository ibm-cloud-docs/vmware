---

copyright:
  years: 1994, 2024
lastupdated: "2024-07-15"

keywords: deploy vcsa, vsphere

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Deploying and configuring a vCenter Server Appliance (vCSA) with VMware vSphere
{: #config-vcsa}

Use the following steps to deploy a VMware&reg; vCenter Server Appliance.
{: shortdesc}

**Prerequisites**

* Windows&reg; system with a compatible browser installed
   * Internet Explorer, Firefox, or Chrome
* vSphere Hosts with adequate resources to support a VMware vCenter Server Appliance
* vCSA ISO Image
* Ability to mount an ISO
* VPN session with access to {{site.data.keyword.cloud}} Private Network

## Deploying and configuring a vCenter Server Appliance**
{: #deploying-and-configuring-vcsa}

1. Mount vCenter Server Appliance (vCSA) ISO.
1. Open `vcsa-setup.html` in a compatible browser.
1. Review and accept the installation of the VMware client integration plug-in and click **Allow** > **Install**
1. Review and accept the terms of the license agreement and click **Next**.
1. Enter the FQDN or Private IP address and username and password of the VMware Host that you want to install the vCSA. Click **Next** > **Yes** to accept the certificate warning.
1. Enter an appropriate appliance name and password and click **Next**.
1. For the deployment type, select _Install vCenter server with an Embedded Platform Services Controller_, then click **Next**.
1. Click **Create an SSO domain** > **Next**.
1. Choose an appliance size and click **Next**.
1. Select a data store and click **Next**.
1. Select 'Use an embedded database (PostgreSQL)' and click **Next**.
1. Set up your network configurations by entering the following information:
    * Network
    * IP address family
    * Network type
    * Network address
    * System name
    * Subnet mask
    * Network gateway
    * Network DNS Servers
    * Configure time sync
1. Click **Next** to review the settings. Then, click **Finish**.

Your vCSA instance is provisioned.
