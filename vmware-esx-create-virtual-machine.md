---

copyright:
  years: 1994, 2020
lastupdated: "2019-08-21"

keywords: custom, vmware esx virtual machine, virtual machine

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}


# Creating a VMware ESX Virtual Machine
{: #create-esx-vm}

To create a new virtual machine, follow these steps.
{: shortdesc}

1. Right-Click your host node IP address in the Inventory pane of the vSphere Client.
2. Select **Custom** in the configuration window.
3. Give the virtual machine an appropriate name and click **Next**.
4. Select the Storage location for virtual machine files and click **Next**.
5. From the **Virtual Machine Version**, select **Virtual Machine Version 8**. <!-- since we are using vSphere instead of the Web Client to create it (in which case we would use version 11 instead).-->
6. Select the **Operating System**.
7. Select the number of virtual processors (**CPU page**) and the amount of **Memory** that you would like to create the virtual machine. **Note:** You can change the number of processors and memory about later if the resources are available. 
In the network section, you need to connect two NICs, with NIC 1 being the Private Network and NIC 2 is the Public Network. The Adapter type is “Flexible”. Make sure that **Connect at Power On** is selected.
8. Keep the **SCSI Controller** screen to the default “LSI Logic Parallel”. On the **Select a Disk** screen, select **Create a new virtual disk**. The **Advanced Options** screen and leave the **Ready to Complete** as the default. The creation of a new virtual machine is now complete. 

To begin loading your installation media, click the server name in the inventory list. Then, click **Edit Virtual machine Settings** under **Basic Tasks**.

9. With **CD/DVD Drive 1** selected, check the **Connect at power** check box under Device Status. To specify an ISO file that is located in your Datastore, click **Browse**.
10. The ISO files that are uploaded to the default Storage1 Datastore are selectable here. You also see folders that contain the configuration/log files for all the server virtual machines.

After you select your ISO image, you are ready to begin the installation process of your respective OS.

For more information about setting up a virtual machine network, see [Setting up a Virtual Machine Network](/docs/virtualization?topic=virtualization-setting-up-a-virtual-machine-network){: new_window}.
