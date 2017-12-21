---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Mounting iSCSI VMWare ESXi

Mounting iSCSI into VMWare ESXi can be accomplished with a few steps and only the details of the server and storage node.
{:shortdesc}

1. Log into the vSphere using the Primary Private IP and user **root** and root's password.
* From the Welcome Page, click the **Configuration** tab.
* Click **Storage Adapters** then **Add…**.
* Click **OK** to add the Software iSCSI Adapter.
* Confirm by clicking **OK**.
* After the refresh, you will see the new iSCSI Adapted listed.
* Click **Properties** in the bottom pane.
* From the Properties Window, click **Configure** near the bottom and set the **Name** to the IQN for the server(found on the storage device page under authorized hosts).
* Click on the **Dynamic Discovery Tab** then click the **Add...**.
* The iSCSI server will be the target IP of the storage device then click on the **CHAP..** button.
* Select **Use CHAP** and uncheck **Inherit from Parent**. Input the **Username** (found on the storage device page under authorized hosts) and its password.
* Select **Do not use CHAP** under the Mutual CHAP section then click **OK**.
* You will now see the device in the Dynamic Discovery Window, click **Close**.
* Confirm the Rescan of the storage devices.
* You will then see the device in the bottom pane grey and 'unmounted.'
* Right click on the device name and select **attach**.
* Click on the **Datastore** Menu on the left side column then click **add storage** and choose **Disc/LUN**.
* Click on the device with the 'iqn.'
* Choose the File system Version you would like and click **next** then continue through the wizard.
* Once complete, you can then use the iSCSI as needed by the host and the VMs you create.



Attaching a Data Transfer Service iSCSI device is the same, except you need to get the IQN from the server.  You complete the following steps from the ESXi console:

First you need to get the device:

`esxcfg-scsidevs -a | grep iSCSI`

Then you'll need to get the IQN (in this case, vmhba33 is the iSCSI device):

`vmkiscsi-tool -I -l vmhba33`
