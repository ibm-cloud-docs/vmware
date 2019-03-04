---
copyright:
  years: 1994, 2018
lastupdated: "2018-11-15"

subcollection: vmware
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Installing VMware vSphere ESXi via Remote Console and Virtual Media

Deploying ESX from installation media is similar across all versions and can be used in BYOL (bring your own license) scenarios.

## Requirements
* A virtual machine instance that has access to the Private Network [such as a cloud compute instance (VSI) that is installed with Windows or Linux, with a Java enabled browser, accessible via vpn.softlayer.com or public IP]. The VSI must be on the same private network that the server’s Intelligent Platform Management Interface (IPMI) addresses are located.
* A copy of VMware ESXi VIM Installer ISO.

## Connecting to IPMI
1. Upload the VMware ISO to the VSI that is specified in Requirements (The VSIs ought to have public web access.)
2. Gather the IPMI address and login information from the customer portal.
3. Select **Devices** > **Device List** > **[Server]** > and **Remote Management** tab.
4. Connect by using remote desktop (RDP) or Remote X into to the VSI that is storing the ESXi image.
5. Open a web browser in the RDP session and enter the IPMI address that you collected in Step 2.
6. Log in to the IPMI console with the credentials that are also found in Step 2 (typically root).
* Make a note of your IPMI user access level. It might be Administrator. You might experience a problem when you mount your remote storage if it is set to **Operator**. File a support ticket to elevate your IPMI credentials if you cannot mount media.
7. Confirm that you are on the home login page and click **Remote Control** > **Console Redirection** > **Launch Console**.

## Attaching ISO
1. On the kernel-based virtual machine (KVM) viewer, select **Virtual Media** > **Virtual Storage**. Your operating system and Java version might require you to allow access to start the Java-based viewer.
2. Click the **CDROM and ISO** tab in the Virtual Storage window. For the Logical Drive Type, select **ISO File** and click **Open Image**.
3. Go to the ESXi ISO and click **OK**. Then, click **Plug in**.
4. After the ISO is plugged into the session, click **OK**.
* Go back to the IPMI webpage and click **Remote** > **Control** > **Reset Server** > **Perform Action** to restart the server.

### Installing and completing networking configuration
1. Install ESXi.
* After the installation is complete, make sure to **Plug Out** the ISO so that you can restart the server.
2. Restart the server.
3. Configure the IP address of the server after it restarts.
4. Gather the details from the Configuration tab of the device.

You can now manage the ESXi host.

For more information about setting up endurance or performance block storage, see [Provisioning and Managing Block Storage](/docs/infrastructure/BlockStorage?topic=BlockStorage-orderingthroughConsole).

For more information about setting up QuantaStor, see [Architecture Guide for QuantaStor](/docs/infrastructure/vmware?topic=VMware-architecture-guide-for-quantastor).
