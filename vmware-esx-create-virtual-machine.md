---
copyright:
  years: 1994, 2018
lastupdated: "2018-11-15"

subcollection: vmware
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Creating a VMware ESX virtual machine

To create a new virtual machine, follow these steps.
{:shortdesc}

1. Right-click your host node IP address in the Inventory pane of the vSphere Client.
2. Select **Custom**.
3. Give the virtual machine an appropriate name and click **Next**.
4. Select the storage location for virtual machine files and click **Next**.
5. Go to **Virtual Machine Version** > **Virtual Machine Version 8**.
6. Select an **Operating System**.
7. Select the number of virtual processors (**CPU page**) and the amount of **Memory** that you want in the virtual machine. **Note:** You can change the number of processors and memory later if the resources are available. 
In the network section, you need to connect two NICs, with NIC 1 being the Private Network and NIC 2 is the Public Network. The adapter type is “Flexible”. Make sure that **Connect at Power On** is selected.
8. Keep the **SCSI Controller** screen to the default “LSI Logic Parallel”. Select **Create a new virtual disk**. The **Advanced Options** screen and the **Ready to complete** screen must also be left default. The creation of a new virtual machine is now complete. 

To load your installation media, click the server name in the inventory list. Click **Edit Virtual machine Settings** under **Basic Tasks**.

9. With **CD/DVD Drive 1** selected, select the **Connect at power** check box under **Device Status**. To specify an ISO file that is located in your data store, click **Browse**.
10. The ISO files that are uploaded to the default Storage1 data store are selectable. You also see folders that contain the configuration and log files for all the server virtual machines.

After you select your ISO image, you are ready to begin installing your respective OS.

For more information about setting up a virtual machine network, see [Setting up a virtual machine network](/docs/infrastructure/virtualization?topic=Virtualization-setting-up-a-virtual-machine-network){:new_window}.
