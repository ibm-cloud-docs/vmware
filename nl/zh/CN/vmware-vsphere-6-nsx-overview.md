---
copyright:
  years: 1994, 2017
lastupdated: "2017-06-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 NSX 概述

VMware NSX&reg; 是一个软件联网和安全虚拟化平台，用于为网络提供虚拟机的运行模型。虚拟网络会在软件中重现第 2 层到第 7 层网络模型，支持通过编程方式在数秒内创建并供应复杂的多层网络拓扑，而无需额外的 {{site.data.keyword.BluSoftlayer_notm}} 专用网络。NSX 还提供了一个新模型用于实现网络安全性。安全概要文件由虚拟端口分发并强制执行，并随虚拟机一起移动。

NSX 支持 VMware 软件定义的数据中心策略。软件定义的数据中心体系结构借助扩展抽象、汇聚和自动化所有数据中心资源和服务的虚拟化功能，通过策略驱动的自动化来简化和加速计算、存储和联网资源的供应与管理。通过对网络进行虚拟化，NSX 交付了新的联网运行模型，打破了当前的物理网络障碍，使得 VMware 和 {{site.data.keyword.BluSoftlayer_notm}} 能以更低的成本更快、更敏捷地运行。

NSX 包括一个逻辑联网服务库 - 逻辑交换机、逻辑路由器、逻辑防火墙、逻辑负载均衡器、逻辑 VPN 和分布式安全性。您可以在隔离的基于软件的虚拟网络中创建这些服务的定制组合，以支持现有应用程序而无需进行修改，或者为新的应用程序工作负载交付独特的需求。虚拟网络通过编程方式进行供应和管理，而与 {{site.data.keyword.BluSoftlayer_notm}} 联网构造无关。这种与硬件解耦的做法引入了灵活性、速度和运行效率，可以变换数据中心的运营。NSX 的优点包括以下功能：
* 数据中心自动化
* 自助服务联网服务
* 利用自动化网络和服务供应，快速部署应用程序
* 在同一裸机基础架构上隔离开发、测试和生产环境
* 单个帐户多租户云

NSX 可以通过 vSphere Web Client、命令行界面 (CLI) 和 REST API 进行配置。NSX 提供的核心网络服务包括：

## 逻辑交换机
云部署或虚拟数据中心可能具有各种跨多个租户的应用程序。这些应用程序和租户需要相互隔离，以实现安全性、故障隔离并避免重叠 IP 寻址问题。NSX 逻辑交换机创建应用程序或租户虚拟机可以通过逻辑方式连接到的逻辑广播域或分段 (VXLAN vWire)。这允许灵活、快速地进行部署，同时仍提供物理网络广播域 (VLAN) 的所有特性，而不会随意扩展物理第 2 层。逻辑交换机支持将数千个租户网络供应到单个 {{site.data.keyword.BluSoftlayer_notm}} 专用网络 (VLAN) 上。逻辑交换机是分布式的，并且范围可跨任意大的计算集群，甚至可以跨同一个数据中心内的多个 Pod。这允许虚拟机在数据中心内移动，对各 Pod 之间的物理第 2 层 (VLAN) 边界没有限制。

## 逻辑路由器
动态路由在第 2 层广播域（VXLAN vWire/逻辑交换机）之间提供必要的转发信息，从而允许您减少第 2 层广播域，提高网络效率和规模。NSX 将此情报扩展到工作负载所在的位置，以提供东西路由功能。这允许虚拟机到虚拟机之间进行更直接的通信，而无需耗费成本或时间来扩展中继段。同时，NSX 还提供了 {{site.data.keyword.BluSoftlayer_notm}} 数据中心南北入站/出站连接，从而使租户能够安全、高效地访问公用网络。

## 逻辑防火墙
逻辑防火墙为动态虚拟数据中心提供了安全机制。NSX 逻辑防火墙的“分布式防火墙”组件支持根据 VM 名称和属性、用户身份和 vCenter 对象（例如，数据中心和主机）以及传统联网属性（例如，IP 地址和 VLAN 等）来对虚拟数据中心实体分段。“Edge 防火墙”组件帮助您实现关键的周边安全性需求（例如，基于 IP/VLAN 构造来构建 DMZ）、多租户虚拟数据中心内租户到租户的隔离、网络地址转换 (NAT)、VPN 和基于用户的 SSL VPN。“Edge 防火墙”可以与 {{site.data.keyword.BluSoftlayer_notm}} 中的 Vyatta 和 Fortinet 服务组合使用，也可以取代这两个服务，以实现周边保护。“防火墙流监视”功能显示虚拟机之间应用程序协议级别的网络活动。您可以使用这些信息来审计网络流量，定义和优化防火墙策略，以及识别对网络的威胁。

## 逻辑虚拟专用网 (VPN)
SSL VPN-Plus 支持远程用户访问专用企业应用程序。IPSec VPN 提供 NSX Edge 实例与远程站点（在 {{site.data.keyword.BluSoftlayer_notm}} 上运行的 VMware）之间的站点间连接。L2 VPN 通过允许虚拟机跨地理边界以及跨 {{site.data.keyword.BluSoftlayer_notm}} 数据中心和本地 VMware 环境来保留网络连接，从而支持您扩展数据中心。

