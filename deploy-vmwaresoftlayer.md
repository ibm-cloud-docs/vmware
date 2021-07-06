---

copyright:
  years: 2017, 2021
lastupdated: "2021-05-26"

keywords:  VMware administrators, vSphere workloads, VMware vSphere environments, cookbooks, VMware deployments, vSphere administrators

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:external: target="_blank" .external} 
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:note: .note}

# Using cookbooks for VMware deployments
{: #using-vmware-cookbooks}

VMware&reg; administrators can quickly realize cost-effective hybrid cloud characteristics by deploying into the {{site.data.keyword.BluSoftlayer_full}} enterprise-grade global cloud. vSphere workloads and catalogs can be provisioned onto VMware&reg; vSphere environments within the {{site.data.keyword.cloud_notm}} data centers without modifying VMware&reg; VMs or guests. These deployments are made possible by using a common vSphere hypervisor and management and orchestration platform. vSphere implementations also can use other components of the VMware&reg; vCloud Suite – vCloud Automation Center, vCenter Operations Management Suite, vSAN, vCloud Network & Security, Site Recovery Manager, vCenter Orchestrator, and NSX.

The core objective of the VMware&reg; cookbook series is to assist vSphere administrators with the deployment of VMware&reg; vSphere environments within an IBM Cloud infrastructure. The cookbooks are not intended to train you how to administer vSphere. For more information about administering vSphere, see [VMware&reg; Education](https://www.vmware.com/learning.html){: external}. 

{{site.data.keyword.cloud_notm}} has several specific capabilities that give VMware&reg; administrators the flexibility to consume bare metal instances and network, storage, and backup and recovery constructs in a self-service manner. You can then use these constructs to deploy fully functional vSphere implementations, which can be built to extend or replace on-premises vSphere implementations (VMware@Home).

The following guides are intended for experienced vSphere administrators. Some topics that are covered, consider that the reader has basic deployment skills to install and configure vSphere and vCenter.
{: note}

* [Build a Single Site VMware&reg; Environment](/docs/virtualization?topic=virtualization-advanced-single-site-vmware-reference-architecture) You, as the vSphere administrator, are walked through the steps of building your environment, including the use of either Endurance or Performance Block Storage or QuantaStor.
* [vSphere Migration](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.update_manager.doc/GUID-F7191592-048B-40C7-A610-CFEE6A790AB0.html){:external} Scenarios are presented to help you migrate workloads into VMware&reg; after your vSphere implementation is deployed in an IBM Cloud data center.<!--docs.vmware.com/en/VMware-vSphere/6.0/vsphere-vcenter-server-602-migration-guide.pdf-->
* [Use NSX®](https://developer.ibm.com/recipes/tutorials/?s=nsx){:external} You can use VMware&reg; NSX to provide software-defining networking (SDN) constructs to VMware&reg; IBM Cloud deployments.
* [VMware&reg; backup](https://www.vmware.com/pdf/vi3_30_20_vm_backup.pdf){: external} describes alternative approaches to backing up, recovering, and archiving VMware-based workloads that are running in a VMware deployment.
* [VMware&reg; disaster recovery guide](https://docs.vmware.com/en/Site-Recovery-Manager/index.html){:external} Documentation for VMware&reg; Site Recovery Manager.
* [Vormetric Encryption of VMware&reg;](http://go.thalesesecurity.com/rs/480-LWA-970/images/VMware-Encryption-and-KMIP-Integration-with-Vormetric-Data-Security-Manager-Integration-guide.pdf){:external} <!--Use cases illustrate how Vormetric protects VMware workloads by encrypting VM data.--> Vormetric protects VMware&reg; workloads by encrypting VM data.
* [Deploy a trusted cloud solution with IBM, VMware&reg;, and HyTrust](https://www.hytrust.com/solutions/ibm-cloud-secure-virtualization/){:external} You can integrate the various architectural elements to create a chain of trust from hardware up through the hypervisor and management applications.

