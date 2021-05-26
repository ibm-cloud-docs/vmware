---

copyright:
  years: 2017, 2021
lastupdated: "2021-05-26"

keywords: Getting Started VMware vSphere 6

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:external: .external}

# Getting Started with VMware vSphere 6
{: #get-started-vsphere-6}

Use the following to get started with vSphere 6.

## Understanding the environment and configuration
{: #vsphere-environment-config}

To optimize your VMware solution it is recommended that you use a Private Network VLAN and Public (Optional, Public Port can be disabled if not needed) for your VMware vSphere environment. This provisioning profile allows for the following Layer 2 segment traffic boundaries:

|Example VLAN ID|Description|Type|Additional detail|
|---|---|---|---|
|VLAN1 - **1101**|Management, VxLAN|Private BCR|Native untagged VLAN, original native VLAN that the VMWare hosts are deployed into at the time of ordering|
|VLAN4 - **2200**|Public internet access DMZ|Public FCR|Native untagged VLAN, original native VLAN that the VMWare hosts are deployed into at the time of ordering|
{: caption="Table 1. Private and public VLAN examples" caption-side="top"}

## Before you begin
{: #before-you-begin-vmware-vsphere}
* Navigate to your console's device menu. For more information, see [Navigating to devices](/docs/bare-metal?topic=virtual-servers-navigating-devices).
* Make sure that you have any necessary account permissions and device access. Only the account owner, or a user with the **Manage Users** classic infrastructure permission, can adjust the permissions.

For more information about permissions, see [Classic infrastructure permissions](/docs/account?topic=account-infrapermission#infrapermission) and [Managing device access](/docs/virtual-servers?topic=virtual-servers-managing-device-access).

## Placing your order for vSphere Servers
{: #order-vsphere-servers}

1. Click **Devices > Device List**.
2. Click **Order Devices**
3. In the **Compute** category, click **Bare Metal Servers**.
3. In the **Bare Metal Server** section, click **Monthly**.
4. Select the servers. See VMware Support publications for minimum requirements:
  * The following servers were selected for the example. **Note:** Having dual unbonded public and private uplinks is a requirement for redundancy. Confirm that the data center where you created your VLANs contain unbonded uplinks. 
  * Capacity Cluster (Quantity: 2)
    * Server configuration: Select an Intel Xeon v3 server from the 'Dual processor multi-core Servers' section
    * Software: OS = VMware 6.0
    * OS Storage: 2 x 1 TB SATA (configured as a RAID 1)
    * Data Storage: Recommend ordering 2 TB SATA or 1.2 TB SSD or Endurance / Performance NFS SAN Storage
      * If you are interested in other storage types, see [Storage to use with VMware Systems](/docs/vmware?topic=vmware-vmware-storage#vmware-storage)
      * Uplink Port Speeds: 1 Gbps Dual Public and Private Networks (Unbonded)
        * 10 Gbps Uplinks are recommended for VMware vSAN solutions
5. If you are creating a new deployment in a new IBM Cloud data center, proceed to step 6. If this deployment is an expansion or a deployment into an existing Data Center, select the preferred Backend BCR VLAN + Frontend FCR VLAN. For the example, the Backend BCR VLAN is 1101 and the Frontend FCR VLAN is 2200. **Note:** If this deployment is new or a new deployment into a new DC the Backend BCR and Frontend FCR VLANs are created when you order the server.
6. Enter a **Host name** and **Domain**.
7. Review the order and click **Finalize Your Order** to start the provisioning process.

## Ordering vCenter Server
{: #order-vcenter-server}

vCenter is an add-on to a Windows Server. This configuration scales up to 20 vSphere hosts. For larger implementations, deployment of the vCenter Server Appliance (VCSA) [Deploy and Configure a vCenter Server Appliance (vCSA)](/docs/vmware?topic=vmware-config-vcsa#config-vcsa) directly to a vSphere cluster is recommended.

Use the following steps to order a virtual server with vCenter installed:

1. Click **Devices > Device list**.
2. Click **Order devices**
3. In the **Compute** category, click either **Bare metal servers** or **Virtual Server**. Select the **Monthly*8 billing option.
  1. For a virtual server instance to qualify for vCenter 6.0, you must deploy on at least **4 x 2.0 GHz Cores** and **4 GB of RAM**
  2. For a listing of vCenter Deployment recommendations, see the [VMware vCenter Server&trade; 6.0 Deployment Guide](https://www.vmware.com/content/dam/digitalmarketing/vmware/en/pdf/techpaper/vmware-vcenter-server6-deployment-guide-white-paper.pdf){: external}.
4. Enter the following information:
  * Based on the Recommended Minimum Server Configuration
    * vCPU Core Configuration: 4 x 2.0 GHz Cores
    * RAM Configuration: 12 GB RAM
    * Software: OS = Windows Server 2012 R2 Standard Edition (64 Bit)
    * OS-Specific Addon: vCenter 6
    * First Disk  : 1 x 100 GB (SAN)
    * Second Disk : 1 x  50 GB (SAN)
    * Uplink Port Speeds: 1 Gbps Public and Private Network Uplinks

5. If this deployment is new, proceed to step 6. If this deployment is an expansion or deployment in to a existing data center, select the preferred backend BCR VLAN + frontend FCR VLAN. For our example, our backend BCR VLAN is 1101 and the frontend FCR VLAN is 2200. (If this is a new deployment or a new deployment into a new DC the backend BCR and frontend FCR VLANs are created when you order the server)
6. Enter a **Host name** and **Domain**.
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

|Subnet Type|subnet size|Bound Vlan|vSphere host usage|
|---|---|---|---|
|Portable - Private|/27 32 Address|**1101**|Management VMs|
|Portable - Private|/27 32 Address|**1101**|VM kernel ports for iSCSI and vMotion|
|Portable - Private|/27 32 Address|**1101**|Private IPs for Guest VM|
|Portable - Public|/27 32 Address|**2200**|Public IPs for Guest VMs (Optional)|
{: caption="Table 2. Subnets" caption-side="top"}

### Optional – Disabling the public interface on the vSphere host

You can disable the vSphere public interfaces for security purposes if you are not going to use them.

1. Click **Devices > Device List**.
2. Click the name of your vSphere Host.
3. Click the Configuration table and scroll down to the Network section.
4. Select **Disconnect** for each applicable vSphere host eth1 and eth3 pairs for all hosts.

## Creating and configuring vSphere data center cluster
{: #create-config-vsphere-data-center-cluster}

You can now log in to the vCenter server and configure the vSphere cluster.

1. Click **Devices > Device List**
2. Find your vCenter device and click its name.
3. Scroll down the **Device Details** screen to the **Network** section of the server and make note of the **Private IP Address**.
4. Scroll down the **Device Details** screen and note the **Passwords** for both the Windows OS and vCenter software.
5. Open a Microsoft Remote Desktop (RDP) session and connect to your vCenter server through its public IP address.
6. Log in using the passwords that you obtained in step 4. **Note:** You need an active VPN connection to IBM Cloud needs if you use a private IP address to access vCenter. For more information about VPN access, see [Enabling SSL VPN access](/docs/iaas-vpn?topic=iaas-vpn-getting-started).
7. Download and install the traditional [vSphere Client](https://kb.vmware.com/s/){: external} or use the vSphere web client by using following the link `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/`.
8. Log in to vCenter with the IP address and passwords you obtained in steps 3 and 4.
9. Right-click the vCenter server name in the left pane and select **New Datacenter**.
10. Enter an appropriate name for the data center.
11. Right-click on the data center and select **New Cluster**.
12. Enter a cluster name. DO NOT turn on Cluster Features, vSphere HA or vSphere DRS.
13. Click **Next**.
14. Leave **EVC** disabled and click **Next**.
15. Accept the _default to store the swapfile in the same directory as the virtual machine_ and click **Next**.
16. Click **Finish** to complete the cluster.
17. Right-click the newly created cluster and select **Add Host**.
18. Enter the IP address or hostname of one of the vSphere hosts and enter **Root** in the **User name** field and the password for the host in the **Password** field.
19. Click **Next** though the Host Summary, Assign License, Lockdown Mode screen, and click **Finish** to complete adding your host to the Cluster
20. Repeat steps 18 and 19 for each other vSphere hosts in your cluster. You will see each vSphere hosts under the new cluster after you are done.

### Configuring the basic network construct for the vSphere hosts

Use the following steps to configure the basic construct for the vSphere hosts in your cluster.

1. Select the first vSphere host and click the **Configuration** tab.
2. Under **Hardware** section, select **Networking** and click **Properties** next to vSwitch0.
3. Select **Network Adapters** on the **vSwitch Properties** window and click **Add**.
4. Select vmnic2 to add to vSwitch0 and click **Next**.
5. Make sure that both vmnics are **Active Adapters** and click **Next**.
6. Click **Finish**.
7. Click the **Ports** tab and make sure vSwitch is highlighted and click **Edit**.
8. Click the **General** Tab and change the **MTU** to 9000 (Jumbo Frame).
9. Click the **NIC Teaming** tab and change the load balancing to **Route based on IP** hash and click **OK**.
10. Use steps 1 - 8 to configure the vmnics for the other vSphere hosts in your cluster.

A port group now needs to be added for vMotion. The group can be created as a Virtual Standard Switch (VSS) or Virtual Distributed Switch (VDS). Use the following steps to create a VSS switch.

1. Select the **Configuration** tab and select **Networking**.
2. Click **Properties...** for vSwitch0.
3. Click **Add...** to create a Port Group.
4. Select **VMkernel** and click **Next**.
5. Complete **Port Group Properties** with the following information:
  * **Network Label:** An appropriate name for the port group.
  * **VLAN ID (Optional):** The VLAN ID for vMotion traffic (1101 for our example). The VLAN ID allows VMware to tag the traffic for the specific VLAN.
  * Select **Use this port group for vMotion**.
6. Click **Next**.
7. Enter a **Portable IP address** for the VLAN. (You can get the port IP address from the control portal, **Network > IP Management > VLANs**. Select the correct VLAN and under **Subnets** you see a portable IP address range. If you have no available Portable IP address or if you exhausted your current pool, follow the steps in 'Order Private Subnets / IP addresses ' to order extra portable IP address
8. Click **Next** and then **Finish** to complete.

Use the following steps to create a port group for VM data traffic.

1. Click **Properties...** for vSwitch0 and select **Add, Virtual Machine**.
2. Complete the **Port Group Properties** with the following information:
  * **Network Label:** Enter the name of the port group, such as `VM Data`.
  * **VLAN ID (Optional):** Enter a VLAN ID; we used 1101 for our example. The VLAN ID allows VMware to tag the traffic for the VLAN.

### Optional - Installing add-on VMware licenses (NSX, vRealize, vSAN, etc.)

Now that the VMware environment is up you are ready to continue with the deployment of extra configurations, Guest VMs or VMware add-ons. Licenses for VMware add-ons can also be purchased through the IBM Cloud control portal and added through your vCenter Console.

## Next steps
{: vsphere-next-steps}
You now have a basic single-site VMware environment that is running in an IBM Cloud data center. The basic configuration has only a local datastore, making it a simplified configuration that does not contain features such as VMware DRS, HA, Storage DRS, and a firewall.

For more information, see [FAQs: VMware](/docs/vmware?topic=vmware-vmware-faq#vmware-faq).
