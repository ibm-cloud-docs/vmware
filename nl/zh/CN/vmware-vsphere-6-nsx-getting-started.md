---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 NSX 入门 

NSX 作为许可权利部署，供您应用于基础架构。{{site.data.keyword.BluSoftlayer_full}} 逐个处理器提供许可证（定价不会因为每个 CPU 的核心数而更改）。在使用 NSX 组件（管理、控制或数据平面）的每个服务器上都需要 NSX 许可证。NSX 向平台添加了额外的联网功能。您可以创建稳健的覆盖网络，以实现系统安全性、租户分段以及跨提供者的混合云环境，或者从内部部署的私有云进行扩展。
{:shortdesc}

您可以通过 RESTful API 将防火墙、负载均衡、VPN、NAT 服务和基于 VXLAN 的微分段添加到环境中以支持自动化。

## 添加许可证
使用以下过程将许可证添加到服务器：
1. 使用 vSphere Client 登录到 vCenter Server。
* 在**管理**下，单击**许可**。
* 单击**解决方案**。
* 在产品列表中，单击 **VMware NSX for vSphere**。
* 单击**许可证密钥**或**输入新的许可证密钥**。
* 单击**确定**。

## 安装 NSX

1. 部署 NSX Manager。
* 向 vCenter Server 注册 NSX Manager。
* vSphere Web Client 通过 NSX Manager 部署 NSX Controller 实例。
* 使用 NSX Manager 来准备 vSphere 主机，以在集群中的主机上安装 VIB。
* 在所有适用主机上部署 NSX Controller 后，定义并配置 NSX 组件，如 Edge 网关、负载均衡器和防火墙。

## 部署注意事项

为解决方案启用 NSX 需要除了标准计算节点外，还使用额外的 vSphere 节点。

**NSX Manager**<br />
管理集群上的 IBM Informix Virtual Appliance 与 vCenter 之间存在一对一的关系。建议使用标准 HA vSphere 功能。NSX Manager 包含已安排/按需提供的备份功能，并需要与 vCenter、控制器、NSX Edge 资源和 ESXi 主机建立 IP 连接。NSX Manager 部署到 vCenter 所在的子网/VLAN 中，但这不是严格必需的。典型的 VM 大小调整如下：

|NSX 发行版|vCPU|内存|操作系统磁盘|
|---|---|---|---|
|6.2（小型）|4|12 GB|60 GB|
|6.2（缺省）|4|16 GB|60 GB|
|6.2（大型）|4|24 GB|60 GB|
{: caption="表 1. NSX Manager 的典型 VM 大小调整" caption-side="top"}

**NSX Controller 节点**<br />
NSX Controller 节点通过 NSX Manager UI 部署为虚拟设备。每个设备通过非重复 IP 地址（通常位于 NSX Manager 所在的子网中）进行通信，但这不是硬性要求。建议至少将三个控制器 VM 部署到至少三个不同的物理 vSphere 节点。这些节点通过 NSX Manager 定义的作业划定，以主动/主动/主动形式工作。如果一个节点发生故障，那么会发生“多数规则”故障转移，以将工作负载重新分发到其余控制器上。NSX 不会本机强制实施此设计实践。您可以使用本机 vSphere 反亲缘关系规则，以避免将多个控制器节点部署在同一 ESXi 服务器上。每个 VM 的典型 VM 大小调整如下：

|控制器 VM|vCPU|保留量|内存|操作系统磁盘|
|---|---|---|---|---|
|3|4|2048 Mhz|4 GB|20 GB|
{: caption="表 2. NSX Controller 的典型 VM 大小调整" caption-side="top"}

**NSX 交换机**
升级后的虚拟分布式交换机 (VDS) 部署到所有主机以实现分布式功能。

**NSX Edge 服务网关**<br />
在环境中根据需要部署为多功能 VM 设备。仅限用于路由，最多可以部署 8 个网关的活动集群。对于其他任何/所有服务，都会将其部署在活动/备用部署中。VM 环境外部的通信需要 IBM Cloud 分配的可移植 IP，以包含任何 NAT 池、VIP 和 VPN 端点。

|网关形式|vCPU|内存|特定用途|
|---|---|---|---|
|超大型|6|8 GB|适用于 L7 高性能 LB|
|较大型|4|1 GB|适用于高性能的 ECMP 和 FW 部署|
|大型|2|1 GB|小型 DC 和单服务|
|精简|1|512 MB|小型部署、单服务使用或 PoC|
{: caption="表 3. NSX Edge 服务" caption-side="top"}

