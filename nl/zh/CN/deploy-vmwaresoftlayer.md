---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 使用手册进行 VMware 部署

VMware 管理员可以通过部署到 {{site.data.keyword.BluSoftlayer_full}} 企业级的全球云，快速实现具有成本效益的混合云特征。可以将 vSphere 工作负载和目录供应到 {{site.data.keyword.cloud_notm}} 数据中心内的 VMware vSphere 环境，而无需修改 VMware VM 或访客。通过使用公共 vSphere 系统管理程序和管理/编排平台，可以实现这些部署。vSphere 实现还可以利用 VMware vCloud Suite 的其他组件 - vCloud Automation Center、vCenter Operations Management Suite、vSAN、vCloud Network & Security、Site Recovery Manager、vCenter Orchestrator 和 NSX。

VMware 手册系列的核心目标是帮助 vSphere 管理员在 IBM Cloud 基础架构中部署 VMware vSphere 环境。这些手册的目的不是为了培训您如何管理 vSphere。有关管理 vSphere 的更多信息，请参阅 [VMware Education ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}。

{{site.data.keyword.cloud_notm}} 有若干特定功能支持 VMware 管理员以自助服务方式灵活地使用裸机实例和网络、存储器以及备份和恢复构造。然后，您可以使用这些构造来部署全功能 vSphere 实现，这些实现可以构建为扩展或替换内部部署的 vSphere 实现 (VMware@Home)。

管理员可以使用以下手册：

* [构建单站点 VMware 环境](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html)：作为 vSphere 管理员，您将逐步完成构建环境的各步骤，包括使用耐久性或高性能块存储器或使用 QuantaStor。
* [Migrate vSphere Workloads ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window}：提供的方案可帮助您在将 vSphere 实现部署到 IBM Cloud 数据中心后，将工作负载 [虚拟机 (VM)] 迁移到 VMware。
* [Leverage NSX® ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window}：您可以利用 VMware NSX 为 VMware@SoftLayer 部署提供软件定义联网 (SDN) 构造。
* [Catalogic ECX ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window}：您可以在混合 IT 基础架构中管理和分析 CopyData。该基础架构通过使用 Catalogic Software 智能 Copy Data 管理平台 ECX 以及使用 NetApp 专用存储器和 VMware vSphere 基础架构，在 IBM Cloud 基础架构上进行部署。
* [VMware Back Up ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window}：此手册描述了对在 VMware 部署中运行的基于 VMware 的工作负载 (VM) 进行备份、恢复和归档的备用方法。
* [VMware Disaster Recovery ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window}：此手册详细描述了使用 VMware 建立灾难恢复 (DR) 解决方案的两个用例。第一个用例对应于支持恢复内部部署工作负载的内部部署 VMware 环境，反之亦然。第二个用例是在另一个 {{site.data.keyword.cloud_notm}} 数据中心内恢复 VMware 工作负载。
* [Vormetric Encryption of VMware ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window}：各用例说明 Vormetric 如何通过对 VM 数据进行加密来保护 VMware 工作负载。
* [Deploy a trusted cloud solution with IBM, VMware, and HyTrust ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window}：您可以集成各种体系结构元素，以创建从硬件一直到系统管理程序和管理应用程序的信任链。


**注：**这些手册适用于经验丰富的 vSphere 管理员。其中涵盖的某些主题默认读者具有基本的部署技能，可安装和配置 vSphere 和 vCenter。
