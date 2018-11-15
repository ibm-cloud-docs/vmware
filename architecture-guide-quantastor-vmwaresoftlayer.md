---
copyright:
  years: 1994, 2018
lastupdated: "2018-11-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Architecture Guide for QuantaStor

You can order and configure the OSNexus QuantaStor shared storage solution for a VMware ESXi 5 environment. Use the following information along with the [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) cookbook to set up one of these storage options in your VMware environment.

## Step 1: Ordering QuantaStor shared storage

Before you place an order for storage, you need to determine the specifications that meet your capacity and I/O requirements. These specifications include, but are not limited to, server RAM, type and number of disk drives, SSDs for caching, RAID configuration, and networking configuration. For more information about choosing the correct QuantaStor configuration in your environment, see [QuantaStor Solution Design Guide for Virtualization ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide#Server_Virtualization){: new_window}.

For the example environment, a smaller configuration that can deliver enough capacity and I/O needed for the virtual machines (VMs) is used. Make sure that you understand the capacity and I/O requirements of your VMs before you place your order. While the QuantaStor server is expandable, it is important that you size your hardware initially to avoid delays in configuration and deployment.

### Ordering QuantaStor

Use the following steps to order a QuantaStor server.

1. Log in to [{{site.data.keyword.slportal_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window} and click **Account > Place an Order**.
2. Select {{site.data.keyword.baremetal_short}}, Monthly on the pop-up screen.
3. Select the appropriate server with the ability to store the numbers of disks that are needed from your environment from the Server List page. [For the example environment, a 12-core system (that is, dual hex core) with 12 drive bays is selected.]
4. Enter the following configuration options:
  * **Data Center:** Location of the VLANs and ESXi hosts that were previously created
  * **Server:** Dual Processor Hex Core Xeon
  * **RAM:** 64 GB
  * **Operating System:** OSNexus QuantaStor 3.x (4 TB)
  * **Hard Disks:**
    * Disks 1 & 2: 500 GB SATA in RAID 1
    * Partition Template: Linux Basic
    * Disks 3-10: 600 GB SAS 15 K in RAID-10
  * **Public Bandwidth:** Private Network Only
  * **Uplink Port Speeds:** 10 Gbps Redundant Private Network Uplinks
5. Click **Continue Your Order**.

**Note:** The storage server is configured with two network interfaces that are unbonded so that two different subnets can be used to load balance traffic to the storage array.

### Finishing configuration

You now have a QuantaStor appliance in your shopping cart. Now, you need to assign the private VLAN, hostname, and domain to the device so it can be provisioned correctly.

1. Assign the following VLANs and create hostnames for the devices: QuantaStor host – Backend VLAN: (1102 in the environment)
2. Select your payment method, agree to the Terms and Conditions, and click Finalize Your Order.

**Note** Do not proceed to Step 3 until the server is provisioned and is accessible through VPN or virtual server.

## Step 2: Enabling iSCSI software adapter for management and capacity hosts

The iSCSI Software Adapter must be enabled on each management and capacity host and its iSCSI Qualified Name (IQN) collected before iSCSI volumes are mounted. Use the following steps to enable the iSCSI software adapter:

1. Go to an ESXi management or capacity host and select Manage, Storage, Storage Adapters.
2. Click the green plus sign (+) and add the iSCSI Software Adapter.
3. Click the vmhba that corresponds to the iSCSI Software Adapter and record the iSCSI Name (Figure 1) in the Adapter Details section after it is enabled.
4. Do steps 1 - 3 for each iSCSI Software Adapter on each ESXi management and capacity host.

## Step 3: Configuring QuantaStor

After the server is provisioned, you can set up the shared storage device. Specifically, you set up networking and configure iSCSI volumes, and assign volumes to hosts. 

For example, volume vmk3 has vmnic0 that connects to Portable Private Subnet A on the storage VLAN. Volume vmk4 has vmnic2 that connects to Portable Private Subnet B on the storage VLAN. The QuantaStor server also has two private network adapters, eth4 and eth6, that connect to the storage VLAN.

### Configuring networking

1. Open a web browser and go to the QuantaStor IP address listed on the **Devices** page on [{{site.data.keyword.slportal_short}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window}.
2. Enter the **Admin User name** and **Password** (found in the Passwords section on the **Device Details** page). Before you proceed, note the private network devices that are used by the QuantaStor server, such as eth4.
3. Go to **Storage System > Network Ports**.
4. Select the private adapter that is active (example: eth4) from the list of network adapters. Right-click and select **Modify Network Port** from the pop-up menu.
5. Clear the **iSCSI Enabled** check box to disable iSCSI connections to this adapter and click **OK**.
6. Select the private adapter that is not active, but is assigned to the private network (example eth6).
7. Right-click on the eth6 adapter and select **Modify Network Port** from the pop-up menu.
8. Select a **Config type** of **Static** on the **Modify Network Port** screen.
9. Enter a primary private IP address, subnet, and gateway for the adapter. Use an address from the Storage row if you are using the VLAN worksheet from the [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) cookbook.
10. Clear the **iSCSI Enabled** check box to disable iSCSI connections to this adapter.
11. Right-click the private adapter and select **Enable Network Port** to bring the adapter online after you configure it with an IP address.
12. Click **OK** to enable the port upon verifying the IP address.

### Opening a support ticket

You need to open a support ticket after you configure a second adapter with a primary private IP address. Opening the ticket helps make sure that the IP address that you used is not taken if another machine is provisioned on the VLAN.

1. Click **Support** > **Add Ticket** and enter the following information:
  * Subject: Private network question
  * Title: Reserve and assign private IP address
  * Associate Devices: 'Select the QuantaStor server'
  * Details: Reserve and assign on VLAN. This IP address is used for the second adapter on the QuantaStor server.

### Configuring QuantaStor

Now that the array can accept connections from both adapters, the adapters’ virtual interfaces that are on the Storage Path A and Storage Path B subnets must be assigned.

  1. Right-click the initial private adapter interface (eth4) and select **Create Virtual Interface** on the pop-up menu.
  2. Enter a portable private IP address and subnet for the adapter on the resulting pop-up screen, and make sure that **iSCSI Enabled** is checked.
  3. Use an address from the Storage Path A row if you are using the VLAN worksheet.
  4. Record the IP address that is used in the Notes section on the Portable IP address page.
  5. Select the initial private adapter interface (eth4) to bind the virtual interface and click **OK**.
  6. Right-click the other private adapter interface (eth6) and select **Create Virtual Interface** on the pop-up menu.
  7. Enter a portable private IP address and subnet for the adapter and make sure that **iSCSI enabled** is checked on the resulting pop-up window.
  8. Use an address from the Storage Path B row if you are using the VLAN worksheet.
  9. Record this IP address as used in the Notes section on the Portable IP address page.
  10. Select the other private adapter interface (eth6) to bind the virtual interface and click **OK**.

After the QuantaStor server is configured with IP addresses and virtual interfaces, you need to configure the routing to make sure that the outgoing traffic uses the correct interface. The two NICs are on different subnets.

1. SSH into the QuantaStor server with your root credentials and append the following lines to /etc/network/interfaces. Assuming eth4 and eth6 are the NICs on the private network:
  * post-up ip route add 10.0.0.0/8 via dev eth4
  * post-up ip route add 10.0.0.0/8 via dev eth6 table eth6
  * post-up ip rule add from table eth6

### Creating a storage pool

Next, you must create a storage pool that is used to allocate volumes before you can create volumes or shares.

1. Right-click **Storage Pools** and select **Create Storage Pool**.
2. Enter the following information on the **Create Storage Pool** screen:
  * Name: Enter the appropriate name for the storage pool. Example: StoragePool-01
  * Pool Type: Default (zfs)
  * I/O Profile: Virtualization
  * Disks to use for the Storage Pool: sdb
3. Click **OK**.

If sdb is not available to add to a pool, it is due to a partition that exists and is being tagged as bootable. You need to use gdisk on the Quantastor console to remove the partition and any /etc/fstab entries. Next, you need to create volumes for ESXi to consume.

### Creating iSCSI storage volumes

You need to create two storage volumes. One volume is used for management VMs on the management cluster and the other for VMs on the capacity cluster. Complete the following steps to create the iSCSI storage volumes:

1. Right-click **Storage Volumes** and select **Create Storage Volume** on the pop-up menu.
2. Enter the information for the storage volumes. **Note:** While your configuration might differ depending on workload and storage capacity, the example shows the values in Table 1 and Table 2 for each storage volume.

|Field|Value|
|---|---|
|Name|Mgmt-LUN0|
|Storage Pool|[Storage Pool Name configured in the previous step]|
|Size|500GB|
|% Reserved|50|
|Compression|Enabled|
{: caption="Table 1. iSCSI Management Volume" caption-side="top"}

|Field|Value|
|---|---|
|Name|Capacity-LUN0|
|Storage Pool|[Storage Pool Name configured in the previous step]|
|Size|3TB|
|% Reserved|50|
|Compression|Enabled|
{: caption="Table 2. iSCSI Capacity Volume" caption-side="top"}

### Assigning host access to volumes

You need to configure QuantaStor to allow access from the ESXi hosts through each host’s IQN after the volumes are set up.

1. Navigate to the QuantaStor administration page and right-click the **Hosts** menu and select **Add Host**.
2. Enter the following information on the **Add Host** screen:
  * Host Name: Enter an appropriate host name. The host name does not have the fully qualified domain name (FQDN), but needs describe the host. Example: MyESXiHostName
  * Operating System Type: VMware
  * Initator: iSCSI Qualified Name (IQN) radio button
  * iSCSI Qualified Name: The IQN for the respective host.
3. Click **OK**.

Follow these steps for each management and capacity host in ESXi environment.

After you add each host in the management and capacity clusters, follow these steps:

1. Right-click the **Host Groups** menu and select **Create Host Group…**.
2. Enter 'ManagementCluster' in the **Name** field and select all the hosts that are in the management cluster.
3. Click **OK**. A host group is created that you can assign to a particular volume.

Repeat this process for the capacity cluster.

1. Click the **Storage Volumes** menu.
2. Right-click the **Mgmt-Lun0** volume and select **Assign / Unassign Host Access**.
3. Confirm that **Mgmt-Lun0** is an option in the drop-down menu and select the host group that you created in the previous step. This option allows each ESXi host in the management cluster to access the Mgmt-Lun0 volume. Do the same for **Capacity-LUN0**

## Step 4: Mounting volumes on capacity clusters

Log in to the vSphere Web Client and go to **Hosts** under the **vCenter Inventory Lists**.

Use the following steps to mount the volume on the ESXi hosts:

1. Select a host and click **Manage, Storage,** > **Storage Adapters**.
2. Select **Targets** > **Dynamic Discovery** > **Add…**.
3. Enter the IP address that is assigned to the QuantaStor storage device on Storage Path A on the **Add Send Target Server** screen.
4. Leave **3260** as the Port and click **OK**.
5. Click **Dynamic Discovery** > **Add…**. Repeat steps 4 and 5 for Storage Path B.

The ESXI host is ready to rescan the iSCSI Software Adapter to discover the Mgmt-Lun0 volume.

1. Select the **Rescan Storage Adapters** icon (Figure 9) on the **Storage Adapters** screen.
2. Leave the default option on the resulting pop-up screen and click **OK**.
3. Click **Actions, New Data store** after the volume is discovered and format it as **VMFS-5**.
4. Confirm that the formatting is complete and click **Storage Devices, Device Details, Edit Multipathing…**.
5. Select **Round Robin** for the **Path Selection Policy** and click **OK**.

Now that the Mgmt-Lun0 volume is attached to a single host, you must go back to the other management hosts in the cluster and repeat the process to add the volume. However, you do not need to format the volume as it already formatted with VMFS-5 and is displayed as such after discovery.

## Step 5: Disabling delayed ACK in vSphere ESXi hosts

The delayed ACK needs to be disabled once the storage LUNs are attached to the management and capacity hosts.

1. Go to the vSphere environment and select **Storage Adapters** > **iSCSI Software Adapter** > **Advanced Options**.
2. Click **Edit** and scroll all the way to the end of the Advanced Options screen.
3. Clear the **DelayedAck** check box and click **OK**.

For more information about delayed ACK regarding VMware, see [VMware’s Knowledge Base](https://kb.vmware.com/s/article/1002598).

You can now return to [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) cookbook and complete the environment setup.
