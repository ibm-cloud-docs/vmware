---

copyright:
  years: 1994, 2024
lastupdated: "2024-07-15"

keywords: custom, vmware esx virtual machine, virtual machine

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Creating a VMWare ESX virtual machine
{: #create-esx-vm}

You create a VMWare ESX virtual machine.
{: shortdesc}

To create a new virtual machine, follow these steps.

1. Right-Click your host node IP address in the Inventory pane of the vSphere Client.
1. Select **Custom** in the configuration window.
1. Give the virtual machine an appropriate name and click **Next**.
1. Select the Storage location for virtual machine files and click **Next**.
1. From the **Virtual Machine Version**, select **Virtual Machine Version 8**.
1. Select the **Operating System**.
1. Select the number of virtual processors (**CPU page**) and the amount of **Memory** that you would like to create the virtual machine. **Note:** You can change the number of processors and memory about later if the resources are available.
In the network section, you need to connect two NICs, with NIC 1 being the Private Network and NIC 2 is the Public Network. The adapter type is “Flexible”. Make sure that **Connect at Power On** is selected.
1. Keep the **SCSI controller** screen to the default “LSI Logic Parallel”. On the **Select a Disk** screen, select **Create a new virtual disk**. Keep the default selection on the **Advanced Options** and the **Ready to complete** screens.

The creation of a new virtual machine is now complete.

## Loading installation media
{: #load-esx-installation-medioa}

To load your installation media, click the server name in the inventory list. Then, click **Edit Virtual machine Settings** under **Basic Tasks**.

1. With **CD/DVD Drive 1** selected, check the **Connect at power** checkbox under Device Status. To specify an ISO file that is located in your data store, click **Browse**.
1. The ISO files that are uploaded to the default Storage1 data store are selectable here. You also see folders that contain the configuration and log files for all the server virtual machines.

After you select your ISO image, you are ready to begin the installation process of your respective OS.

For more information about setting up a virtual machine network, see [Setting up a virtual machine network](/docs/virtualization?topic=virtualization-setting-up-a-virtual-machine-network){: new_window}.
