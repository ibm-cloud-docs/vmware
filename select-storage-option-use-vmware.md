---

copyright:
  years: 2017, 2021
lastupdated: "2021-07-07"

keywords: NetApp OnTap Select, High performance, vmware storage, QuantaStor, IBM Spectrum Accelerate, shared storage, private storage

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Storage to use with VMware Systems
{: #vmware-storage}

You have several options when it comes to storage and VMware&reg;. You can choose private, shared, or bring your own storage solutions. Use the following information to help you decide which storage solution works best with your workload.

See the following table for storage tiers and where your workload might fall.

| Tier 1 | Tier 2 | Tier 3|
|--------|--------|-------|
| Business use | High performance and or high availability production applications, databases, and data| Non-mission critical test and development application, databases, and data | Non-mission critical data storage, backup, and archive |
| Performance | High (SSDs, SAS) | Medium (SAS, SATA) | Low (SATA)|
|Guaranteed IOPS|Yes| No | No|
|High availability (HA)|Yes|No|No|
|Replication|Yes|Yes|No|
|Snapshots|Yes|No|No|

<caption>Table 1. Storage tiers</caption>


## VMware Private and Shared Storage Options
{: #vmware-private-shared-storage}

For private storage, you can select local disk options, VSAN, or QuantaStor. For shared storage, you can select Endurance or Performance storage. If you decide to bring your storage, several “private” options are available, including NetApp OnTap Select, NetApp Private Storage (NPS), {{site.data.keyword.IBM}} Spectrum Accelerate, and software defined storage. Table 2 and Table 3 offer a side-by-side comparison of the options for your convenience.

## Private Storage Options
{: 3vmware-private-storage-options}

You have several options for storage for connecting to VMware in a single-tenant environment:

* Local
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
### Local Storage

Order {{site.data.keyword.baremetal_short}} from the {{site.data.keyword.cloud_notm}} catalog with ESX and select the wanted disks [SATA, serial attached SCSI (SA SCSI), or SSD].

You can bring your own ESX license, but you need to open a ticket with Support to inform them of the change.

* Recommended workloads - Tier 3
* Performance - Limited dependent on RAID and disk type. SSDs present a cost increase for better performance.
* Scalability - Limited to the number of drive slots in the chassis
* Protocols - Not applicable
* Cost: Low capital expenditure (CAPEX) and operating expenditure (OPEX)
* HA - Not available
* Replication - [vSphere Replication Virtual Appliance](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: external}
* Reliability - Multiple single points of failure

### vSAN [1]

* Recommended workloads - Tier 1
* Performance - 90 K+ IOPS per host (depends on host configuration)
* Scalability - v5.5 virtual machine disk (VMDK) up to 2 TB; v6.0 VMDK up to 62 TB. Scale out with more nodes.
* Protocols - Proprietary
* Cost - Medium for both CAPEX and OPEX
* HA - Supported for both host and disk failures. Failure domains are supported from v6 of VMware.
* Replication - [vSphere Replication Virtual Appliance](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: external}
* Replication and disaster recovery
* Reliability - Tolerates up to three host failures with seven or more hosts. Failure domains were introduced in v6 of VMware.   

<!--[1] vSan 6.2 new feature, stretched clusters, allows for hosts to be in different pods in the same data center (validation tests are in progress).-->

vSAN 5.5 is available only with BYOL (Bring Your Own License). vSAN 5.5 supported by VMware only if you use an Avago LSI MegaRAID SAS 9361-8i disk controller.

vSAN 6.0 is available directly from the {{site.data.keyword.cloud_notm}} catalog with CPU license billing base.

### QuantaStor

The [OSNexus Solution Design Guide](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: external} can be used to help connect VMware with QuantaStor.

* Recommended workloads - Tiers 2 and 3
* Performance - Variable based on the number of drives, RAID, and disk use (iSCSI or NFS)  
* Scalability - v3 single frame supports 128 TB with no scale up or scale out.
* Protocols - iSCSI, NFS, and SMB
* Cost - High for both CAPEX and OPEX
* HA - Not available  
* Replication - Built-in replication features, SRA not available. Can use vSphere Replication Appliance too
* Reliability - Single point of failure for the enclosure and RAID controller.


<a name="NetApp"></a>
### NetApp Data OnTap Select

NetApp® ONTAP® Select on {{site.data.keyword.cloud}}, a software-defined storage virtual appliance, extends existing data management capabilities by implementing NetApp ONTAP software as a service on {{site.data.keyword.cloud}} dedicated bare metal servers. You can provision storage resources with agility and flexibility while your data is protected by using NetApp’s advanced data management functions, such as the fast and efficient NetApp Snapshot® copies, FlexClone® copies, and SnapMirror® replication. NetApp ONTAP Select accelerates application DevOps and reduces the complexity and increased processor usage that are associated with physical storage systems.

NetApp ONTAP Select on {{site.data.keyword.cloud}} is offered in both high performance (all SSD) and high capacity (all SATA) configurations, which can meet the range of use cases you demand today. You can use the tools that are provided by NetApp ONTAP Select to address your hybrid cloud needs, such as addressing disaster recovery scenarios, providing file services, and managing rapid transactional data workloads.

NetApp ONTAP Select on {{site.data.keyword.cloud}} helps to improve productivity and efficiency, reduce IT costs, and gain agility by offloading IT resources and management complexity from the cloud. The offering can accelerate hybrid cloud adoption by harnessing the NetApp integrated ONTAP capabilities with VMware running on IBM Cloud bare metal servers. The offering enables easier, security-rich, and near-seamless extension of existing workloads from on-premises data centers to IBM Cloud data centers worldwide.

* Recommended workloads - Tiers 1, 2 and 3
* Performance - Variable based on the number of drives, media type, and RAID topology
* Scalability - Supports up to 400 TB per node (RAW and Active Licensed Capacity)
* HA - Supports 2, 4 and 8 node HA configurations or single node if no HA is required
* Protocols - iSCSI, NFS v3 and v4, and SMB/CIFS
* Protected - Integrated NetApp® Snapshot™ copies, local and remote backup, disaster recovery, and volume encryption
* Efficient - Thin provisioning, cloning, deduplication, and compression
* Cost - Available in CAPEX and OPEX models and is charged on a $GB Basis
* Replication - Supports SnapMirror; also achieved by using vRealize Automation External link icon (vRA).
* Resiliency 
   - in a non-HA Configuration single point of failure include enclosure hardware
   - in an HA configuration, no single point of failure

For more information about how to request ONTAP Select, see [NetApp ONTAP Select](/docs/vmwaresolutions?topic=vmwaresolutions-netapp).

<a name="NPS"></a>
### NetApp Private Storage

You must purchase a NetApp device from NetApp or {{site.data.keyword.cloud}}. You need to install it in one of the colocation sites that are near your {{site.data.keyword.cloud}} data center and connect it by using Direct Link Colocation or Direct Link Cloud.

For more information about connecting to VMware with NetApp, see the following links:
* [NetApp Private Storage for {{site.data.keyword.cloud}}](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: external}
* [Solution brief: NetApp Private Storage for {{site.data.keyword.cloud}}](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: external}


* Recommended workloads - Tier 1
* Performance - Dependent on NetApp model
* Scalability - Supports extra of drives and frames for increased capacity and IOPS
* Protocols: - iSCSI, NFS, and SMB
* Cost - High for both CAPEX and OPEX
* HA - Dual heads and controllers
* Replication - Supports SnapVault and SnapMirror, which is achieved by using [vRealize Automation](https://www.vmware.com/products/vrealize-automation.html){: external}.
* Reliability - High redundancy and MPIO support

<a name="IBM"></a>
### IBM Spectrum Accelerate

The IBM Spectrum Accelerate private storage option is not available on the {{site.data.keyword.cloud_notm}} catalog.

* Recommended workloads: Tier 1
* Performance: Dependent upon number of disks, SSD (optional), and amount of memory that is given to each “node” VM.
* Scalability: Scales ~8 - 325 TB usable
   * Minimum capacity: 3 VMs x 6 drives
   * Maximum capacity: 15 VMs x 12 drives
   * Scales up to 144 virtual arrays and more than 40 PB usable through IBM Hyper-Scale Manager
   * Non-disruptive capacity expansion by adding more nodes
   * 1 x 500 or 800 GB SSD per node supported
* Protocols: iSCSI only
* Cost: Dependent upon pricing model and physical machines that are deployed for nodes. High CAPEX; medium to low OPEX depending on licensing.
   * Priced per binary (TiB) of usable capacity
   * Not tied to any specific hardware configuration. Example: 200 TiB license can be deployed various ways – one 200 TiB instance, two 100 TiB instances, or four 50 TiB instances
   * Offered two ways: perpetual license [includes one year of subscription and service (S&S)] and monthly license (includes S&S)
* HA: Clustered solution
* Replication: Achieved by using [vRealize Automation](https://www.vmware.com/products/vrealize-automation){: external}
 or SRA, which can be used to replicate from physical IBM XIV with VMware’s Site Recovery Manager (SRM)
   * [vSphere Replication](https://www.vmware.com/products/vsphere/replication.html){: external}
   <!--* [VMware vCenter Site Recovery Manager version 5.x guidelines for IBM XIV Gen3 Storage System](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3)-->
* Reliability: High redundancy and MPIO support. Any available node can manage the cluster. The following capabilities are not supported by IBM Spectrum Accelerate over hardware-based IBM XIV:
   * Three-site mirroring
   * IBM Hyper-Scale Mobility (iSCSI)
   * USG v6
   * 6 TB disk drives
   * Storage Management Initiative Specifications (SMI-S) 1.6
   * Data at rest encryption
   * vStorage for API Array Integration (VAAI) if it is aligned with Virtual Volumes (VVol)ß
   * vCenter Operations Manager (VCop)
   * For more information about IBM XIV Storage System, see [Platform and application integration for IBM XIV Storage System](https://www.ibm.com/support/knowledgecenter/STJTAG/css/css_kcwelcomepage_xiv.html){: external}

See the following table to see pros and cons of private storage in a single-tenant environment.

|Key Factors or storage options| Local | Virtual SAN | QuantStor|NetApp (_OnTap Edge_)|NetApp (_NPS_)|IBM Spectrum Accelerate|
|-|-|-|-|-|-|-|
| **Type** |Local |SDS |SDS| SDS |Monolithic|SDS|
| **Performance** | Based on SSD/SA-SCSI specs, further RAID 5 and 10 can be used for read and write gains. | 90 K+ IOPS per host that depends on host configuration. 100 VMs per host, 32 hosts per cluster, 3,200 VMs per cluster, only 2,048 protected (v5.5). Up to 20 K IOPS, 200 VMs per host, 64 hosts per cluster, and 6,000 protected VMs per cluster (v6.0).| Based on types and number of disks that are selected, and RAID configurations and use of iSCSI or NFS. | Based on types and number of disks that are selected and RAID configure-actions.| Depends on model. |Based on types and number of disks that are selected, RAID configurations, and optional use of SSD disk per hypervisor node.|
|**Scalability**|Limited growth in size and in disk I/O throughput. | Virtual machine disk (VMDK) up to 2 TB with v5.5, and up to 62 TB with v6.0.|Single QS up to 128 TB (3.x). No scaling up or out.|Up to 10 TB; no scaling out.|Yes, add disk shelves for capacity and IOPS. | Scales from ~8 - 325 TB usable space. Min capacity is 3 VMs x 6 drives. Max capacity is 15 VMs x 12 drives. Scales up to 144 virtual arrays and more than 40 PB usable through IBM Hyper-Scale Manager. Non-disruptive capacity expansion by adding more nodes.|
|**Protocols**|N/A|Proprietary|iSCSI/NFS/SMB|iSCSI/NFS/SMB|iSCSI/NFS/SMB|iSCSI|
|**Use cases**|Tier 2 and 3 workloads|Tier 1 workloads|Tier 2 and 3 workloads|Tier 2 and 3 workloads|Tier 1 workloads|Tier 1 workloads|
|**High availability (HA)**|Available with RAID|Yes; host and disk failures; failure domains (v6.0)|N/A|N/A|Yes; dual heads and controllers.|Yes; clustered solution.|
|**Configurability (HA)**|Number and type of disks; RAID levels|Specific controllers required.|CPU, memory, cache, number and type of disks, and RAID levels.|CPU, memory, cache, number and type of disks, and RAID levels.|TBD|CPU, memory, cache, number and type of disks, SSD, caching, iSCSI port configuration. Multi-tenancy QOS.|
|**Disaster recovery and replication**|Use vRA to replicate, no SRAs.|Use vRA to replicate.|Built-in replication; no SRAs available.|Can use vRA to replicate, SnapMirror.|Can use vRA to replicate, SnapMirror, SnapVault.|vRA or SRA supported, replication between SDS and or Physical XIV devices. Snapshots supported; application recovery through IBM FlashCopy Manager.|
|**Reliability**|Single point of failure without HA.|Tolerates up to three host failures with seven plus hosts. Failure domains are introduced in v6.0.|Single point of failure (enclosure and RAID controller) and no HA.|Single point of failure (enclosure and RAID controller) and no HA.|Highly redundant multipath I/O (MPIO) connection.|Highly redundant iSCSI MPIO connections: any node can manage the cluster.|

<caption>Table 2. Pros and cons of VMware private storage options</caption>

Table 2 documentation links:
* NetApp OnTap Edge: Not available on the {{site.data.keyword.cloud_notm}} catalog – bring your own solution.
   * [Data ONTAP Installation and Administration Guide](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: external}
   * [Data ONTAP Express Setup Guide](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: external}
* [NetApp Private Storage for IBM Cloud](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: external}
* Spectrum Accelerate: Not available on the {{site.data.keyword.cloud_notm}} catalog – bring your own solution.
   * [Working with an IBM Spectrum Accelerate system](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: external}


## Shared Storage Options
{: #vmware-shared-storage-options}

{{site.data.keyword.cloud}} offers great {{site.data.keyword.filestorage_short}} options that you can use to connect to VMware in a multi-tenant environment.

### {{site.data.keyword.filestorage_short}}

You can order the {{site.data.keyword.baremetal_short}} from the {{site.data.keyword.cloud_notm}} catalog with ESX. In the {{site.data.keyword.cloud_notm}} catalog, you can also provision {{site.data.keyword.filestorage_full}} in the same availability zone as your host. For more information about provisioning file storage, see [Ordering and Managing IBM File Storage for IBM Cloud](/docs/FileStorage?topic=FileStorage-orderingConsole#orderingConsole).

In VMware, three predefined values are provided on **Host Device Details Storage** – Username, Password (for CHAP authentication), and Host IQN.
{: note}

See the following table for pros and cons of shared storage in a multi-tenant environment.

|Key Factors/storage options| File Storage - Endurance and Performance options | 
|-|-|
| **Type** |SDS |
| **Performance** |Predictable storage performance parameters. <br>Endurance option: <br><ol>Available in 0.25, 2, 4 or 10 IOPS per GB.<br>Performance option: Client provisions wanted level of performance based on workload needs or price point.<br></ol>Multiple volumes can be striped together to achieve higher IOPS and more throughput. |
|**Scalability**|Volume sizes range 20 - 12 TB.<br>File Share Capacity can be expanded to 12 TB after initial provisioning in GB increments. | 
|**Protocols**|NFS|
|**Host connections**|Maximum of 64 for NFS.|
|**Use cases**|Tier 1, 2, and 3 workloads:<br><ol>0.25 IOPS per GB: Low I/O intensity. Example applications include storing mailboxes or department-level file shares.<br></ol>2 IOPS per GB: General purposes. Example applications include hosting small databases that are backing web applications or virtual machine disk images for a hypervisor.<br>4 IOPS per GB: High I/O intensity. Example applications include transactional and other performance-sensitive databases.<br>10 IOPS per GB: High I/O intensity. Example applications include analytics.|
|**HA**|Yes, dual heads and controllers.|
|**Configurability**|Size and IOPS only.|
|**Disaster recovery and replication** | Snapshot and Replication provided over the {{site.data.keyword.cloud}} Private Network, also achieved by using [vRealize Automation](https://www.vmware.com/products/vrealize-automation){: external}, but no SRA.|
|**Reliability**|Highly redundant, MPIO connection, NFS-based file storage routed TCP/IP connections. Snapshots and Replication enabled.|
|**Latency**|<10 ms|
|**Cost**|High for both CAPEX (10x for SAN of the same size) and OPEX|

<caption> Table 3. Pros and cons of VMware shared storage options</caption>

Table 3 documentation links:
* [File storage](/docs/FileStorage?topic=FileStorage-getting-started)
* [Architecture Guide for IBM File Storage for IBM Cloud with VMware](/docs/FileStorage?topic=FileStorage-architectureguide)
