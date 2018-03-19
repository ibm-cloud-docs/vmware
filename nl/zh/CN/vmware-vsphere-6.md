---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware 许可选项 

VMware 管理员可以通过部署到 {{site.data.keyword.BluSoftlayer_full}} 企业级的全球云，快速实现具有成本效益的混合云特征。关键的 {{site.data.keyword.BluSoftlayer_notm}} 特色是可以将 vSphere 工作负载和目录供应到 {{site.data.keyword.BluSoftlayer_notm}} 数据中心内的 VMware vSphere 环境，而无需修改 VMware VM 或访客。通过使用公共 vSphere 系统管理程序和管理/编排平台，可以实现这些部署。

除了提供 vSphere 6 Enterprise Plus 许可证外，{{site.data.keyword.BluSoftlayer_notm}} 还为 vCenter、NSX、vRealize、vSAN 和 Site Recovery Manager (SRM) 提供每月许可。

## VMware vSphere

**目标用途：**裸机服务器虚拟操作系统平台，可对处理器、内存、存储器和联网资源进行抽象化，从而在单个物理服务器上创建多个虚拟服务器。可以将多个物理服务器集群在一起，以创建私有云。

**用户界面：**vCenter Client、VMware API 和 VMware CLI

**功能：**
* vMotion 实时迁移
* 高可用性
* 容错
* 复制
* Nvidia GRID vGPU 虚拟化
* 工作负载容量优化
* 分布式资源调度程序 (DRS)
* 精简供应
* 网络 I/O 控制

## VMware vCenter

**目标用途：**集中管理每个 vSphere 主机中的计算资源。虽然 vSphere 主机可以单独管理，将这些主机置于 vCenter 控制下则可启用以下功能：

**用户界面：**Web Client、Thick Client、VMware API 和 VMware CLI

**功能：**
* 集中控制和显示受管 vSphere 主机和访客虚拟机中的所有方面。
* 通过 vCenter Web Client 提供单窗格的玻璃界面视图，用于计算网络和存储器管理。
* 主动优化。支持分配和优化资源，以在各 vSphere 主机上实现最高效率。
* 其他集成附加组件和服务（例如，NSX、vRealize、vSAN 和 Site Recovery Manager (SRM)）的扩展管理功能。
* 监视、警报和安排。云管理员可以在 vCenter Web Client 中查看事件和警报并配置安排的操作。
* 自动化引擎。vCenter 是执行通过 vSphere API Web 界面向其提供的任务的引擎。VMware vRealize Automation 和 vRealize Orchestration 是通过 VMware API 驱动 vCenter 操作的应用程序的示例。

## VMware NSX

**目标用途：**NSX 提供软件定义的网络 (SDN) 功能，这些功能对于支持云平台操作至关重要。

**用户界面：**vCenter Client、VMware API 和 VMware CLI

**功能：**
* 负载均衡
* 防火墙
* 路由
* 逻辑交换机
* VPN
* VxLAN 分段/隧道端点

## VMware vRealize

**目标用途：**VMware vRealize Suite 是一个企业就绪型云管理平台，可用于管理异构的混合云。

**用户界面：**vCenter Client、VMware API 和 VMware CLI

**许可证模型：**按月按处理器许可

**功能：**
* vRealize Automation：自动交付个性化基础架构、应用程序和定制 IT 服务
* vRealize Operations：智能运行状况、性能、容量和配置管理编排
* vRealize Log Insight：实时日志管理和日志分析。

## VMware vSAN

**目标用途：**VMware vSAN 是一种分布式存储技术，支持每个 vSphere 主机上的本地存储驱动器聚合并汇聚到无共享内容的存储设备，此设备可供 vSAN 集群中的所有主机访问。

**用户界面：**vCenter Client、VMware API 和 VMware CLI

**功能：**
* 基于分布式主机的存储器
* 无共享内容的体系结构
* 最多可扩展到 64 个节点
* 低延迟
* 可配置容错

## VMware Site Recovery Manager (SRM)

**目标用途：**VMware Site Recovery Manager (SRM) 支持跨私有云环境中各站点的应用程序可用性和移动性。通过充分利用虚拟机封装和隔离，Site Recovery Manager 能够简化灾难恢复的自动执行，以满足恢复时间目标 (RTO)。SRM 还可帮助降低与业务连续性计划关联的成本，并实现低风险、可预测的虚拟环境恢复结果。

**用户界面：**vCenter Client、VMware API 和 VMware CLI

**功能：**
* 非中断性恢复测试
* 自动化编排工作流程
* 自动恢复网络和安全设置
* 可扩展定制自动化
* 编排的跨 vCenter 的 vMotion
* 集中式恢复计划
* 基于策略的管理
