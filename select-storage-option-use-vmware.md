---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Storage to use with VMware Systems
You have several options when it comes to storage. They can choose private, shared, or bring their own storage solutions. Use the following information to help you decide which storage solution works best with your workload.

Table 1 contains the storage tiers and where your workload might fall.
<table border="1" cellpadding="0" cellspacing="0">
        <caption>Table 1. Storage tiers</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Tier 1</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Tier 2</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Tier 3</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Business use</strong></p>
			</td>
			<td style="width:160px;">
				<p>High performance and or high availability production applications, databases, and data</p>
			</td>
			<td style="width:160px;">
				<p>Non-mission critical test and development application, databases, and data</p>
			</td>
			<td style="width:160px;">
				<p>Non-mission critical data storage, backup, and archive</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Performance</strong></p>
			</td>
			<td style="width:160px;">
				<p>High (SSDs, SAS)</p>
			</td>
			<td style="width:160px;">
				<p>Medium (SAS, SATA)</p>
			</td>
			<td style="width:160px;">
				<p>Low (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Guaranteed IOPS</strong></p>
			</td>
			<td style="width:160px;">
				<p>Yes</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>High availability (HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>Yes</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Replication</strong></p>
			</td>
			<td style="width:160px;">
				<p>Yes</p>
			</td>
			<td style="width:160px;">
				<p>Yes</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Snapshots</strong></p>
			</td>
			<td style="width:160px;">
				<p>Yes</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
			<td style="width:160px;">
				<p>No</p>
			</td>
		</tr>
	</tbody>
</table>


## VMware Private and Shared Storage Options

You can choose from several storage options.  For private storage, you can select local disk options, VSAN, or QuantaStor. For shared storage, you can select Endurance or Performance storage. If you decide to bring your storage, there are several “private” options, including NetApp OnTap Edge, NetApp Private Storage (NPS), {{site.data.keyword.IBM}} Spectrum Accelerate, and software defined storage. Table 2 and Table 3 offer a side-by-side comparison of the options for your convenience.

## Private Storage Options

There are several options for storage for connecting to VMware in a single-tenant environment:

* Local
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## Local Storage

Order {{site.data.keyword.baremetal_short}} from the IBM Cloud customer portal with ESX and select the wanted disks [SATA, serial attached SCSI (SA SCSI), or SSD].

You can bring your own ESX license, but you need to open a ticket with Support to inform them of the change.

* Recommended workloads: Tier 3
* Performance: Limited: dependent on RAID and disk type. SSDs present a cost increase for better performance.
* Scalability: Limited to the number of drive slots in the chassis
* Protocols: Not applicable
* Cost: Low capital expenditure (CAPEX) and operating expenditure (OPEX)
* HA: Not available
* Replication: [vSphere Replication Virtual Appliance ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Reliability: Multiple single points of failure


ß
## vSAN [1]

* Recommended workloads: Tier 1
* Performance: 90K+ IOPS per host depending on host configuration
* Scalability: v5.5 virtual machine disk (VMDK) up to 2 TB; v6.0 VMDK up to 62 TB. Scale out with more nodes.
* Protocols: Proprietary
* Cost: Medium for both CAPEX and OPEX
* HA: Supported for both host and disk failures. Failure domains are supported from v6 of VMware.
* Replication: [vSphere Replication Virtual Appliance ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Replication and disaster recovery:
* Reliability: Tolerates up to three host failures with seven or more hosts. Failure domains were introduced in v6 of VMware.   

[1] vSan 6.2 new feature, stretched clusters, allows for hosts to be in different pods in the same data center (validation tests are in progress). <!-- Should this in progress mention be removed? -->

vSAN 5.5 is only available with BYOL (Bring Your Own License). It is only supported by VMware if you use an Avago LSI MegaRAID SAS 9361-8i disk controller.

vSAN 6.0 is available directly from the IBM Cloud portal with CPU license billing base.

## QuantaStor

The [OSNexus Solution Design Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} can be used to help connect VMware with QuantaStor.

* Recommended workloads: Tiers 2 and 3
* Performance: Variable based on the number of drives, RAID, and disk use (iSCSI or NFS)  
* Scalability: v3 single frame supports 128TB; no scale up or scale out.
* Protocols: iSCSI, NFS, and SMB
* Cost: High for both CAPEX and OPEX
* HA: Not available  
* Replication: Built-in replication features; no SRA available. Can use vSphere Replication Appliance as well
* Reliability: Single point of failure for the enclosure and RAID controller.


<a name="NetApp"></a>
## NetApp Data OnTap Edge

You must purchase a NetApp device from NetApp or IBM. You need to install it on a {{site.data.keyword.baremetal_short}} in your {{site.data.keyword.BluSoftlayer}} data center.

For more information about connecting VMware with NetApp, see the following links:
* [NetApp ONTAP Select ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: Build a data center on a server with NetApp fundamentals ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* Recommended workloads: Tiers 2 and 3
* Performance: Variable based on the number of drives and RAID
* Scalability: Supports 110 TB; no scale out.
* Protocols: iSCSI, NFS, and SMB
* Cost: Medium for both CAPEX and OPEX
* HA: Not available
* Replication: Supports SnapMirror; also achieved using [vRealize Automation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.vmware.com/products/vrealize-automation){: new_window} (vRA).
* Reliability: Single point of failure for the enclosure and RAID controller.

<a name="NPS"></a>
## NetApp Private Storage

You must purchase a NetApp device from NetApp or IBM. You need to install it in one of the colocation sites near your IBM Cloud data center and connect it by using Direct Link Colocation or Direct Link Cloud.

For more information about connectting to VMware with NetApp, see the following links:
* [NetApp Private Storage for IBM Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Solution brief: NetApp Private Storage for IBM Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* Recommended workloads: Tier 1
* Performance: Dependent on NetApp model
* Scalability: Supports addition of drives and frames for increased capacity and IOPS
* Protocols: iSCSI, NFS, and SMB
* Cost: High for both CAPEX and OPEX
* HA: Dual heads and controllers
* Replication: Supports SnapVault and SnapMirror; also achieved using [vRealize Automation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.vmware.com/products/vrealize-automation).
* Reliability: High redundancy and MPIO support

<a name="IBM"></a>
## IBM Spectrum Accelerate

The IBM Spectrum Accelerate private storage option is not available on the IBM Cloud customer portal. <!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* Recommended workloads: Tier 1
* Performance: Dependent upon number of disks, SSD (optional), and amount of memory that is given to each “node” VM.
* Scalability: Scales ~8 - 325 TB usable
  * Minimum capacity: 3 VMs x 6 drives
  * Maximum capacity: 15 VMs x 12 drives
  * Scales up to 144 virtual arrays and more than 40 PB usable through IBM Hyper-Scale Manager
  * Non-disruptive capacity expansion by adding more nodes
  * 1 x 500 or 800 GB SSD per node supported
* Protocols: iSCSI only
* Cost: Dependent upon pricing model and physical machines deployed for nodes. High CAPEX; medium to low OPEX depending on licensing.
  * Priced per binary (TiB) of usable capacity
  * Not tied to any specific hardware configuration. Example: 200 TiB license could be deployed various ways – one 200 TiB instance, two 100 TiB instances, or four 50 TiB instances
  * Offered two ways: perpetual license [includes one year of subscription and service (S&S)] and monthly license (includes S&S)
* HA: Clustered solution
* Replication: Achieved by using [vRealize Automation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.vmware.com/products/vrealize-automation){: new_window}
 or SRA, which can be used to replicate from physical IBM XIV with VMware’s Site Recovery Manager (SRM)
  * [vSphere Replication ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [VMware vCenter Site Recovery Manager version 5.x guidelines for IBM XIV Gen3 Storage System ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* Reliability: High redundancy and MPIO support. Any available node can manage the cluster. The following capabilities are not supported by IBM Spectrum Accelerate at this time over hardware-based IBM XIV:
  * Three-site mirroring
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG v6
  * 6 TB disk drives
  * Storage Management Initiative Specifications (SMI-S) 1.6
  * Data at rest encryption
  * vStorage for API Array Integration (VAAI) if it is aligned with Virtual Volumes (VVol)ß
  * vCenter Operations Manager (VCop)
  * For more information about IBM XIV Storage System, see [Platform and application integration for IBM XIV Storage System ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}

## Shared Storage Options

There are two storage options that you can use to connect to VMware in a multi-tenant environment: Block Storage and File Storage.

### Block and File Storage

Order the {{site.data.keyword.baremetal_short}} from the IBM Cloud customer portal with ESX.

In VMware, three <!--**Authorize** (**Block** or **File**) **Storage SoftLayer** --> predefined values are provided on the **Host Device Details Storage** tab – Username, Password (for CHAP authentication), and Host IQN.

For more information about provision block storage, see [Provisioning and managing block storage](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

For more information about provision file storage, see [Provisioning and Managing IBM File Storage for IBM Cloud](/docs/infrastructure/FileStorage/provisioning-file-storage.html).

* Recommended workloads:     Tiers 1, 2, and 3
* Two ways to provision performance:
    1. Endurance IOPS tiers: Available in 0.25, 2, 4 or 104 IOPS per GB
    2. Performance Allocated IOPS: Specify IOPS independent of capacity. Recommended for workloads with well defined performance requirements.
    * Predictable storage performance parameters
    * Multiple volumes can be striped together to achieve higher IOPS and more throughput
* Latency <10 ms UP to 48,000 IOPS
* Scalability: Order from 20 GB to 12 TB. You cannot resize the volume after it is ordered.
* Protocols: iSCSI and NFS
* Cost: High for both CAPEX (10x for SAN of same size) and OPEX
* HA: Dual heads and controllers
* Replication: Snapshot and Replication provided over the IBM Cloud Private Network; also achieved using [vRealize Automation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.vmware.com/products/vrealize-automation){: new_window}, but no SRA.
* Reliability: High redundancy; iSCSI uses an MPIO connection; NFS-based storage is routed over TCP/IP connections. Snapshot and Replication enabled.

Table 2 provides the pros and cons of private storage in a single-tenant environment.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Table 2. Pros and cons of VMware private storage options</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; Private storage (single tenant)</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>Key factors/ storage option</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>Local</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>Virtual SAN</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:99px;">
				<p>QuantaStor</p>
			</td>
			<td bgcolor="#C6D9F1" colspan="2" style="width:159px;">
				<p align="center">NetApp</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p>IBM Spectrum Accelerate</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>OnTap Edge</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>NPS</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p align="center">&nbsp;</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Type</strong></p>
			</td>
			<td style="width:87px;">
				<p>Local</p>
			</td>
			<td style="width:95px;">
				<p>SDS</p>
			</td>
			<td style="width:99px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>Monolithic</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Performance</strong></p>
			</td>
			<td style="width:87px;">
				<p>Based on SSD /SA-SCSI specs; further RAID 5/10 can be used for read /write gains.</p>
			</td>
			<td style="width:95px;">
				<p>90K+ IOPS per host depending on host configuration. 100 VMs per host, 32 hosts per cluster, 3,200 VMs per cluster, only 2,048 protected (v5.5)</p>
				<p>Up to 20K IOPS, 200 VMs per host, 64 hosts per cluster, and 6,000 protected VMs per cluster (v6.0).</p>
			</td>
			<td style="width:99px;">
				<p>Based on types and number of disks selected, as well as RAID configurations and use of iSCSI or NFS.</p>
			</td>
			<td style="width:80px;">
				<p>Based on types and number of disks selected, as well as RAID configure-actions.</p>
			</td>
			<td style="width:80px;">
				<p>Depends on model.</p>
			</td>
			<td style="width:96px;">
				<p>Based on types and number of disks selected, as well as RAID configurations and optional use of SSD disk per hypervisor node.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Scalability</strong></p>
			</td>
			<td style="width:87px;">
				<p>Limited growth in size and in disk I/O throughput.</p>
			</td>
			<td style="width:95px;">
				<p>Virtual machine disk (VMDK) up to 2TB with v5.5, and up to 62TB with v6.0.</p>
				<p>Scale out with more nodes.</p>
			</td>
			<td style="width:99px;">
				<p>Single QS up to 128TB (3.x). No scaling up or out.</p>
			</td>
			<td style="width:80px;">
				<p>Up to 10TB; no scaling out.</p>
			</td>
			<td style="width:80px;">
				<p>Yes, add disk shelves for capacity and IOPS.</p>
			</td>
			<td style="width:96px;">
				<p>Scales from ~8 to 325TB usable space.</p>
				<p>Min capacity is 3 VMs x 6 drives.</p>
				<p>Max capacity is 15 VMs x 12 drives.</p>
				<p>Scales up to 144 virtual arrays and more than 40 PB usable via IBM Hyper-Scale Manager.</p>
				<p>Non-disruptive capacity expansion by adding more nodes.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocols</strong></p>
			</td>
			<td style="width:87px;">
				<p>NA</p>
			</td>
			<td style="width:95px;">
				<p>Proprietary</p>
			</td>
			<td style="width:99px;">
				<p>iSCSI/NFS/SMB</p>
			</td>
			<td colspan="2" style="width:159px;">
				<p align="center">iSCSI/NFS/SMB</p>
			</td>
			<td style="width:96px;">
				<p>iSCSI</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Use cases</strong></p>
			</td>
			<td style="width:87px;">
				<p>Tier 2 and 3 workloads</p>
			</td>
			<td style="width:95px;">
				<p>Tier 1 workloads</p>
			</td>
			<td style="width:99px;">
				<p>Tier 2 and 3 workloads</p>
			</td>
			<td style="width:80px;">
				<p>Tier 2 and 3 workloads</p>
			</td>
			<td style="width:80px;">
				<p>Tier 1 workloads</p>
			</td>
			<td style="width:96px;">
				<p>Tier 1 workloads</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>High availability (HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>Available with RAID</p>
			</td>
			<td style="width:95px;">
				<p>Yes; host and disk failures; failure domains (v6.0)</p>
			</td>
			<td style="width:99px;">
				<p>Not available in IBM Cloud.</p>
			</td>
			<td style="width:80px;">
				<p>NA</p>
			</td>
			<td style="width:80px;">
				<p>Yes; dual heads and controllers.</p>
			</td>
			<td style="width:96px;">
				<p>Yes; clustered solution.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Configurability</strong></p>
			</td>
			<td style="width:87px;">
				<p>Number and type of disks; RAID levels</p>
			</td>
			<td style="width:95px;">
				<p>Specific controllers required.</p>
			</td>
			<td style="width:99px;">
				<p>CPU, memory, cache, number and type of disks, and RAID levels.</p>
			</td>
			<td style="width:80px;">
				<p>CPU, memory, cache, number and type of disks, and RAID levels.</p>
			</td>
			<td style="width:80px;">
				<p>TBD</p>
			</td>
			<td style="width:96px;">
				<p>CPU, memory, cache, number and type of disks, SSD, caching, iSCSI port configuration. Multi-tenancy QOS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Disaster recovery and replication</strong></p>
			</td>
			<td style="width:87px;">
				<p>Use vRA to replicate; no SRAs.</p>
			</td>
			<td style="width:95px;">
				<p>Use vRA to replicate.</p>
			</td>
			<td style="width:99px;">
				<p>Built in replication; no SRAs available.</p>
			</td>
			<td style="width:80px;">
				<p>Can use vRA to replicate, SnapMirror.</p>
			</td>
			<td style="width:80px;">
				<p>Can use vRA to replicate, SnapMirror, SnapVault.</p>
			</td>
			<td style="width:96px;">
				<p>vRA or SRA supported; replication between SDS and or Physical XIV devices.</p>
				<p>Snapshots supported; application recovery via IBM FlashCopy Manager.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Reliability</strong></p>
			</td>
			<td style="width:87px;">
				<p>Single point of failure without HA.</p>
			</td>
			<td style="width:95px;">
				<p>Tolerates up to three host failures with seven plus hosts.</p>
				<p>Failure domains are introduced in v6.0.</p>
			</td>
			<td style="width:99px;">
				<p>Single point of failure (enclosure and RAID controller) and no HA.</p>
			</td>
			<td style="width:80px;">
				<p>Single point of failure (enclosure and RAID controller) and no HA.</p>
			</td>
			<td style="width:80px;">
				<p>Highly- redundant multipath I/O (MPIO) connection.</p>
			</td>
			<td style="width:96px;">
				<p>Highly-redundant iSCSI MPIO connections: any node can manage the cluster.</p>
			</td>
		</tr>
	</tbody>
</table>

Table 2 documentation links:
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge: Not available on the customer portal – bring your own solution.
  * [Data ONTAP Installation and Administration Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP Express Setup Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate: Not available on the customer portal – bring your own solution.
  * [Working with an IBM Spectrum Accelerate system ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

Table 3 provides the pros and cons of shared storage in a multi-tenant environment.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Table 3. Pros and cons of VMware shared storage options</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>VMware Shared storage (multi-tenant)</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Key factors/ storage options</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">Block and File Endurance</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">Block and File Performance</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Type</strong></p>
			</td>
			<td style="width:266px;">
				<p>SDS</p>
			</td>
			<td style="width:271px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Performance</strong></p>
			</td>
			<td style="width:266px;">
				<p>Available in 0.25, 2, 4 or 104 IOPS per GB.</p>
				<p>Predictable storage performance parameters.</p>
				<p>Multiple volumes may be striped together to achieve higher IOPS and more throughput.</p>
			</td>
			<td style="width:271px;">
				<p>Client provisions desired level of performance based on workload needs or price point.</p>
				<p>&nbsp;</p>
				<p>Predictable storage performance parameters.</p>
				<p>Multiple volumes may be striped together to achieve higher IOPS and more throughput.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Scalability</strong></p>
			</td>
			<td style="width:266px;">
				<p>Volume sizes range from 20 GB to 12 TB. Cannot be resized once ordered.</p>
			</td>
			<td style="width:271px;">
				<p>Volume sizes range from 20 GB to 12 TB. Cannot be resized once ordered.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocols</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI and NFS.</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI and NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Host Connections</strong></p>
			</td>
			<td style="width:266px;">
				<p>Maximum of eight for iSCSI and64 for NFS.</p>
			</td>
			<td style="width:271px;">
				<p>Maximum of eight for iSCSI and 64 for NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Use cases</strong></p>
			</td>
			<td style="width:266px;">
				<p>Tier 1, 2, and 3 workloads:</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 0.25 IOPS per GB: Low I/O intensity. Example applications include storing mailboxes or department-level file shares.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 2 IOPS per GB: General purposes. Example applications include hosting small databases backing web applications or virtual machine disk images for a hypervisor.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 4 IOPS per GB: High I/O intensity. Example applications include transactional and other performance-sensitive databases.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 10 IOPS per GB: High I/O intensity. Example applications include analytics.</p>
			</td>
			<td style="width:271px;">
				<p>Tier 1, 2, and 3 workloads:</p>
				<p>MPIO iSCSI-based storage ideally suited for I/O intensive applications such as relational databases that require predictable levels of performance. The storage volumes come in sizes from 20 GB to 12 TB with user selectable IOPS ranging from 100 to 48,000 IOPS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>HA</strong></p>
			</td>
			<td style="width:266px;">
				<p>Yes, dual heads and controllers.</p>
			</td>
			<td style="width:271px;">
				<p>Yes, dual heads and controllers.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Configurability</strong></p>
			</td>
			<td style="width:266px;">
				<p>Size and IOPS only.</p>
			</td>
			<td style="width:271px;">
				<p>Size and IOPS only.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Disaster recovery and replication</strong></p>
			</td>
			<td style="width:266px;">
				<p>Snapshot and Replication provided, which is done over the IBM Cloud Private Network. Can use vRA to replicate at the VM level; no SRA.</p>
			</td>
			<td style="width:271px;">
				<p>Snapshot and Replication provided, which is done over the IBM Cloud Private Network. Can use vRA to replicate at the VM level; no SRA.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Reliability</strong></p>
			</td>
			<td style="width:266px;">
				<p>Highly redundant, MPIO connection, NFS-based file storage routed TCP/IP connections. Snapshots and Replication enabled.</p>
			</td>
			<td style="width:271px;">
				<p>Highly redundant, MPIO connection, NFS-based file storage routed TCP/IP connections.</p>
			</td>
		</tr>
	</tbody>
</table>

Table 3 documentation links:
* [Block storage](/docs/infrastructure/BlockStorage/index.html)
* [File storage](/docs/infrastructure/FileStorage/index.html)
