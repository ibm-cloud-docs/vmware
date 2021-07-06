---

copyright:
  years: 1994, 2021
lastupdated: "2020-05-19"

keywords: iSCSI, VMWare ESXi, mount iscsi, mount esxi, 

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Mounting iSCSI VMWare ESXi
{: #mount-iscsi-esxi}

Mounting iSCSI into VMWare&reg; ESXi can be accomplished with a few steps and only the details of the server and storage node.
{:shortdesc}

1. Log in to the vSphere by using the primary private IP and user **root** and root's password.
* From the **Welcome page**, click the **Configuration** tab.
* Click **Storage adapters** > **Add**.
* Click **OK** to add the Software iSCSI adapter.
* Confirm by clicking **OK**.
* After the refresh, the new iSCSI adapter is listed.
* Click **Properties**.
* From the **Properties Window**, click **Configure** and set the **Name** to the IQN for the server (found on the storage device page under authorized hosts).
* Click the **Dynamic discovery** tab then click **Add...**.
* The iSCSI server is the target IP of the storage device, then click **CHAP**.
* Select **Use CHAP** and clear **Inherit from parent**. Input the **username** (found on the storage device page under authorized hosts) and the password.
* Select **Do not use CHAP** under the **Mutual CHAP** section then click **OK**.
* You now see the device in the **Dynamic discovery** window and click **Close**.
* Confirm the rescan of the storage devices.
* You now see the device turn gray and 'unmounted.'
* Right-click the device name and select **attach**.
* Click the **Data store** Menu on the left side column then click **add storage** and choose **Disc/LUN**.
* Click the device with the 'iqn.'
* Choose the file system Version that you want and click **Next** to continue through the wizard.
* You can now use the iSCSI as needed by the host and the VMs you create.



<!-- Attaching a Data Transfer Service iSCSI device is the same process, with the exception that you need to get the IQN from the server. Complete the following steps from the ESXi console: -->

<!--First, you need to get the device:-->

<!-- `esxcfg-scsidevs -a | grep iSCSI` -->

<!-- Then, you need to get the IQN (in this case, vmhba33 is the iSCSI device): -->

<!-- `vmkiscsi-tool -I -l vmhba33` -->