## 逻辑负载均衡器
NSX Edge 负载均衡器支持网络流量通过多条路径流至特定目标。负载均衡器通过在多个服务器之间均匀分发入局服务请求，并且使负载分发对用户透明。因此，负载均衡有助于实现最佳的资源利用率，最大限度地提高吞吐量和缩短响应时间，避免发生超负荷。NSX Edge 提供最高第 7 层负载均衡。

## 服务组合器
服务组合器可帮助您为虚拟基础架构中的应用程序供应和分配网络与安全服务。这些服务可以映射并应用于安全组中的虚拟机。Data Security 提供了对存储在您组织的虚拟化环境和云环境（包括 {{site.data.keyword.BluSoftlayer_notm}}）中敏感数据的可视性。根据 NSX Data Security 所报告的违例，您可以确保敏感数据受到充分的保护，并评估与世界各地法规的合规性。

## NSX 可扩展性
VMware 合作伙伴可以将其网络服务解决方案与 NSX 平台集成，从而支持客户获得对各个 VMware 产品和合作伙伴解决方案的综合体验。数据中心操作员可以在数秒内供应复杂的多层虚拟网络，而与 {{site.data.keyword.BluSoftlayer_notm}} 中的底层网络拓扑或组件无关。

## NSX 核心组件
本部分描述将部署在 {{site.data.keyword.BluSoftlayer_notm}} 上的核心 NSX 组件。这些组件可以通过 vSphere Web Client、命令行界面 (CLI) 和 REST API 进行配置/管理。VMware NSX 需要正常运行的 {{site.data.keyword.BluSoftlayer_notm}} 环境，此环境中至少部署了 vSphere 和 vCenter V6。本部分中描述的所有组件都会作为在 {{site.data.keyword.BluSoftlayer_notm}} 上运行的 VMware 设备 VM 进行部署。不支持将 NSX 组件作为虚拟服务器实例 (VSI)。建议遵循指导信息来创建专用 ESX 管理集群，此外还可能需要 Edge 服务集群，这将在本文档中做进一步讨论。

<!-- ![Figure 1](images/vmware6_nsx_overview_1.png)-->

## NSX Manager
NSX Manager 是 NSX 的集中式网络管理组件，作为虚拟设备安装在 vCenter Server 环境中的 ESX 主机上。{{site.data.keyword.BluSoftlayer_notm}} 体系结构建议将此 VM 部署在专用管理 ESX 集群上。一个 NSX Manager 可映射到单个 vCenter Server 环境以及多个 NSX Edge、vShield Endpoint 和 NSX Data Security 实例。

## NSX vSwitch
NSX vSwitch 是在 {{site.data.keyword.BluSoftlayer_notm}} ESX 主机上运行的软件，用于在服务器与物理网络之间形成软件抽象层。随着对数据中心的需求不断增长和加速，与对数据本身的速度和访问相关的需求也在不断增长。在大多数基础架构中，虚拟机访问和移动性通常取决于物理联网基础架构及其所在的物理联网环境。由于潜在的第 2 层或第 3 层边界（例如，与特定 Pod 中的特定 {{site.data.keyword.BluSoftlayer_notm}} 专用网络 (VLAN) 相关），这可能会强制虚拟工作负载进入不太理想的环境。NSX vSwitch 支持将这些虚拟工作负载置于数据中心内任何可用的基础架构上，而不考虑底层物理网络基础架构。这不仅能提高灵活性和移动性，还提高了可用性和弹性。

## NSX Controller 
NSX Controller 是一种高级分布式状态管理系统，可控制虚拟网络和 VXLAN 覆盖传输隧道。NSX Controller 是网络中所有逻辑交换机的中央控制点，并维护所有虚拟机、主机、逻辑交换机和 VXLAN 的信息。控制器支持三种逻辑交换机控制平面方式：多点广播、单点广播和混合。这些方式将 NSX 与物理网络解耦。{{site.data.keyword.BluSoftlayer_notm}} 需要单点广播方式，因为 {{site.data.keyword.BluSoftlayer_notm}} 专用网络 (VLAN) 不会为多点广播或混合方式提供 IGMP 服务。NSX Controller 将利用单点广播方式和虚拟隧道端点 (VTEPS) 来提供 MAC 学习和其他功能，以支持逻辑交换机中的 VXLAN 广播、未知单点广播和多点广播 (BUM) 流量。单点广播方式会在主机上本地复制所有 BUM 流量，并且在 VTEPS 之间的第 3 层连接外部，无需进行物理网络配置。NSX Controller 由 NSX Manager 部署为至少包含 3 个控制器节点（以及用于支持（分布式）第 3 层路由服务的其他各种节点）的集合。所有节点都作为虚拟机进行部署，并由位于 {{site.data.keyword.BluSoftlayer_notm}} 的 ESX 管理集群上的 NSX Manager 进行管理。

## NSX Edge
NSX Edge 提供网络边缘安全性和网关服务，以隔离虚拟化网络。您可以将 NSX Edge 安装为逻辑（分布式）路由器或服务网关。NSX Edge 逻辑（分布式）路由器通过租户 IP 地址空间和数据路径隔离来提供东西分布式路由。同一主机上位于不同子网中的虚拟机或工作负载可以相互通信，而不必遍历传统的路由接口。NSX Edge 网关通过提供常用网关服务（例如，DHCP、VPN、NAT、动态路由选择和负载均衡），将隔离的存根网络连接到共享（上行链路）网络。NSX Edge 的常见部署包括部署在 DMZ、VPN 外联网和多租户云环境中，其中 NSX Edge 会为每个租户创建虚拟边界。
