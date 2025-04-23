---

copyright:
  years: 1994, 2025
lastupdated: "2025-04-23"

keywords: iSCSI, VMWare ESXi, mount iscsi, mount esxi,

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Mounting ISCSI VMware ESXi
{: #mount-iscsi-esxi}

Mounting iSCSI into VMware&reg; ESXi can be accomplished with a few steps and only the details of the server and storage node.
{: shortdesc}

In most VMware&reg; environments, NFS {{site.data.keyword.filestorage_short}} is the better choice. {{site.data.keyword.filestorage_short}} is designed to support high I/O applications that require predictable levels of performance. In a VMware&reg; deployment, a single {{site.data.keyword.filestorage_short}} volume can be mounted to up to 64 ESXi hosts as shared storage that is much better than {{site.data.keyword.blockstorageshort}}, which supports 8 hosts by default. You can also mount multiple {{site.data.keyword.filestorage_short}} volumes to create a storage cluster to use vSphere Storage Distributed Resource Scheduler (DRS). For more information, see [Attached Storage for vCenter Server architecture](/docs/vmwaresolutions?topic=vmwaresolutions-storage-benefits) and [Provisioning File Storage for use as VMware datastore](/docs/FileStorage?topic=FileStorage-architectureguide&interface=ui).
{: tip}

Before you begin, you can familiarize yourself with [VMware vSphere 8.0 - Using ESXi with iSCSI SAN](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/8-0/vsphere-storage-8-0/using-esxi-with-iscsi-san.html){: external}.

1. Log in to the vSphere by using the primary private IP and user **root** and root's password.
1. From the **Welcome page**, click the **Configuration** tab > **Storage adapters** > **Add**.
1. Click **OK** to add the Software iSCSI adapter and confirm by clicking **OK** again.
1. After the refresh, the new iSCSI adapter is listed. Click **Properties**.
1. From the **Properties Window**, click **Configure** and set the **Name** to the IQN for the server (found on the storage device page under authorized hosts). 
   - Alternatively, you can set the IQN by running the following command from the ESXi shell: `esxcli iscsi adapter set -A $(esxcli iscsi adapter list | grep vmh | awk '{print$1}') -n $IQNFROMAUTHORIZEDHOSTSECTION`.
1. Click the **Dynamic discovery** tab then click **Add...**.
1. The iSCSI server is the target IP of the storage device. Click **CHAP**.
1. Select **Use CHAP** and clear **Inherit from parent**. Enter the **username** (found on the storage device page under authorized hosts) and password.
1. Select **Do not use CHAP** under the **Mutual CHAP** section then click **OK**. Now you can see the device in the **Dynamic discovery** window and click **Close**.
1. Confirm the rescan of the storage devices. You now see the device turn gray and 'unmounted.'
1. Right-click the device name and select **Attach**.
1. Click the **data store** Menu on the left side column then click **add storage** and choose **Disc/LUN**.
1. Click the device with the `iqn`.
1. Choose the file system version that you want and click **Next** to continue through the wizard.

You can now use the iSCSI as needed by the host and the VMs you create. 

For a more stable connection, mount the network storage on the hypervisor first as described. Then create the VMs, and mount the attached storage volume from the virtual server's OS with a multipath connection. For more information, see [Understanding Multipathing and Failover in the ESXi Environment](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/8-0/vsphere-storage-8-0/understanding-multipathing-and-failover-in-the-esxi-environment.html#GUID-DD2FFAA7-796E-414C-84CE-1FCC14474D5B-en){: external}, and [Setting Up Network for iSCSI and iSER with ESXi](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/8-0/vsphere-storage-8-0/configuring-iscsi-and-iser-adapters-and-storage-with-esxi/setting-up-network-for-iscsi-and-iser-with-esxi.html#GUID-0D31125F-DC9D-475B-BC3D-A3E131251642-en){: external}.
{: tip}

## Verifying the MPIO configuration
{: #verifyMPIOconfigESXI}

Complete the following steps to view which multipathing policies the host uses for a specific storage device and the status of all available paths for the storage device. If MPIO is configured correctly, then each storage volume has a single group, with the number of paths equal to the number of iSCSI sessions.

1. In the vSphere Client, go to the ESXi host.
1. Click the Configure tab.
1. Under Storage, click **Storage Devices**.
1. Select the storage device whose paths you want to view.
1. Click the Properties tab.

   Under Multipathing Policies, you can also see the Path Selection Policy and, if applicable, the Storage Array Type Policy assigned to the device.
   {: note}

1. Click the Paths tab to review all paths that are available for the storage device and the status of each path.
   |Status        | Description |
   |--------------|-------------|
   | Active (I/O)	| Working path or multiple paths that currently transfer data. |
   | Standby      |	These paths are inactive. If the active path fails, they can become operational and start transferring I/O.|
   | Disabled     | These paths are deactivated by the administrator. |
   | Dead         |	Paths that are no longer available for processing I/O. A physical medium failure or array misconfiguration can cause this status. |
   {: caption="Possible status values for the device paths." caption-side="bottom"}
   
For more information, see [Viewing and Managing Storage Paths on ESXi Hosts](https://techdocs.broadcom.com/us/en/vmware-cis/vsphere/vsphere/8-0/vsphere-storage-8-0/understanding-multipathing-and-failover-in-the-esxi-environment/viewing-and-managing-storage-paths-on-esxi-hosts.html){: external}.

If MPIO isn't configured correctly, your storage device might disconnect and appear offline when a network outage occurs or when {{site.data.keyword.cloud}} teams perform maintenance. MPIO provides an extra level of connectivity during those events, and keeps an established session to the volume with active read/write operations.
