---

copyright:
  years: 1994, 2022
lastupdated: "2022-08-15"

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
   * For more information about required system resources, see [Minimum requirements for the VMware vCenter Server Appliance](https://kb.vmware.com/s/article/2106572){: external}.
* vCSA ISO Image
* Ability to mount an ISO
* VPN session with access to {{site.data.keyword.cloud}} Private Network

**Deploying and configuring a vCenter Server Appliance**

1. Mount vCenter Server Appliance (vCSA) ISO.
2. Open `vcsa-setup.html` in a compatible browser.
3. Review and accept the installation of the VMware client integration plug-in.
4. Click **Allow** > **Install**
5. Review and accept terms of the license agreement and click **Next**.
6. Enter the FQDN or Private IP address and username and password of the VMware Host that you want to install the vCSA. Click **Next**.
7. Click **Yes** to accept the certificate warning.
8. Enter an appropriate appliance name and password and click **Next**.
9. For the deployment type, select 'Install vCenter server with an Embedded Platform Services Controller', then click **Next**.
10. Click **Create an SSO domain** > **Next**. 
11. Choose an appliance size and click **Next**.
12. Select a data store and click **Next**.
13. Select 'Use an embedded database (PostgreSQL)' and click **Next*.
14. Set up your network configurations by entering the following information:
    *  Network
    * IP address family
    * Network type
    * Network address
    * System name
    * Subnet mask
    * Network gateway
    * Network DNS Servers. For more information, see [What are Local DNS Resolvers](/docs/dns?topic=dns-dns-faq#what-are-the-local-dns-resolvers-).
    * Configure time sync
    * Click **Next**
15. Review the settings, then click **Finish**. Your vCSA instance is provisioned.

