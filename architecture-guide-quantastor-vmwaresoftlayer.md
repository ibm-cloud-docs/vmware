---

copyright:
  years: 1994, 2020
lastupdated: "2020-03-18"

keywords: iSCSI software adapter, Select Targets, QuantaStor, VMware shared storage, iSCSI, storage volume, software defined storage

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}


# QuantaStor for VMware Architecture Guide
{: #quantastor-architecture-guide}

You can order and configure the OSNexus QuantaStor shared storage solution for a VMware ESXi 5 environment. Use the following information along with the [Advanced Single-Site VMware Reference Architecture](/docs/virtualization?topic=virtualization-advanced-single-site-vmware-reference-architecture) cookbook to set up one of these storage options in your VMware environment.

## Before you begin
{: #before-you-begin-vmware-arch}
* Navigate to your console's device menu. For more information, see [Navigating to devices](/docs/bare-metal?topic=virtual-servers-navigating-devices).
* Ensure that you have any necessary account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions.

For more information about permissions, see [Classic infrastructure permissions](/docs/account?topic=account-infrapermission#infrapermission) and [Managing device access](/docs/virtual-servers?topic=virtual-servers-managing-device-access).

## Step 1: Ordering QuantaStor Shared Storage
{: #order-quantastor-storage}

Before you place an order for storage, you need to determine the specifications that meet your capacity, performance, and redundancy requirements. This can include processor and chassis choice, QuantaStor license capacity, server RAM, type and number of data disk drives, type and number of cache disks, and networking configuration and other specifications. For more information about choosing the correct QuantaStor configuration in your environment, see [QuantaStor Solution Design Guide for Virtualization ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://wiki.osnexus.com/index.php?title=-_1._IBM_Cloud_QuantaStor_SAN/NAS_Storage_Servers){: new_window}.

Make sure that you understand the capacity and I/O requirements of your VMs before you place your order. While the QuantaStor server is expandable, it is important that you size your hardware initially to avoid delays in configuration and deployment.

### Ordering QuantaStor
{: #order-quantastor}

Complete the following steps to order a 24 TB usable QuantaStor hybrid system that is tuned for mid-range performance for VMware workloads:

1. Log in to [{{site.data.keyword.slportal_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/){: new_window} and click **Account > Place an Order**.
2. Select {{site.data.keyword.baremetal_short}}, Monthly on the pop-up screen.
3. Enter the following configuration options:
   * **Data Center:** Location of the VLANs and ESXi hosts that were previously created
   * **Server:** 36-bay chassis with Dual Processor Xeon
   * **RAM:** 128 GB
   * **Operating System:** OSNEXUS QuantaStor 5.x (48 TB)
   * **Hard Disk Drives:**
      * OS Disks: 2 x 960 GB SSD in RAID 1
      * Data Disks: 24 x 2 TB SATA in Individual
      * Log Disks: 2 x 960 GB SSD in Individual
      * Cache Disks: 2 x 960 GB SSD in Individual
   * **Public Bandwidth:** Private Network Only
   * **Uplink Port Speeds:** 10 Gbps Redundant Private Network Uplinks
4. Click **Continue Your Order**.

**Note:** The storage server is configured with two network interfaces that are unbonded so that two different subnets can be used to load balance traffic to the storage array.

### Finishing Configuration
{: #finish-quantastor-configuration}

You now have a QuantaStor appliance in your shopping cart. Assign the private VLAN, hostname, and domain to the device so it can be provisioned correctly.

1. Assign the following VLANs and create hostnames for the devices: QuantaStor host – Backend VLAN: (1102 in the environment)
2. Select your payment method, agree to the Terms and Conditions, and click Finalize Your Order.

**Note** Do not proceed to Step 3 until the server is provisioned and is accessible through VPN or virtual server.

## Step 2: Enabling iSCSI Software Adapter for VMware Hosts
{: #enabling-iSCSI}

The iSCSI Software Adapter must be enabled on each management and capacity host and its iSCSI Qualified Name (IQN) collected before iSCSI volumes are mounted. Use the following steps to enable the iSCSI software adapter:

1. Go to an ESXi management or capacity host and select Manage, Storage, Storage Adapters.
2. Click the green plus sign (+) and add the iSCSI Software Adapter.
3. Click the vmhba that corresponds to the iSCSI Software Adapter and record the iSCSI Name (Figure 1) in the Adapter Details section after it is enabled.
4. Do steps 1 - 3 for each iSCSI Software Adapter on each ESXi host.

## Step 3: Configuring QuantaStor
{: #configuring-iscsi}

After the QuantaStor server is provisioned, you can set up networking, create pass-through (RAID0) units, build the storage pool, create iSCSI volumes, and finally assign those volumes to hosts.

For example, volume vmk3 has vmnic0 that connects to Portable Private Subnet A on the storage VLAN. Volume vmk4 has vmnic2 that connects to Portable Private Subnet B on the storage VLAN. The QuantaStor server also has two private network adapters, eth4 and eth6, that connect to the storage VLAN.

### Configuring Networking
{: #configuring-networking}

1. Open a web browser and go to the QuantaStor IP address listed on the **Devices** page on [{{site.data.keyword.slportal_short}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/){: new_window}.
2. Enter the **Admin user name** and **Password** (found in the Passwords section on the **Device Details** page). Before you proceed, note the private network devices that are used by the QuantaStor server, such as eth4.
3. Go to **Storage System > Network Ports**.
4. Select the private adapter that is active (example: eth4) from the list of network adapters. Right-click and select **Modify Network Port** from the menu.
5. Clear the **iSCSI Enabled** check box to disable iSCSI connections to this adapter and click **OK**.
6. Select the private adapter that is not active, but is assigned to the private network (example eth6).
7. Right-click on the eth6 adapter and select **Modify Network Port** from the menu.
8. Select a **Config Type** of **Static** on the **Modify Network Port** screen.
9. Enter a primary private IP address, subnet, and gateway for the adapter. Use an address from the Storage row if you are using the VLAN worksheet from the [Advanced Single-Site VMware Reference Architecture](/docs/virtualization?topic=Virtualization-advanced-single-site-vmware-reference-architecture) cookbook.
10. Clear the **iSCSI Enabled** check box to disable iSCSI connections to this adapter.
11. Right-click the private adapter and select **Enable Network Port** to bring the adapter online after you configure it with an IP address.
12. Click **OK** to enable the port upon verifying the IP address.

### Opening a Support Ticket
{: #open-support-ticket}

You need to open a support ticket after you configure a second adapter with a primary private IP address. Opening the ticket helps make sure that the IP address that you used is not taken if another system is provisioned on the VLAN.

1. Click **Support** > **Add Ticket** and enter the following information:
   * Subject: Private network question
   * Title: Reserve and assign private IP address
   * Associate Devices: 'Select the QuantaStor server'
   * Details: Reserve and assign on VLAN. This IP address is used for the second adapter on the QuantaStor server.

### Configuring QuantaStor
{: #configuring-quantastor}

Now that the array can accept connections from both adapters, the adapters’ virtual interfaces that are on the Storage Path A and Storage Path B subnets must be assigned.

1. Right-click the initial private adapter interface (eth4) and select **Create Virtual Interface** on the menu.
2. Enter a portable private IP address and subnet for the adapter on the resulting pop-up screen, and make sure that **iSCSI Enabled** is checked.
3. If you are using the VLAN worksheet, use an address from the Storage Path A row.
4. Record the IP address that is used in the Notes section on the Portable IP address page.
5. Select the initial private adapter interface (eth4) to bind the virtual interface and click **OK**.
6. Right-click the other private adapter interface (eth6) and select **Create Virtual Interface** on the menu.
7. Enter a portable private IP address and subnet for the adapter and make sure that **iSCSI enabled** is checked on the resulting pop-up window.
8. If you are using the VLAN worksheet, use an address from the Storage Path B row.
9. Record this IP address as used in the Notes section on the Portable IP address page.
10. Select the other private adapter interface (eth6) to bind the virtual interface and click **OK**.

After the QuantaStor server is configured with IP addresses and virtual interfaces, configure the routing to make sure that the outgoing traffic uses the correct interface.(There are two NICs on different subnets).

1. SSH into the QuantaStor server with your root credentials and append the following lines to /etc/network/interfaces. Assuming eth4 and eth6 are the NICs on the private network:
   * post-up ip route add 10.0.0.0/8 on dev eth4
   * post-up ip route add 10.0.0.0/8 on dev eth6 table eth6
   * post-up ip rule add from table eth6

### Configure pass-through (RAID0) Units
{: #creating-passthru-units}

** Depending on provisioning, the physical disks might not be exposed to QuantaStor. You can check by clicking the Physical Disks section and looking at the list of available hard disk drives. If you do not see the correct number of drives, follow these steps:

1. Click Controllers & Enclosures and click "Create pass-through Units" in the Hardware Controller menu.
2. Verify host and controller and click OK.
3. After the task completes click Physical Disks and verify

### Creating a Storage Pool
{: #creating-storage-pool}

Next, you must create a storage pool that is used to allocate volumes before you can create volumes or shares.

1. Right-click **Storage Pools** and select **Create Storage Pool**.
2. Enter the following information on the **Create Storage Pool** screen:
   * Name: Enter the appropriate name for the storage pool. Example: StoragePool-01
   * Pool Type: Default (zfs)
   * I/O Profile: Virtualization
   * Disks to use for the Storage Pool: check all the data disks (do not check SSD's).
3. Click **OK**.

### Creating iSCSI Storage Volumes
{: #creating-iSCSI-storage}

You need to create two storage volumes. One volume is used for management VMs on the management cluster and the other for VMs on the capacity cluster. Complete the following steps to create the iSCSI storage volumes:

1. Right-click **Storage Volumes** and select **Create Storage Volume** on the menu.
2. Enter the information for the storage volumes. **Note:** While your configuration might differ depending on workload and storage capacity, the example shows the values in Table 1 and Table 2 for each storage volume.

|Field|Value|
|---|---|
|Name|Mgmt-LUN0|
|Storage Pool|[Storage Pool Name configured in the previous step]|
|Size|1TB|
|% Reserved|0-100|
|Compression|Enabled|
{: caption="Table 1. iSCSI Management Volume" caption-side="top"}

|Field|Value|
|---|---|
|Name|Capacity-LUN0|
|Storage Pool|[Storage Pool Name configured in the previous step]|
|Size|40TB|
|% Reserved|0-100|
|Compression|Enabled|
{: caption="Table 2. iSCSI Capacity Volume" caption-side="top"}

### Assigning Host Access to Volumes
{: #assigning-host-access}

You need to configure QuantaStor to allow access from the ESXi hosts through each host’s IQN after the volumes are set up.

1. Navigate to the QuantaStor administration page and right-click the **Hosts** menu and select **Add Host**.
2. Enter the following information on the **Add Host** screen:
   * Host name: Enter an appropriate host name. The host name does not have the fully qualified domain name (FQDN), but is must describe the host. Example: MyESXiHostName
   * Operating System Type: VMware
   * Initiator: iSCSI Qualified Name (IQN)
   * iSCSI Qualified Name: The IQN for the respective host.
3. Click **OK**.

Follow these steps for each host in ESXi environment. After you add each host in the management and capacity clusters follow these steps:

1. Right-click the **Host Groups** menu and select **Create Host Group…**.
2. Enter 'ManagementCluster' in the **Name** field and select all the hosts that are in the management cluster.
3. Click **OK**. A host group is created that we can assign to a particular volume.

Repeat this process for the capacity cluster.

1. Click the **Storage Volumes** menu.
2. Right-click the **Mgmt-Lun0** volume and select **Assign or Unassign Host Access**.
3. Confirm that **Mgmt-Lun0** is an option in the menu and select the host group that you created in the previous step. This option allows each ESXi host in the management cluster to access the Mgmt-Lun0 volume. Do the same for **Capacity-LUN0**

## Step 4: Mounting Volumes on Management / Capacity Clusters
{: #mount-volumes}

Log in to the vSphere web Client and go to **Hosts** under the **vCenter Inventory Lists**.

Use the following steps to mount the volume on the ESXi hosts:

1. Select a host and click **Manage, Storage,** > **Storage Adapters**.
2. Select **Targets** > **Dynamic Discovery** > **Add…**.
3. Enter the IP address that is assigned to the QuantaStor storage device on Storage Path A on the **Add Send Target Server** screen.
4. Leave **3260** as the Port and click **OK**.
5. Click **Dynamic Discovery** > **Add…**. Repeat steps 4 and 5 for Storage Path B.

The ESXI host is ready to rescan the iSCSI Software Adapter to discover the Mgmt-Lun0 volume.

1. Select the **Rescan Storage Adapters** icon (Figure 9) on the **Storage Adapters** screen.
2. Leave the default option on the resulting pop-up screen and click **OK**.
3. Click **Actions, New Datastore** after the volume is discovered and format it as **VMFS-5**.
4. Confirm that the formatting is complete and click **Storage Devices, Device Details, Edit Multipathing…**.
5. Select **Round Robin** for the **Path Selection Policy** and click **OK**.

Now that the Mgmt-Lun0 volume is attached to a single host, you must go back to the other management hosts in the cluster and repeat the process to add the volume. You do not need to format the volume as it already formatted with VMFS-5 and is displayed as such after discovery.

## Step 5: Disabling Delayed ACK in vSphere ESXi hosts
{: #disabling-delayed-ACK}

The delayed ACK needs to be disabled after the storage LUNs are attached to the management and capacity hosts.

1. Go to the vSphere environment and select **Storage Adapters** > **iSCSI Software Adapter** > **Advanced Options**.
2. Click **Edit** and scroll all the way to the end of the Advanced Options screen.
3. Clear the **DelayedAck** check box and click **OK**.

For more information about delayed ACK regarding VMware, see [VMware’s Knowledge Base](https://kb.vmware.com/s/article/1002598).

You can now return to [Advanced Single-Site VMware Reference Architecture](/docs/virtualization?topic=Virtualization-advanced-single-site-vmware-reference-architecture) cookbook and complete the environment setup.
