---

copyright:
  years: 1994, 2022
lastupdated: "2022-06-30"

keywords: iSCSI, VMWare ESXi, mount iscsi, mount esxi, 

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:shortdesc: .shortdesc}
{:term: .term}

# Mounting ISCSI VMware ESXi
{: #mount-iscsi-esxi}

Mounting iSCSI into VMware&reg; ESXi can be accomplished with a few steps and only the details of the server and storage node.
{: shortdesc}

In most VMware&reg; environments, NFS {{site.data.keyword.filestorage_short}} is the better choice. {{site.data.keyword.filestorage_short}} is designed to support high I/O applications that require predictable levels of performance. In a VMware&reg; deployment, a single {{site.data.keyword.filestorage_short}} volume can be mounted to up to 64 ESXi hosts as shared storage, that is much better than {{site.data.keyword.blockstorageshort}} which supports 8 hosts by default. You can also mount multiple {{site.data.keyword.filestorage_short}} volumes to create a storage cluster to use vSphere Storage Distributed Resource Scheduler (DRS). For more information, see [Provisioning File Storage for use as VMware datastore](/docs/FileStorage?topic=FileStorage-architectureguide&interface=ui){: external}.
{: tip}

1. Log in to the vSphere by using the primary private IP and user **root** and root's password.
2. From the **Welcome page**, click the **Configuration** tab.
3. Click **Storage adapters** > **Add**.
4. Click **OK** to add the Software iSCSI adapter.
5. Confirm by clicking **OK**.
6. After the refresh, the new iSCSI adapter is listed.
7. Click **Properties**.
8. From the **Properties Window**, click **Configure** and set the **Name** to the IQN for the server (found on the storage device page under authorized hosts).
9. Click the **Dynamic discovery** tab then click **Add...**.
10. The iSCSI server is the target IP of the storage device, then click **CHAP**.
11. Select **Use CHAP** and clear **Inherit from parent**. Input the **username** (found on the storage device page under authorized hosts) and the password.
12. Select **Do not use CHAP** under the **Mutual CHAP** section then click **OK**.
13. You now see the device in the **Dynamic discovery** window and click **Close**.
14. Confirm the rescan of the storage devices.
15. You now see the device turn gray and 'unmounted.'
16. Right-click the device name and select **attach**.
17. Click the **Data store** Menu on the left side column then click **add storage** and choose **Disc/LUN**.
18. Click the device with the 'iqn.'
19. Choose the file system version that you want and click **Next** to continue through the wizard.
20. You can now use the iSCSI as needed by the host and the VMs you create.











