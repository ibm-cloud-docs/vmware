---

copyright:
  years: 2017, 2024
lastupdated: "2024-07-11"

keywords: Getting Started VMware vSphere

subcollection: vmware

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with VMware vSphere
{: #get-started-vsphere-6}

Use the following information to get started with VMware&reg; vSphere.
{: shortdesc}

## Understanding the environment and configuration
{: #vsphere-environment-config}

To optimize your VMware solution, it is recommended that you use a private network VLAN for your VMware vSphere environment. You can use the provisioning profile for the following Layer 2 segment traffic boundaries:

|Example VLAN ID|Description|Type|Extra detail|
|---|---|---|---|
|VLAN1 - **1101**|Management, VxLAN|Private BCR|Native untagged VLAN, the original native VLAN that the VMware hosts are deployed into at the time of ordering|
|VLAN4 - **2200**|Public internet access DMZ|Public FCR|Native untagged VLAN, the original native VLAN that the VMware hosts are deployed into at the time of ordering|
{: caption="Table 1. Private and public VLAN examples" caption-side="top"}

## Before you begin
{: #before-you-begin-vmware-vsphere}

Make sure that you have any necessary account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions.

## Ordering vSphere servers
{: #order-vsphere-servers}

1. Click **Devices > Device list**.
2. Click **Order devices**
3. In the **Compute** category, click **Bare Metal Servers**.
3. In the **Bare Metal Server** section, click **Monthly**.
4. Select the servers. See VMware Support publications for minimum requirements:
   * The following servers were selected for the example. Keep in mind that having dual unbonded public and private uplinks is a requirement for redundancy. Confirm that the data center where you created your VLANs contain unbonded uplinks.
   * Capacity Cluster (Quantity 2)
      - Server configuration - Select an Intel&reg; Xeon v3 server from the 'Dual processor multi-core Servers' section
      - Software is OS = VMware
      - OS Storage is 2 x 1 TB SATA (configured as a RAID 1)
      - Data Storage - Recommend ordering 2 TB SATA or 1.2 TB SSD or Endurance or Performance NFS SAN Storage
         * If you are interested in other storage types, see [Storage to use with VMware Systems](/docs/vmware?topic=vmware-vmware-storage#vmware-storage)
         * Uplink Port Speeds: 1 Gbps Dual Public and Private Networks (Unbonded)
            * 10 Gbps Uplinks are recommended for VMware vSAN solutions
5. If you are creating a new deployment in a new {{site.data.keyword.cloud}} data center, proceed to step 6. If this deployment is an expansion or a deployment into an existing Data Center, select the preferred back-end BCR VLAN + front-end FCR VLAN. For the example, the back-end BCR VLAN is 1101 and the front-end FCR VLAN is 2200. **Note:** If this deployment is new or a new deployment into a new DC the back-end BCR and front-end FCR VLANs are created when you order the server.
6. Enter a **Hostname** and **Domain**.
7. Review the order and click **Finalize Your Order** to start the provisioning process.

## Ordering vCenter Server
{: #order-vcenter-server}

vCenter is an add-on to a Windows Server. This configuration scales up to 20 vSphere hosts. For larger implementations, deployment of the vCenter Server Appliance (VCSA) [Deploy and Configure a vCenter Server Appliance (vCSA)](/docs/vmware?topic=vmware-config-vcsa#config-vcsa) directly to a vSphere cluster is recommended.

Use the following steps to order a virtual server with vCenter.

1. Click **Devices > Device list**.
2. Click **Order devices**
3. In the **Compute** category, click either **Bare metal servers** or **Virtual Server**. Select the **Monthly** billing option.
   1. For a virtual server instance to qualify for vCenter, you must deploy on at least **4 x 2.0 GHz Cores** and **4 GB of RAM**
   2. For a listing of vCenter Deployment recommendations, see the [VMware vCenter Server Deployment Guide](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/vmware-vcenter-server6-deployment-guide-white-paper.pdf){: external}.
4. Enter the following information:
   * Based on the Recommended Minimum Server Configuration
      * vCPU Core Configuration: 4 x 2.0 GHz Cores
      * RAM Configuration: 12 GB RAM
      * Software - OS = Windows&reg; Server 2012 R2 Standard Edition (64 Bit)
      * OS-Specific Addon: vCenter
      * First Disk - 1 x 100 GB (SAN)
      * Second Disk - 1 x 50 GB (SAN)
      * Uplink Port Speeds: 1 Gbps Public and Private Network Uplinks

5. If this deployment is new, proceed to step 6. If this deployment is an expansion or deployment in to an existing data center, select the preferred back-end BCR VLAN + front-end FCR VLAN. For our example, our back-end BCR VLAN is 1101 and the front-end FCR VLAN is 2200. **Note:** If this deployment is new or if it's a new deployment into a new DC, the back-end BCR and front-end FCR VLANs are created when you order the server)
6. Enter a **Hostname** and **Domain**.
7. Review the order and click **Finalize your order** to start the provisioning process.

## Ordering portable public and private subnets and IP addresses
{: #order-public-private-subnet}

**Note:** Do not proceed if the VLANs are not provisioned.

The subnets are used for addressing VMware Guest virtual machine (VM) and VMware host kernel-based traffic.

1. Click **Network > IP Management > Subnets**.
2. Click **Order IP addresses** on the upper right of the screen.
3. Select **Portable Private**.
4. Select the appropriate VLAN (Example: bcr01.wdc04: 1101)
5. Click **Continue**.
6. Complete the **Order IP address** form.
7. Click **Order IP addresses** on the upper right of the screen.
8. Click **Place order**.
9. Follow this process for each applicable VLAN (Ex. 1101, 2200)
   1. For more information about VLANs, see [Getting started with VLANs](/docs/vlans?topic=vlans-getting-started).

|Subnet Type|Subnet size|Bound VLAN|vSphere host usage|
|---|---|---|---|
|Portable - Private|/27 32 Address|**1101**|Management VMs|
|Portable - Private|/27 32 Address|**1101**|VM kernel ports for iSCSI and vMotion|
|Portable - Private|/27 32 Address|**1101**|Private IPs for Guest VM|
|Portable - Public |/27 32 Address|**2200**|Public IPs for Guest VMs (Optional)|
{: caption="Table 2. Subnets" caption-side="top"}

### Optional – Disabling the public interface on the vSphere host

You can disable the vSphere public interfaces for security purposes if you aren't using them.

1. Click **Devices > Device list**.
2. Click the name of your vSphere host.
3. Click the Configuration table and scroll down to the Network section.
4. Select **Disconnect** for each applicable vSphere host eth1 and eth3 pairs for all hosts.

## Creating and configuring vSphere data center cluster
{: #create-config-vsphere-data-center-cluster}

You can now log in to the vCenter server and configure the vSphere cluster.

1. Click **Devices > Device list**
2. Find your vCenter device and click its name.
3. Scroll down the **Device details** screen to the **Network** section of the server and make note of the **Private IP address**.
4. Scroll down the **Device details** screen and note the **Passwords** for both the Windows OS and vCenter software.
5. Open a Microsoft&reg; Remote Desktop (RDP) session and connect to your vCenter server through its public IP address.
6. Log in by using the passwords that you obtained in step 4. **Note:** You need an active VPN connection to {{site.data.keyword.cloud}} needs if you use a private IP address to access vCenter. For more information about VPN access, see [Enabling SSL VPN access](/docs/iaas-vpn?topic=iaas-vpn-getting-started).
7. Download and install the traditional vSphere client or use the vSphere web client by using following the link `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/`.
8. Log in to vCenter with the IP address and passwords that you obtained in steps 3 and 4.
9. Right-click the vCenter server name in the left pane and select **New data center**.
10. Enter an appropriate name for the data center.
11. Right-click on the data center and select **New cluster**.
12. Enter a cluster name. DO NOT turn on Cluster Features, vSphere HA or vSphere DRS.
13. Click **Next**.
14. Leave **EVC** disabled and click **Next**.
15. Accept the _default to store the swapfile in the same directory as the virtual machine_ and click **Next**.
16. Click **Finish** to complete the cluster.
17. Right-click the newly created cluster and select **Add Host**.
18. Enter the IP address or hostname of one of the vSphere hosts and enter **Root** in the **Username** field and the password for the host in the **Password** field.
19. Click **Next** through the Host Summary, Assign License, Lockdown Mode screen, and click **Finish** to complete adding your host to the Cluster
20. Repeat steps 18 and 19 for each other vSphere hosts in your cluster. You can see each vSphere hosts under the new cluster after you are done.

### Configuring the basic network construct for the vSphere hosts

Use the following steps to configure the basic construct for the vSphere hosts in your cluster.

1. Select the first vSphere host and click the **Configuration** tab.
2. Under the **Hardware** section, select **Networking** and click **Properties** next to vSwitch0.
3. Select **Network adapters** on the **vSwitch properties** window and click **Add**.
4. Select vmnic2 to add to vSwitch0 and click **Next**.
5. Make sure that both vmnics are **Active adapters** and click **Next**.
6. Click **Finish**.
7. Click the **Ports** tab and make sure that vSwitch is highlighted and click **Edit**.
8. Click the **General** Tab and change the **MTU** to 9000 (jumbo frame).
9. Click the **NIC teaming** tab and change the load balancing to **Route based on IP** hash and click **OK**.
10. Use steps 1 - 8 to configure the vmnics for the other vSphere hosts in your cluster.

Now, you need to add a port group for vMotion. You can create the group with a Virtual Standard Switch (VSS) or Virtual Distributed Switch (VDS). Use the following steps to create a VSS switch.

1. Select the **Configuration** tab and select **Networking**.
2. Click **Properties...** for vSwitch0.
3. Click **Add...** to create a Port Group.
4. Select **VMkernel** and click **Next**.
5. Complete **Port group properties** with the following information:
   * **Network label:** An appropriate name for the port group.
   * **VLAN ID (Optional):** The VLAN ID for vMotion traffic (1101 for our example). The VLAN ID allows VMware to tag the traffic for the specific VLAN.
   * Select **Use this port group for vMotion**.
6. Click **Next**.
7. Enter a **Portable IP address** for the VLAN. (You can get the port IP address from the control portal, **Network > IP management > VLANs**. Select the correct VLAN and under **Subnets** that you see a portable IP address range. If you have no available portable IP address or if you exhausted your current pool, follow the steps that are in 'Order private subnets and IP addresses' to order extra portable IP addresses.
8. Click **Next** and then **Finish** to complete.

Use the following steps to create a port group for VM data traffic.

1. Click **Properties...** for vSwitch0 and select **Add virtual machine**.
2. Complete the **Port group properties** with the following information:
   * **Network label:** Enter the name of the port group, such as `VM Data`.
   * **VLAN ID (Optional):** Enter a VLAN ID; 1101 was used for the example. The VLAN ID gives access to VMware to tag the traffic for the VLAN.

### Optional - Installing add-on VMware licenses (NSX, vRealize, vSAN)

Now that the VMware environment is up you are ready to continue with the deployment of extra configurations, guest VMs or VMware add-ons. Licenses for VMware add-ons can also be purchased through the {{site.data.keyword.cloud}} control portal and added through your vCenter Console.

## Next steps
{: vsphere-next-steps}

You now have a basic single-site VMware environment that is running in an {{site.data.keyword.cloud}} data center. The basic configuration has only a local data store, making it a simplified configuration that does not contain features such as VMware DRS, HA, Storage DRS, and a firewall.

For more information, see the [FAQs: VMware](/docs/vmware?topic=vmware-vmware-faq#vmware-faq).
