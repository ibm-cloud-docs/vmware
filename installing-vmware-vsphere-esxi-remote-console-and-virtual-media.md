---

copyright:
  years: 1994, {CURRENT_YEAR}]
lastupdated: "2024-07-15"

keywords: virtual media, deploying esx, private network, remote console, install vsphere, install esxi, esxi

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Installing VMware vSphere ESXi with remote console and virtual media
{: #installing-vsphere-esxi}

Deploying ESX from installation media is similar across all versions.

## Requirements
{: #reqs-vsphere-esxi}

Make sure that the following requirements are met before you install VMware vSphere ESXi.

* A virtual server that has access to the private network
* Windows or Linux operating system with a Java-enabled browser that is accessible through the {{site.data.keyword.cloud}} VPN or public IP
* The virtual server must be on the same private network that Intelligent Platform Management Interface (IPMI) addresses are located
* A copy of VMware ESXi VIM Installer ISO

## Connecting to IPMI
{: #connecting-ipmi}

Use the following steps to connect to IPMI.

1. Upload the VMware ISO to the virtual server instance that is specified in the Requirements. The virtual server instance needs public web access.
2. Gather the IPMI address and login information from the customer portal.
3. Select **Devices** > **Device List** > **[Server]** > and the **Remote Management** tab.
4. Remote desktop (RDP) or Remote X into to the virtual server instance that is storing the ESXi image.
5. Open a web browser in the RDP session and enter the IPMI address that you collected in Step 2.
6. Log in to the IPMI console with the credentials that are also found in Step 2 (typically root).

   Make a note of your IPMI user access level. If your access level isn't **Administrator**, then you might experience a problem when you mount your remote storage. Open a support case to elevate your IPMI credentials if you cannot mount media.
   {: tip}

7. Confirm that you are on the home login page and click **Remote control** > **Console redirection** > **Launch console**.

## Attaching an ISO
{: #attaching-iso}

Use the following steps to attach an ISO.

1. On the Kernel-based Virtual Machine (KVM) viewer, click **Virtual media** > **Virtual storage**. Your operating system and Java version might require you to allow access to start the Java-based viewer.
2. Click the **CD and ISO** tab in the Virtual Storage window. For the Logical Drive Type, click **ISO file** > **Open image**.
3. Go to the ESXi ISO and click **OK**. Then, click **Plug-in**.
4. After the ISO plugs into the session, click **OK**.
5. Go back to the IPMI webpage and click **Remote** > **Control** > **Reset server** > **Perform action** to restart the server.

### Installing network configuration
{: #install-network-configuratio}

Use the following steps to install the network configuration.

1. Install ESXi.

   After the installation is complete, make sure to **Plug out** the ISO so that you can restart the server.
   {: note}

2. Restart the server.
3. Configure the IP address of the server after it restarts.
4. Gather the details from the **Configuration** tab of the device.

You can now manage the ESXi host.

For more information about setting up QuantaStor, see the [Architecture guide for QuantaStor](/docs/vmware?topic=vmware-quantastor-architecture-guide).
