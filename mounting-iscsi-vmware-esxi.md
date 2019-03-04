---
copyright:
  years: 1994, 2017
lastupdated: "2018-11-16"

subcollection: vmware
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Mounting iSCSI VMWare ESXi

Mounting iSCSI into VMWare ESXi can be accomplished with a few steps and only the details of the server and storage node. **Note:** If you want to connect multiple ESXi servers to the same ISCSI LUNs, the Host Authorization limit for ISCSI is eight hosts.
{:shortdesc}

1. Log in to the vSphere by using the Primary Private IP and user **root** and root's password.
* From the Welcome Page, click the **Configuration** tab.
* Click **Storage adapters** > **Add…**.
* Click **OK** to add the Software iSCSI adapter.
* Confirm by clicking **OK**.
* After the refresh, the new iSCSI adapter is listed.
* Click **Properties**.
* From the Properties Window, click **Configure** and set the **Name** to the IQN for the server(found on the storage device page under authorized hosts).
* Click the **Dynamic Discovery Tab** then click the **Add...**.
* The iSCSI server is the target IP of the storage device, then click **CHAP..**.
* Select **Use CHAP** and clear **Inherit from Parent**. Input the **User name** (found on the storage device page under authorized hosts) and its password.
* Select **Do not use CHAP** under the Mutual CHAP section then click **OK**.
* You now see the device in the Dynamic Discovery Window, click **Close**.
* Confirm the Rescan of the storage devices.
* The device turns gray and is 'unmounted.'
* Right-click the device name and select **attach**.
* Click the **Data store** Menu on the left side column then click **add storage** and choose **Disc/LUN**.
* Click the device with the 'iqn.'
* Choose the file system version that you want and click **Next**.
* You can now use the iSCSI.



Attaching a Data Transfer Service iSCSI device is the same, except you need to get the IQN from the server.  You complete the following steps from the ESXi console:

You need to get the device:

`esxcfg-scsidevs -a | grep iSCSI`

You also need to get the IQN (in this case, vmhba33 is the iSCSI device):

`vmkiscsi-tool -I -l vmhba33`
