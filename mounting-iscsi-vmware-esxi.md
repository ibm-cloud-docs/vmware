---

copyright:
  years: 1994, 2019
lastupdated: "2019-08-21"

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

Mounting iSCSI into VMWare ESXi can be accomplished with a few steps and only the details of the server and storage node.
{:shortdesc}

1. Log in to the vSphere by using the Primary Private IP and user **root** and root's password.
* On the Welcome Page, click the **Configuration** tab.
* Click **Storage Adapters** > **Add…**.
* Click **OK** to add the Software iSCSI Adapter.
* Confirm by clicking **OK**.
* After the refresh, the new iSCSI Adapted listed.
* Click **Properties**.
* From the Properties Window, click **Configure** and set the **Name** to the IQN for the server(found on the storage device page under authorized hosts).
* Click the **Dynamic Discovery Tab** then click the **Add...**.
* The iSCSI server is the target IP of the storage device then click **CHAP..**.
* Select **Use CHAP** and clear **Inherit from Parent**. Input the **Username** (found on the storage device page under authorized hosts) and its password.
* Select **Do not use CHAP** under the Mutual CHAP section then click **OK**.
* You now see the device in the Dynamic Discovery Window, click **Close**.
* Confirm the Rescan of the storage devices.
* You now see the device turn gray and 'unmounted.'
* Right-click the device name and select **attach**.
* Click the **Datastore** Menu on the left side column then click **add storage** and choose **Disc/LUN**.
* Click the device with the 'iqn.'
* Choose the File system Version that you want click **Next** to continue through the wizard.
* You can now use the iSCSI as needed by the host and the VMs you create.

