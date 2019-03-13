---

copyright:
  years: 1994, 2019
lastupdated: "2018-06-25"

keywords: Getting Started VMware vSphere 6

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Getting Started with VMware vSphere 6
{: #get-started-vsphere-6}

Use the following to get started with vSphere 6.

## Understanding the environment and configuration
{: #vsphere-environment-config}

To optimize your VMware solution it is recommended that you use a Private Network VLAN and Public (Optional, Public Port can be disabled if not needed) for your VMware vSphere environment. This provisioning profile allows for the following Layer 2 segment traffic boundaries:

|Example VLAN ID|Description|Type|Additional Detail|
|---|---|---|---|
|VLAN1 - **1101**|Management, VxLAN|Private BCR|Native Untagged VLAN, Original Native VLAN that the VMWare Hosts are deployed into at the time of ordering|
|VLAN4 - **2200**|Public Internet Access DMZ|Public FCR|Native Untagged VLAN, Original Native VLAN that the VMWare Hosts are deployed into at the time of ordering|
{: caption="Table 1. Private and Public VLAN examples" caption-side="top"}

## Placing your order for vSphere Servers
{: #order-vsphere-servers}

1. Log in to the [{{site.data.keyword.slportal_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://control.softlayer.com/){: new_window}.
2. Click **Account > Place an Order**.
3. In the **Bare Metal Server** section, click **Monthly**.
4. Select the servers. See VMware Support publications for minimum requirements:
  * The following servers were selected for the example. **Note:** Having dual unbonded public and private uplinks is a requirement for redundancy. Confirm that the data center where you created your VLANs have unbonded uplinks.  
  * Capacity Cluster (Quantity: 2)
    * Server configuration: Select a Intel Xeon v3 server from the 'Dual Processor Multi-Core Servers' section
    * Software: OS = vSphere Enterprise Plus 6
    * OS Storage: 2 x 1 TB SATA (configured as a RAID 1)
    * Data Storage : Recommend to order 2 TB SATA or 1.2 TB SSD or Endurance / Performance NFS SAN Storage
      * If you are interested in other storage types, see [Storage to use with VMware Systems](/docs/infrastructure/vmware?topic=VMware-storage-to-use-with-vmware-systems)
      * Uplink Port Speeds: 1 Gbps Dual Public and Private Networks (Unbonded)
        * 10 Gbps Uplinks are recommended for VMware vSAN solutions
5. If you are creating a new deployment in a new IBM Cloud data center, proceed to step 6. If this is a expansion or a deployment into a existing Data Center, select the preferred Backend BCR VLAN + Frontend FCR VLAN. For the example, the Backend BCR VLAN is 1101 and the Frontend FCR VLAN is 2200. **Note:** If this is a new deployment or a new deployment into a new DC the Backend BCR and Frontend FCR VLANs are created when you order the server.
6. Enter a **Hostname** and **Domain**.
7. Review the order and click **Finalize Your Order** to start the provisioning process.

## Placing your order for vCenter Server
{: #order-vcenter-server}

vCenter is an add-on to a Windows Server.  This configuration scales up to 20 vSphere hosts.  For larger implementations, deployment of the vCenter Server Appliance (VCSA) [Deploy and Configure a vCenter Server Appliance (vCSA)](/docs/infrastructure/vmware?topic=VMware-deploying-and-configuring-a-vcenter-server-appliance-vcsa-with-vmware-vsphere-6-deploying-and-configuring-should-each-be-a-separate-topic-) directly to a vSphere cluster is recommended.

Use the following steps to order a virtual server with vCenter installed:

1. Log in to the {{site.data.keyword.slportal_short}}.
2. Click **Account > Place an Order**.
3. Order either a **Monthly** Bare Metal or Virtual Server public/private node Instance (VSI) under Virtual Servers.
  1. For a SoftLayer Virtual Server Instance (VSI) to qualify for vCenter 6.0, you must deploy on at least **4 x 2.0 GHz Cores** and **4 GB of RAM**
  2. For a listing of vCenter Deployment recommendations, see the [VMware vCenter Server&trade; 6.0 Deployment Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}.
4. Enter the following information:
  * Based on the Recommended Minimum Server Configuration
    * vCPU Core Configuration: 4 x 2.0 GHz Cores
    * RAM Configuration: 12 GB RAM
    * Software: OS = Windows Server 2012 R2 Standard Edition (64 Bit)
    * OS-Specific Addon: vCenter 6
    * First Disk  : 1 x 100 GB (SAN)
    * Second Disk : 1 x  50 GB (SAN)
    * Uplink Port Speeds: 1 Gbps Public and Private Network Uplinks

5. If this is a new deployment into a new IBM Cloud Data Center proceed to step 6. If this deployment is an expansion or deployment in to a existing Data Center, select the preferred Backend BCR VLAN + Frontend FCR VLAN. For our example, our Backend BCR VLAN is 1101 and the Frontend FCR VLAN is 2200. (If this is a brand new deployment or a new deployment into a new DC the Backend BCR and Frontend FCR VLANs are created when you order the server)
6. Enter a **Hostname** and **Domain**.
7. Review the order and click **Finalize Your Order** to start the provisioning process.

## Ordering Portable Public and Private Subnets / IP addresses
{: #order-public-private-subnet}

**Note:** Do not proceed if the VLANs have not been completely provisioned.

The subnets are used for addressing VMware Guest Virtual Machine (VM) and VMware Host kernel-based traffic.

1. From the Control Portal, click **Network > IP Management > Subnets**.
2. Click **Order IP Addresses** on the upper right of the screen.
3. Select **Portable Private**.
4. Select the appropriate VLAN (Example: bcr01.wdc04: 1101)
5. Click **Continue**.
6. Complete the **Order IP Address** form.
7. Click **Order IP Addresses** on the upper right of the screen.
8. Click **Place Order**.
9. Follow this process for each applicable VLAN (Ex. 1101, 2200)
  1. For more information about VLANs, see [Getting started with VLANs](/docs/infrastructure/vlans?topic=vlans-getting-started-with-vlans).

|Subnet Type|subnet size|Bound Vlan|vSphere host usage|
|---|---|---|---|
|Portable - Private|/27 32 Address|**1101**|Management VMs|
|Portable - Private|/27 32 Address|**1101**|VM kernel ports for iSCSI and vMotion|
|Portable - Private|/27 32 Address|**1101**|Private IPs for Guest VM|
|Portable - Public|/27 32 Address|**2200**|Public IPs for Guest VMs (Optional)|
{: caption="Table 2. Subnets" caption-side="top"}

### Optional – Disabling the public interface on the vSphere host

You can disable the vSphere public interfaces for security purposes if you are not going to use them.

1. From the Control Portal, click **Devices > Device List**.
2. Click the name of your vSphere Host.
3. Click the Configuration table and scroll down to the Network section.
4. Select **Disconnect** for each applicable vSphere host eth1 and eth3 pairs for all hosts

<!--This can also be performed through the [{{site.data.keyword.slapi_full}} ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sldn.softlayer.com/reference/services/softlayer_hardware_server/shutdownpublicport){: new_window}.-->

## Creating and Configuring vSphere Data Center Cluster 
{: #create-config-vsphere-data-center-cluster}

You can now log in to the vCenter server and configure the vSphere Cluster.

1. From the Control Portal, click **Devices > Device List**
2. Find your vCenter device and click its name.
3. Scroll down the **Device Details** screen to the **Network** section of the server and make note of the **Private IP Address**.
4. Scroll down the **Device Details** screen and note the **Passwords** for both the Windows OS and vCenter Software.
5. Open a Microsoft Remote Desktop (RDP) session and connect to your vCenter Server via its Public IP address.
6. Log in using the passwords that you obtained in step 4. **Note:** An active VPN connection to IBM Cloud will need to be in place if the Private IP Address is used to access vCenter. For more information about VPN access, see [Enable access to the IBM Cloud infrastructure private network](/docs/customer-portal?topic=customer-portal-getting-started#enable-private-network).
7. Download and install the traditional [vSphere Client ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window} or use the vSphere Web Client via the link `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/`.
8. Log in to vCenter with the IP Address and passwords you obtained in steps 3 and 4.
9. Right-click the vCenter server name in the left pane and select **New Datacenter**.
10. Enter an appropriate name for the data center.
11. Right-click on the data center and select **New Cluster**.
12. Enter a cluster name. DO NOT turn on Cluster Features, vSphere HA or vSphere DRS at this time.
13. Click **Next**.
14. Leave **EVC** disabled and click **Next**.
15. Accept the _default to store the swapfile in the same directory as the virtual machine_ and click **Next**.
16. Click **Finish** to complete the cluster.
17. Right-click the new cluster that you just created and select **Add Host**.
18. Enter the IP address or Hostname of one of the vSphere hosts and enter **Root** in the **Username** field and the password for the host in the **Password** field.
19. Click **Next** though the Host Summary, Assign License, Lockdown Mode screen, and click **Finish** to complete adding your host to the Cluster
20. Repeat steps 18 and 19 for each other vSphere hosts in your cluster. You will see each vSphere hosts under the new cluster after you are done.

### Configuring the basic network construct for the vSphere hosts

Use the following steps to configure the basic construct for the vSphere hosts in your cluster.

1. Select the first vSphere host and click the **Configuration** tab.
2. Under **Hardware** section, select **Networking**. You should already have vSwitch0 with vmnic0; click on **Properties** next to vSwitch0.
3. Select **Network Adapters** on the **vSwitch Properties** window and click the **Add** button.
4. Select vmnic2 to add to vSwitch0 and click **Next**.
5. Make sure both vmnics are **Active Adapters** and click **Next**.
6. Click **Finish**.
7. Click on the **Ports** tab and make sure vSwitch is highlighted; click on **Edit**.
8. Click on the **General** Tab and change the **MTU** to 9000 (Jumbo Frame).
9. Click on the **NIC Teaming** tab and change the load balancing to **Route Based on IP** hash and click **OK**.
10. Use steps 1 to 8 to configure the vmnics for the other vSphere hosts in your cluster.

A port group now needs to be added for vMotion. The group can be created as a Virtual Standard Switch (VSS) or Virtual Distributed Switch (VDS). For purpose of our example, we will create a VSS switch.

1. Select the **Configuration** tab and select **Networking**.
2. Click **Properties...** for vSwitch0.
3. Click **Add...** to create a Port Group.
4. Select **VMkernel** and click **Next**.
5. Fill in Port Group Properties with the following information:
  * **Network Label:** An approptiate name for the port group.
  * **VLAN ID (Optional):** The VLAN ID for vMotion traffic (1101 for our example). The VLAN ID will allow VMware to tag the traffic for the specific VLAN.
  * Select **Use this port group for vMotion**.
6. Click **Next**.
7. Enter a **Portable IP address** for the VLAN. (You can get the port IP address from the SoftLayer portal, **Network > IP Management > VLANs**. Select the correct VLAN and under **Subnets** you will see a portable IP address range. If you have no available Portable IP Address or if you have exhausted your current pool please follow the steps in the section 'Order Private Subnets / IP Addresses ' to order additional Portable IP address
8. Click **Next** and then **Finish** to complete.

Use the following steps to create a Port Group for VM data traffic.

1. Click **Properties...** for vSwitch0 and select **Add, Virtual Machine**.
2. Fill in the **Port Group Properties** with the following information:
  * **Network Label:** Enter the name of the Port Group, e.g., VM Data
  * **VLAN ID (Optional):** Enter a VLAN ID; we used 1101 for our example. The VLAN ID allows VMware to tag the traffic for the VLAN.

### Optional - Installing Add On VMware licenses (NSX, vRealize, vSAN, etc.)

Now that the VMware environment is up you are ready to continue with the deployment of additional configurations, Guest VMs or VMware Add Ons. Licenses for VMware Add Ons can also be purchased via the IBM Cloud control portal and added via your vCenter Console. <!--For more information about ordering and managing VMware Add On licenses, see [VMware vSphere 6 Ordering and Managing Licenses](vmware-vsphere-6-ordering-and-managing-licenses.html).-->

## Next Steps
{: vsphere-next-steps}
You now have a basic single-site VMware environment running in an IBM Cloud data center. The basic configuration has only a local datastore, making it a simplified configuration that does not contain features such as VMware DRS, HA, Storage DRS, and a firewall.

For more information, see [FAQs: VMware](/docs/infrastructure/vmware?topic=VMware-faqs-vmware). 
