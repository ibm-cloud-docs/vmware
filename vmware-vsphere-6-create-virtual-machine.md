---

copyright:
  years: 1994, 2020
lastupdated: "2017-08-10"

keywords: VMware vSphere 6 virtual machine

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Creating a Virtual Machine with VMware vSphere 6
{: #create-vsphere-6-virtual-machine}

1. Right-click your host node IP address in the **Inventory** pane of the vSphere Client.
2. In the configuration window, select **Custom**.
3. Give the virtual machine an appropriate name and click **Next**.
4. Select the Storage location for virtual machine files and click **Next**.
* The **Virtual Machine Version** menu gives you the option to use different cluster types. Since this cluster is new and you do not need support for older versions, select **Virtual Machine Version 8**. **Note:** If you use the Web Client to create a cluster, use version 11.
5. Select the **Operating System** type.
6. Set the number of virtual processors (on the CPUs page) and click **Next**
  1. **Note:** You can change the number of CPUs later if the resources are available.
7. Set the amount of memory that you want for the virtual machine. Click **Next**
  1. **Note:** You can change the amount of memory later if the resources are available.
8. In the network section, you need to connect the two NICs. NIC 1 is for the Private Network and NIC 2 is for the Public Network. The adapter type id “Flexible”. Make sure that the “Connect at Power On” check box is selected.
9. Leave the SCSI Controller screen to the default “LSI Logic Parallel”. On the Select a Disk screen, select **Create a new virtual disk**. Keep the default settings on the **Advanced Options** screen and the **Ready to Complete** screen. Your new virtual machine is now created. To begin loading your installation media, click the server name from the inventory list and click **Edit Virtual machine Settings** under **Basic Tasks**.
<!--* false-->
10. With CD/DVD Drive 1 selected, select **Connect at power** under Device Status. To specify an ISO file that is located in your Datastore, click **Browse**.
* The ISO files that are uploaded to the default Storage1 Datastore are selectable here. You also see folders that contain the configuration/log files (set up during Step 3 Datastore section of the Create a new Virtual Machine process) for all the server virtual machines.
11. After you select your ISO image, you are ready to begin the installation process of your respective OS.
* After your Guest VM is successfully up and running, if supported, install [VMWare Tools ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kb.vmware.com/s/article/1014294){: new_window}.
* For more information about networking instructions, see [Setting up a Virtual Machine Network](/docs/virtualization?topic=virtualization-setting-up-a-virtual-machine-network).
