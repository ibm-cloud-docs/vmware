---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# QuantaStor 体系结构指南

您可以为 VMware ESXi 5 环境订购和配置 OSNexus QuantaStor 共享存储器解决方案。请将以下信息与[高级单站点 VMware 参考体系结构](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html)手册一起使用，在 VMware 环境中设置其中一个存储器选项。

## 步骤 1：订购 QuantaStor 共享存储器

下存储器订单之前，需要确定满足容量和 I/O 需求的规范。这些规范包括但不限于服务器 RAM、磁盘驱动器的类型和数量、用于缓存的 SSD、RAID 配置和联网配置。有关在您的环境中选择正确 QuantaStor 配置的更多信息，请参阅 [QuantaStor Solution for Virtualization ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide#Server_Virtualization){: new_window}。

对于示例环境，将使用可以提供虚拟机 (VM) 所需足够容量和 I/O 的较小配置。确保您了解 VM 的容量和 I/O 需求，然后再下单。虽然 QuantaStor 服务器是可扩展的，但初始调整硬件大小也非常重要，这可避免配置和部署中发生延迟。

### 订购 QuantaStor

使用以下步骤来订购 QuantaStor 服务器。

1. 登录到 [{{site.data.keyword.slportal_full}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window}，然后单击**帐户 > 下单**。
2. 在弹出屏幕上，选择“{{site.data.keyword.baremetal_short}}”>“每月”。
3. 从“服务器列表”页面中，选择有能力存储环境中所需磁盘数的相应服务器。[对于示例环境，将选择具有 12 个驱动器托架的 12 核系统（即，双六核）。]
4. 输入以下配置选项：
  * **数据中心：**先前创建的 VLAN 和 ESXi 主机的位置
  * **服务器：**双处理器六核 Xeon
  * **RAM：**64 GB
  * **操作系统：**OSNexus QuantaStor 3.x (4 TB)
  * **硬盘驱动器：**
    * 磁盘 1 和 2：RAID 1 中 500 GB SATA
    * 分区模板：Linux 基本版
    * 磁盘 3-10：RAID-10 中 600 GB SAS 15000
  * **公用带宽：**仅限专用网络
  * **上行端口速度：**10 Gbps 冗余专用网络上行链路
5. 单击**继续处理订单**。

**注：**存储服务器配置了两个未结合的网络接口，因此可以使用两个不同的子网将流量负载均衡到存储阵列。

### 完成配置

现在，您的购物车中有一个 QuantaStor 设备。您现在需要向该设备分配专用 VLAN、主机名和域，以便正确供应该设备。

1. 分配以下 VLAN 并为设备创建主机名：QuantaStor 主机 - 后端 VLAN：（在环境中为 1102）
2. 选择付款方式，同意“条款和条件”，然后单击“最终确定订单”。

**注：**在服务器已供应并可通过 VPN 或虚拟服务器进行访问之前，请勿继续执行步骤 3。

## 步骤 2：为管理和容量主机启用 iSCSI Software Adapter

必须在每个管理和容量主机上启用 iSCSI Software Adapter，并在装载 iSCSI 卷之前收集其 iSCSI 限定名 (IQN)。使用以下步骤来启用 iSCSI Software Adapter：

1. 转至 ESXi 管理或容量主机，然后选择“管理”>“存储器”>“存储适配器”。
2. 单击绿色加号 (+) 并添加 iSCSI Software Adapter。
3. 启用后，单击对应于 iSCSI Software Adapter 的 vmhba，并记录“适配器详细信息”部分中的“iSCSI 名称”（图 1）。
4. 对于每个 ESXi 管理和容量主机上的每个 iSCSI Software Adapter，执行步骤 1 - 3。

## 步骤 3：配置 QuantaStor

供应服务器后，可以设置共享存储器设备。具体地说，可设置联网并配置 iSCSI 卷，然后将卷分配给主机。 

例如，卷 vmk3 具有 vmnic0，用于连接到存储器 VLAN 上的“可移植专用子网 A”。卷 vmk4 具有 vmnic2，用于连接到存储器 VLAN 上的“可移植专用子网 B”。QuantaStor 服务器还具有两个专用网络适配器 eth4 和 eth6，用于连接到存储器 VLAN。

### 配置联网

1. 打开 Web 浏览器，然后转至 [{{site.data.keyword.slportal_short}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window} 上的**设备**页面中列出的 QuantaStor IP 地址。
2. 输入**管理用户名**和**密码**（位于**设备详细信息**页面上的“密码”部分中）。继续之前，请记下 QuantaStor 服务器所使用的专用网络设备，例如 eth4。
3. 转至**存储系统 > 网络端口**。
4. 从网络适配器列表中选择活动的专用适配器（示例：eth4）。右键单击并从弹出菜单中选择**修改网络端口**。
5. 清除**启用 iSCSI** 复选框以禁用与此适配器的 iSCSI 连接，然后单击**确定**。
6. 选择不活动但已分配给专用网络的专用适配器（示例：eth6）。
7. 右键单击 eth6 适配器，并从弹出菜单中选择**修改网络端口**。
8. 在**修改网络端口**屏幕上，对于**配置类型**，选择**静态**。
9. 输入适配器的主专用 IP 地址、子网和网关。如果要使用[高级单站点 VMware 参考体系结构](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html)手册中的 VLAN 工作表，请使用“存储器”行中的地址。
10. 清除**启用 iSCSI** 复选框以禁用与此适配器的 iSCSI 连接。
11. 为该专用适配器配置 IP 地址后，右键单击该适配器，并选择**启用网络端口**以使其联机。
12. 单击**确定**以在验证 IP 地址后启用端口。

### 开具支持凭单

为第二个适配器配置主专用 IP 地址后，需要开具支持凭单。开具凭单有助于确保在 VLAN 上供应其他计算机时，不会占用您使用的 IP 地址。

1. 单击**支持** > **添加凭单**，然后输入以下信息：
  * 主题：专用网络问题
  * 标题：保留和分配专用 IP 地址
  * 关联设备：“选择 QuantaStor 服务器”
  * 详细信息：在 VLAN 上保留和分配。此 IP 地址用于 QuantaStor 服务器上的第二个适配器。

### 配置 QuantaStor

现在，阵列可以接受来自两个适配器的连接，那么必须分配这两个适配器在“存储路径 A”和“存储路径 B”子网上的虚拟接口。

  1. 右键单击初始专用适配器接口 (eth4)，并在弹出菜单中选择**创建虚拟接口**。
  2. 在生成的弹出屏幕上，输入适配器的可移植专用 IP 地址和子网，并确保选中**启用 iSCSI**。
  3. 如果要使用 VLAN 工作表，请使用“存储路径 A”行中的地址。
  4. 记录“可移植 IP 地址”页面上“注释”部分中使用的 IP 地址。
  5. 选择要绑定虚拟接口的初始专用适配器接口 (eth4)，然后单击**确定**。
  6. 右键单击另一个专用适配器接口 (eth6)，并在弹出菜单中选择**创建虚拟接口**。
  7. 在生成的弹出窗口上，输入适配器的可移植专用 IP 地址和子网，并确保选中**启用 iSCSI**。
  8. 如果要使用 VLAN 工作表，请使用“存储路径 B”行中的地址。
  9. 记录“可移植 IP 地址”页面上“注释”部分中使用的此 IP 地址。
  10. 选择要绑定虚拟接口的另一个专用适配器接口 (eth6)，然后单击**确定**。

为 QuantaStor 服务器配置了 IP 地址和虚拟接口后，您需要配置路由以确保出局流量使用正确的接口（因为有两个 NIC，但位于不同的子网上）。

1. 使用 root 用户凭证通过 SSH 登录到 QuantaStor 服务器，然后将以下行附加到 /etc/network/interfaces。假定 eth4 和 eth6 是专用网络上的 NIC：
  * post-up ip route add 10.0.0.0/8 via dev eth4
  * post-up ip route add 10.0.0.0/8 via dev eth6 table eth6
  * post-up ip rule add from table eth6

### 创建存储池

接下来，必须创建用于分配卷的存储池，然后才能创建卷或共享。

1. 右键单击**存储池**，并选择**创建存储池**。
2. 在**创建存储池**屏幕上，输入以下信息：
  * 名称：输入适用的存储池名称。示例：StoragePool-01
  * 池类型：缺省值 (zfs)
  * I/O 概要文件：虚拟化
  * 要用于存储池的磁盘：sdb
3. 单击**确定**。

如果 sdb 不可用于添加到池中，原因是存在分区且该分区标记为可引导。您需要在 Quantastor 控制台上使用 gdisk 来除去该分区和所有 /etc/fstab 条目。接下来，您需要创建卷以供 ESXi 使用。

### 创建 iSCSI 存储卷

您需要创建两个存储卷。一个卷用于管理集群上的管理 VM，另一个卷用于容量集群上的 VM。完成以下步骤以创建 iSCSI 存储卷：

1. 右键单击**存储卷**，并在弹出菜单上选择**创建存储卷**。
2. 输入存储卷的信息。**注：**尽管配置可能因工作负载和存储容量而有所不同，但是该示例仍对每个存储卷显示表 1 和表 2 中的值。

|字段|值|
|---|---|
|名称|Mgmt-LUN0|
|存储池|[先前步骤中配置的存储池名称]|
|大小|500 GB|
|保留百分比|50|
|压缩|已启用|
{: caption="表 1. iSCSI 管理卷" caption-side="top"}

|字段|值|
|---|---|
|名称|Capacity-LUN0|
|存储池|[先前步骤中配置的存储池名称]|
|大小|3 TB|
|保留百分比|50|
|压缩|已启用|
{: caption="表 2. iSCSI 容量卷" caption-side="top"}

### 为主机分配对卷的访问权

设置卷之后，您需要配置 QuantaStor，以允许 ESXi 主机通过每个主机的 IQN 对这些卷进行访问。

1. 浏览至 QuantaStor 管理页面，右键单击**主机**菜单，并选择**添加主机**。
2. 在**添加主机**屏幕上，输入以下信息：
  * 主机名：输入适用的主机名。主机名不包含标准域名 (FQDN)，但应该对主机进行描述。示例：MyESXiHostName
  * 操作系统类型：VMware
  * 启动程序：iSCSI 限定名 (IQN) 单选按钮
  * iSCSI 限定名：相应主机的 IQN。
3. 单击**确定**。

针对 ESXi 环境中的每个管理主机和容量主机，执行以下步骤。

在管理集群和容量集群中添加每个主机后，执行以下步骤：

1. 右键单击**主机组**菜单，并选择**创建主机组...**。
2. 在**名称**字段中输入“ManagementCluster”，然后选择位于管理集群中的所有主机。
3. 单击**确定**。这将创建主机组，可以为该组分配特定的卷。

对容量集群重复此过程。

1. 单击**存储卷**菜单。
2. 右键单击 **Mgmt-Lun0** 卷，并选择**分配/取消分配主机访问权**。
3. 确认 **Mgmt-Lun0** 是下拉菜单中的一个选项，然后选择在先前步骤中创建的主机组。此选项允许管理集群中的每个 ESXi 主机访问 Mgmt-Lun0 卷。对 **Capacity-LUN0** 执行相同的操作。

## 步骤 4：在管理/容量集群上装载卷

登录到 vSphere Web 客户机，然后转至 **vCenter 库存列表**下的**主机**。

使用以下步骤在 ESXi 主机上装载卷：

1. 选择一个主机，然后单击**管理 > 存储器** > **存储适配器**。
2. 选择**目标** > **动态发现** > **添加...**。
3. 在**添加发送目标服务器**屏幕上，输入在“存储路径 A”上分配给 QuantaStor 存储设备的 IP 地址。
4. 将“端口”保留为 **3260**，然后单击**确定**。
5. 单击**动态发现** > **添加...**。对“存储路径 B”重复步骤 4 和 5。

ESXI 主机已准备好重新扫描 iSCSI Software Adapter 来发现 Mgmt-Lun0 卷。

1. 选择**存储适配器**屏幕上的**重新扫描存储适配器**图标（图 9）。
2. 保留生成的弹出屏幕上的缺省选项，然后单击**确定**。
3. 发现卷之后，单击**操作 > 新建数据存储器**，并将其格式设置为 **VMFS-5**。
4. 确认格式设置完成，然后单击**存储设备 > 设备详细信息 > 编辑多路径...**。
5. 对于**路径选择策略**，选择**循环法**，然后单击**确定**。

现在 Mmgt-Lun0 卷已连接到单个主机，您必须返回到集群中的其他管理主机，然后重复该过程来添加该卷。但是，您不需要设置该卷的格式，因为它已设置为 VMFS-5 格式，并且在发现后即按此格式显示。

## 步骤 5：在 vSphere ESXi 主机中禁用延迟确认

存储器 LUN 已连接到管理主机和容量主机后，需要立即禁用延迟确认。

1. 转至 vSphere 环境，然后选择**存储适配器** > **iSCSI Software Adapter** > **高级选项**。
2. 单击**编辑**，然后一直滚动到“高级选项”屏幕的末尾。
3. 清除 **DelayedAck** 复选框，然后单击**确定**。

有关与 VMware 相关的延迟确认的更多信息，请参阅 [VMware 知识库](https://kb.vmware.com/s/article/1002598)。

现在，您可以返回到[高级单站点 VMware 参考体系结构](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html)手册并完成环境设置。
