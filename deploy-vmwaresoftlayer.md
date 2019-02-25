---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Using cookbooks for VMware deployments

VMware administrators can quickly realize cost-effective hybrid cloud characteristics by deploying into the {{site.data.keyword.BluSoftlayer_full}} enterprise-grade global cloud. vSphere workloads and catalogs can be provisioned onto VMware vSphere environments within the {{site.data.keyword.cloud_notm}} data centers without modififying VMware VMs or guests. These deployments are made  possible by using a common vSphere hypervisor and management/orchestration platform. vSphere implementations also can leverage other components of the VMware vCloud Suite – vCloud Automation Center, vCenter Operations Management Suite, vSAN, vCloud Network & Security, Site Recovery Manager, vCenter Orchestrator, and NSX.

The core objective of the VMware cookbook series is to assist vSphere administrators with the deployment of VMware vSphere environments within an IBM Cloud infrastructure. The cookbooks are not intended to train you how to administer vSphere. For more information about administering vSphere, see [VMware Education ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}.

{{site.data.keyword.cloud_notm}} has several specific capabilities that give VMware administrators the flexibility to consume bare metal instances and network, storage, and backup and recovery constructs in a self-service manner. You can then use these constructs to deploy fully functional vSphere implementations, which can be built to extend or replace on-premises vSphere implementations (VMware@Home).

The following cookbooks are available to administrators:

* [Build a Single Site VMware Environment](/docs/infrastructure/virtualization?topic=Virtualization-advanced-single-site-vmware-reference-architecture): You, as the vSphere administrator, are walked through the steps of building your environment, including the use of either Endurance or Performance Block Storage or QuantaStor.
* [Migrate vSphere Workloads ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window}: Scenarios are presented to help you migrate workloads [virtual machines (VMs)] into VMware after your vSphere implementation is deployed in an IBM Cloud data center.
* [Leverage NSX® ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window}: You can leverage VMware NSX to provide software-defining networking (SDN) constructs to VMware@SoftLayer deployments.
* [Catalogic ECX ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window}: You can manage and analyze CopyData in a hybrid IT infrastructure. The infrastructure is deployed on the IBM Cloud infrastructure by using the Catalogic Software intelligent Copy Data management platform, ECX, and by using NetApp Private Storage and VMware vSphere infrastructure.
* [VMware Back Up ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window}: This cookbook describes alternative approaches to backing up, recovering, and archiving VMware-based workloads (VMs) that are running in a VMware deployment.
* [VMware Disaster Recovery ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window}: This cookbook details two use cases that establish a disaster recovery (DR) solution by using VMware. The first pairs with an on-premises VMware environment that allows an on-premises workload to be recovered or vice versa. The second is recovering VMware workloads in a second {{site.data.keyword.cloud_notm}} data center.
* [Vormetric Encryption of VMware ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window}: Use cases illustrate how Vormetric protects VMware workloads by encrypting VM data.
* [Deploy a trusted cloud solution with IBM, VMware, and HyTrust ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window}: You can integrate the various architectural elements to create a chain of trust from hardware up through the hypervisor and management applications.


**Note:** The cookbooks are intended for experienced vSphere Administrators. Some topics that are covered, consider that the reader has basic deployment skills to install and configure vSphere and vCenter.
