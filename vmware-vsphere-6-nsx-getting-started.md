---

copyright:
  years: 1994, 2019
lastupdated: "2017-12-14"

keywords: getting started nsx, nsx license

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Getting Started with VMware vSphere 6 NSX
{: #getting-started-nsx} 

NSX is deployed as a license entitlement for you to apply to your infrastructure. {{site.data.keyword.BluSoftlayer_full}} supplies the licenses on a per-processor basis (pricing does not change for number of cores per CPU). An NSX license is required on every server that uses an NSX component (Management, Control, or Data Plane). NSX adds extra networking capabilities to the platform. You can create a robust overlay network for system security, tenant segmentation, and hybrid cloud environments that span providers or extends from on-premises private clouds.
{:shortdesc}

You can add firewalls, load balancing, VPN, NAT services, VXLAN-based micro segmentation to your environment with support for automation through a RESTful API.

## Adding Licenses
{: #add-nsx-license}
Licenses are added to the servers by using the following process:
1. Log in to vCenter Server with the vSphere Client.
* Under **Administration**, click **Licensing**.
* Click **Solutions**.
* In the product list, click **VMware NSX for vSphere**.
* Click **License Key** or **Enter New license key**.
* Click **OK**.

## Installing NSX
{: #install-nsx}

1. Deploy NSX Manager.
* Register NSX Manager with the vCenter Server.
* vSphere Web Client deploys the NSX Controller instances through NSX Manager.
* Prepare vSphere Hosts by using the NSX Manager to install the VIBs on the hosts in the cluster.
* After the NSX Controllers are deployed on all applicable Hosts, define and configure the NSX Components such as Edge Gateways, Load Balancers, and Firewalls.

## Deployment Considerations
{: #nsx-deployment-considerations}

Enabling NSX for a solution requires that you use extra vSphere nodes in addition to the standard compute nodes.

**NSX Manager**<br />
IBM Informix Virtual Appliance on Management Cluster has a 1:1 relationship with vCenter. Normal HA vSphere features are recommended. NSX Manager includes scheduled/on-demand backup capabilities and requires IP connectivity to vCenter, controller, NSX Edge resources, and ESXi hosts. NSX manager is deployed to the same subnet/VLAN as vCenter, but is not strictly required. Typical VM sizing is as follows:

|NSX Release|vCPU|Memory|OS Disk|
|---|---|---|---|
|6.2 Small|4|12 GB|60 GB|
|6.2 Default|4|16 GB|60 GB|
|6.2 Large Scale|4|24 GB|60 GB|
{: caption="Table 1. NSX Manager Typical VM sizing" caption-side="top"}

**NSX Controller Nodes**<br />
NSX Controller Nodes are deployed as virtual appliances from the NSX Manager UI. Each appliance communicates through a distinct IP address that is typically within the same subnet as the NSX manager, but is not a hard requirement. It is recommended to deploy at least three controller VMs to at least three separate physical vSphere nodes. These act as active-active-active with job delineation that is defined by the NSX Manager. IF a node fails, a "majority rules" failover happens to redistribute the workload to the remaining controllers. NSX does not natively enforce this design practice. You can use the native vSphere anti-affinity rules to avoid deploying more than one controller node on the same ESXi server. Typical VM sizing per VM is as follows:

|Controller VMs|vCPU|Reservation|Memory|OS Disk|
|---|---|---|---|---|
|3|4|2048 Mhz|4 GB|20 GB|
{: caption="Table 2. NSX Controller Typical VM sizing" caption-side="top"}

**NSX Switch**
An upgraded Virtual Distributed Switch (VDS) is deployed to all hosts to implement distributed capabilities.

**NSX Edge Services Gateway**<br />
Deployed as multi-function VM appliances as needed in the environment. For routing-only, an active cluster of up to eight gateways can be deployed. For any/all other services, it is deployed in an active-standby deployment. Communications that are external to the VM environment require IBM Cloud assigned portable IPs to include any NAT pools, VIPs, and VPN endpoints.

|Gateway Form|vCPU|Memory|Specific Usage|
|---|---|---|---|
|X-Large|6|8 GB|Suitable for L7 High Performance LB|
|Quad-Large|4|1 GB|Suitable for high performance ECMP and FW deployment|
|Large|2|1 GB|Small DC & Single Service|
|Compact|1|512 MB|Small Deployments or Single Service use or PoC|
{: caption="Table 3. NSX Edge Services" caption-side="top"}

