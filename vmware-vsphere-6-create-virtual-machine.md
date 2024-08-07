---

copyright:
  years: 1994, 2024
lastupdated: "2024-07-15"

keywords: VMware vSphere virtual machine

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Creating a virtual machine with VMware vSphere
{: #create-vsphere-6-virtual-machine}

1. Right-click your host node IP address in the **Inventory** pane of the vSphere Client.
1. In the configuration window, select **Custom**.
1. Give the virtual machine an appropriate name and click **Next**.
1. Select the storage location for virtual machine files and click **Next**. The **Virtual machine version** menu gives you the option to use different cluster types.
1. Select an **Operating system**.
1. Set the number of virtual processors (on the CPUs page) and click **Next**. You can change the number of CPUs later if the resources are available.
1. Set the amount of memory that you want for the virtual machine. Click **Next**. You can change the amount of memory later if the resources are available.
1. In the network section, you need to connect the two NICs. NIC 1 is for the Private Network and NIC 2 is for the Public Network. The adapter type ID “Flexible”. Make sure that the “Connect at Power On” checkbox is selected.
1. Leave the SCSI Controller screen to the default “LSI Logic Parallel”. On the _Select a Disk_ screen, select **Create a new virtual disk**. Keep the default settings on the **Advanced options** screen and the **Ready to complete** screen. Your virtual machine is created. To load your installation media, click the server name from the inventory list and click **Edit virtual machine settings** under **Basic tasks**.
1. With CD/DVD Drive 1 selected, select **Connect at power** under Device Status. To specify an ISO file that is located in your data store, click **Browse**.
    * The ISO files that are uploaded to the default Storage1 data store are selectable here. You also see folders that contain the configuration and log files (set up during Step 3 data store section of the Create a new virtual machine process) for all the server virtual machines.
1. After you select your ISO image, you are ready to install the respective OS.

* After your Guest VM is running, if supported, install VMWare&reg; Tools.
* For more information about networking instructions, see [Setting up a virtual machine network](/docs/virtualization?topic=virtualization-setting-up-a-virtual-machine-network).
