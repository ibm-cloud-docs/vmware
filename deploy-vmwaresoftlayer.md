---

copyright:
  years: 1994, 2019
lastupdated: "2019-12-12"

keywords:  VMware administrators, vSphere workloads, VMware vSphere environments, cookbooks, VMware deployments, vSphere administrators

subcollection: vmware

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Using cookbooks for VMware deployments
{: #using-vmware-cookbooks}

VMware administrators can quickly realize cost-effective hybrid cloud characteristics by deploying into the {{site.data.keyword.BluSoftlayer_full}} enterprise-grade global cloud. vSphere workloads and catalogs can be provisioned onto VMware vSphere environments within the {{site.data.keyword.cloud_notm}} data centers without modifying VMware VMs or guests. These deployments are made possible by using a common vSphere hypervisor and management or orchestration platform. vSphere implementations also can use other components of the VMware vCloud Suite – vCloud Automation Center, vCenter Operations Management Suite, vSAN, vCloud Network & Security, Site Recovery Manager, vCenter Orchestrator, and NSX.

The core objective of the VMware cookbook series is to assist vSphere administrators with the deployment of VMware vSphere environments within an IBM Cloud infrastructure. The cookbooks are not intended to train you how to administer vSphere. For more information about administering vSphere, see [VMware Education ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}.

{{site.data.keyword.cloud_notm}} has several specific capabilities that give VMware administrators the flexibility to consume bare metal instances and network, storage, and backup and recovery constructs in a self-service manner. You can then use these constructs to deploy fully functional vSphere implementations, which can be built to extend or replace on-premises vSphere implementations (VMware@Home).

The following cookbooks are available to administrators:


* [Build a Single Site VMware Environment](/docs/infrastructure/virtualization?topic=Virtualization-advanced-single-site-vmware-reference-architecture): You, as the vSphere administrator, are walked through the steps of building your environment, including the use of either Endurance or Performance Block Storage or QuantaStor.
* [vSphere Migration](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.update_manager.doc/GUID-F7191592-048B-40C7-A610-CFEE6A790AB0.html){: external} Scenarios are presented to help you migrate workloads into VMware after your vSphere implementation is deployed in an IBM Cloud data center.
* [Leverage NSX®](https://developer.ibm.com/recipes/tutorials/?s=nsx){: external} You can use VMware NSX to provide software-defining networking (SDN) constructs to VMware IBM Cloud deployments.
* [Catalogic ECX](https://developer.ibm.com/recipes/tutorials/steps-to-attach-dedicated-storage-to-existing-ic4v-deployments-on-ibm-cloud/#r_overview){: external} This recipe explains how IBM Cloud (IC4V) users can attach their NetApp ONTAP Select (OTS) to their existing IC4V deployments. Providing step-by-step instructions to create NFS volume and mount it on Linux virtual machines.
* [VMware Back Up](https://www.vmware.com/pdf/vi3_30_20_vm_backup.pdf){: external} This guide describes alternative approaches to backing up, recovering, and archiving VMware-based workloads (VMs) that are running in a VMware deployment.
* [VMware Disaster Recovery Guide](https://www.vmware.com/support/pubs/srm_pubs.html){: external} Documentation for VMware Site Recovery Manager.
* [Vormetric Encryption of VMware](http://go.thalesesecurity.com/rs/480-LWA-970/images/VMware-Encryption-and-KMIP-Integration-with-Vormetric-Data-Security-Manager-Integration-guide.pdf){: external}Vormetric protects VMware workloads by encrypting VM data.
* [Deploy a trusted cloud solution with IBM, VMware, and HyTrust](https://www.hytrust.com/solutions/ibm-cloud-secure-virtualization/){: external} You can integrate the various architectural elements to create a chain of trust from hardware up through the hypervisor and management applications.


**Note:** The cookbooks are intended for experienced vSphere Administrators. Some topics that are covered, consider that the reader has basic deployment skills to install and configure vSphere and vCenter.
