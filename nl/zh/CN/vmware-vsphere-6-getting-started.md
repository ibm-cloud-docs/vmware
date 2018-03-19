---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 入门 

使用以下内容以开始使用 vSphere 6。

## 了解环境和配置

要优化 VMware 解决方案，建议您将专用网络 VLAN 和公用网络（可选，如果不需要，可以禁用公共端口）用于 VMware vSphere 环境。此供应概要文件支持以下第 2 层分段流量边界：

|示例 VLAN 标识|描述|类型|其他详细信息|
|---|---|---|---|
|VLAN1 - **1101**|管理，VxLAN|专用 BCR|本机未标记的 VLAN，订购时 VMWare 主机部署在其中的原始本机 VLAN|
|VLAN4 - **2200**|公用因特网访问 DMZ|公共 FCR|本机未标记的 VLAN，订购时 VMWare 主机部署在其中的原始本机 VLAN|
{: caption="表 1. 专用和公用 VLAN 示例" caption-side="top"}

## 下单订购 vSphere 服务器
1. 登录到 [{{site.data.keyword.slportal_full}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://control.softlayer.com/){: new_window}。
2. 单击**帐户 > 下单**。
3. 在**裸机服务器**部分中，单击**每月**。
4. 选择服务器。请参阅 VMware 支持出版物以了解最低需求：
  * 为示例选择了以下服务器。**注：**冗余要求具有双重未结合的公用和专用上行链路。确认您在其中创建了 VLAN 的数据中心是否具有未结合的上行链路。
  * 容量集群（数量：2）
    * 服务器配置：从“双处理器多核服务器”部分中选择 Intel Xeon V3 服务器
    * 软件：操作系统 = vSphere Enterprise Plus 6
    * 操作系统存储器：2 个 1 TB SATA（配置为 RAID 1）
    * 数据存储器：建议订购 2 TB SATA 或者 1.2 TB SSD 或耐久性/高性能 NFS SAN 存储器
      * 如果您对其他存储类型感兴趣，请参阅[用于 VMware 系统的存储器](select-storage-option-use-vmware.html)
      * 上行端口速度：1 Gbps 双重公用和专用网络（未结合）
        * 针对 VMware vSAN 解决方案，建议使用 10 Gbps 上行链路
5. 如果要在新的 IBM Cloud 数据中心创建新部署，请继续执行步骤 6。如果这是扩展或部署到现有数据中心，请选择首选的“后端 BCR VLAN”+“前端 FCR VLAN”。例如，“后端 BCR VLAN”为 1101，“前端 FCR VLAN”为 2200。**注：**如果这是新部署或是到新 DC 的新部署，那么订购服务器时会创建后端 BCR 和前端 FCR VLAN。
6. 输入**主机名**和**域**。
7. 复查订单，然后单击**最终完成订单**以开始供应过程。

## 下单订购 vCenter Server

vCenter 是 Windows 服务器的附加组件。此配置最高可扩展到 20 个 vSphere 主机。对于更大规模的实现，建议直接将 vCenter Server Appliance (VCSA) 部署到 vSphere 集群；请参阅[部署和配置 vCenter Server Appliance (vCSA)](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)。

使用以下步骤来订购安装了 vCenter 的虚拟服务器：

1. 登录到 {{site.data.keyword.slportal_short}}。
2. 单击**帐户 > 下单**。
3. 在“虚拟服务器”下，订购**每月**裸机服务器或虚拟服务器公用/专用节点实例 (VSI)。
  1. 要使 SoftLayer 虚拟服务器实例 (VSI) 有资格用于 vCenter 6.0，必须至少部署 **4 个 2.0 GHz 核心**和 **4 GB RAM**。
  2. 有关 vCenter 部署建议的列表，请参阅 [VMware vCenter Server&trade; 6.0 Deployment Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}。
4. 输入以下信息：
  * 基于建议的最低服务器配置
    * vCPU 核心配置：4 个 2.0 GHz 核心
    * RAM 配置：12 GB RAM
    * 软件：操作系统 = Windows Server 2012 R2 Standard Edition（64 位）
    * 特定于操作系统的附加组件：vCenter 6
    * 第一个磁盘：1 个 100 GB (SAN)
    * 第二个磁盘：1 个 50 GB (SAN)
    * 上行端口速度：1 Gbps 公用和专用网络上行链路

5. 如果这是到新 IBM Cloud 数据中心的新部署，请继续执行下面的步骤 6。如果此部署是扩展或部署到现有数据中心，请选择首选的“后端 BCR VLAN”+“前端 FCR VLAN”。例如，“后端 BCR VLAN”为 1101，“前端 FCR VLAN”为 2200。（如果这是全新部署或是到新 DC 的新部署，那么订购服务器时会创建后端 BCR 和前端 FCR VLAN。）
6. 输入**主机名**和**域**。
7. 复查订单，然后单击**最终完成订单**以开始供应过程。

## 订购可移植公用和专用子网/IP 地址

**注：**如果尚未完全供应 VLAN，请勿继续。

子网用于对 VMware 访客虚拟机 (VM) 和基于 VMware 主机内核的流量进行寻址。

1. 在控制门户网站中，单击**网络 > IP 管理 > 子网**。
2. 单击屏幕右上方的**订购 IP 地址**。
3. 选择**可移植专用**。
4. 选择相应的 VLAN（示例：bcr01.wdc04: 1101）。
5. 单击**继续**。
6. 填写**订购 IP 地址**表单。
7. 单击屏幕右上方的**订购 IP 地址**。
8. 单击**下单**。
9. 对于每个适用的 VLAN（例如，1101 和 2200）执行此过程。
  1. 有关 VLAN 的更多信息，请参阅 [VLAN 入门](/docs/infrastructure/vlans/getting-started.html)。

|子网类型|子网大小|绑定 VLAN|vSphere 主机用途|
|---|---|---|---|
|可移植 - 专用|/27 32 地址|**1101**|管理 VM|
|可移植 - 专用|/27 32 地址|**1101**|VM 内核端口用于 iSCSI 和 vMotion|
|可移植 - 专用|/27 32 地址|**1101**|专用 IP 用于访客 VM|
|可移植 - 公用|/27 32 地址|**2200**|公用 IP 用于访客 VM（可选）|
{: caption="表 2. 子网" caption-side="top"}

### 可选 - 在 vSphere 主机上禁用公共接口

如果您不打算使用 vSphere 公共接口，那么出于安全目的，可以将其禁用。

1. 在控制门户网站中，单击**设备 > 设备列表**。
2. 单击您的 vSphere 主机的名称。
3. 单击“配置”表，然后向下滚动到“网络”部分。
4. 对于所有主机的每个适用 vSphere 主机 eth1 和 eth3 对，选择**断开连接**

这还可以通过 [{{site.data.keyword.slapi_full}} ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window} 来执行。

## 创建和配置 vSphere 数据中心集群<!-- create and configure should be separate tasks-->

现在，您可以登录到 vCenter Server 并配置 vSphere 集群。

1. 在控制门户网站中，单击**设备 > 设备列表**。
2. 找到您的 vCenter 设备并单击其名称。
3. 将**设备详细信息**屏幕向下滚动到服务器的**网络**部分，并记下**专用 IP 地址**。
4. 向下滚动**设备详细信息**屏幕，并记下 Windows 操作系统和 vCenter 软件的**密码**。
5. 打开 Microsoft Remote Desktop (RDP) 会话，并通过其公用 IP 地址连接到您的 vCenter Server。
6. 使用在步骤 4 中获取的密码进行登录。**注：**如果是使用“专用 IP 地址”来访问 vCenter，那么需要有到 IBM Cloud 的活动 VPN 连接。有关 VPN 访问的更多信息，请参阅[启用对 IBM Cloud 基础架构专用网络的访问](/docs/customer-portal/getting-started.html#enable-private-network)。
7. 下载并安装传统 [vSphere Client ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window}，或通过链接 `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/` 来使用 vSphere Web Client。
8. 使用在步骤 3 和 4 中获取的 IP 地址和密码登录到 vCenter。
9. 右键单击左窗格中的 vCenter Server 名称，并选择**新建数据中心**。
10. 为数据中心输入相应名称。
11. 右键单击数据中心，并选择**新建集群**。
12. 输入集群名称。此时请勿开启集群功能 vSphere HA 或 vSphere DRS。
13. 单击**下一步**。
14. 使 **EVC** 保持禁用，然后单击**下一步**。
15. 接受_用于将交换文件存储在虚拟机所在目录的缺省值_，然后单击**下一步**。
16. 单击**完成**以完成集群。
17. 右键单击刚才创建的新集群，并选择**添加主机**。
18. 输入其中一个 vSphere 主机的 IP 地址或主机名，然后在**用户名**字段中输入 **Root**，并在**密码**字段中输入该主机的密码。
19. 单击**下一步**以依次完成“主机摘要”、“分配许可证”和“锁定方式”屏幕，然后单击**完成**以完成将主机添加到集群中的操作。
20. 对集群中的每个其他 vSphere 主机重复步骤 18 和 19。完成后，您将在新集群下看到各个 vSphere 主机。

### 为 vSphere 主机配置基本网络构造

使用以下步骤为集群中的 vSphere 主机配置基本构造。

1. 选择第一个 vSphere 主机，然后单击**配置**选项卡。
2. 在**硬件**部分下，选择**联网**。您应该已经有具有 vmnic0 的 vSwitch0；单击 vSwitch0 旁边的**属性**。
3. 在 **vSwitch 属性**窗口上选择**网络适配器**，然后单击**添加**按钮。
4. 选择要添加到 vSwitch0 的 vmnic2，然后单击**下一步**。
5. 确保这两个 vmnic 都是**活动适配器**，然后单击**下一步**。
6. 单击**完成**。
7. 单击**端口**选项卡，并确保 vSwitch 已突出显示；单击**编辑**。
8. 单击**常规**选项卡，然后将 **MTU** 更改为 9000（巨型帧）。
9. 单击 **NIC 组合**选项卡，并将负载均衡更改为**基于 IP 路由**散列，然后单击**确定**。
10. 使用步骤 1 到 8 为集群中的其他 vSphere 主机配置 vmnic。

现在，需要为 vMotion 添加端口组。该组可以创建为虚拟标准交换机 (VSS) 或虚拟分布式交换机 (VDS)。在示例中，我们将创建 VSS 交换机。

1. 选择**配置**选项卡，然后选择**联网**。
2. 对于 vSwitch0，单击**属性...**。
3. 单击**添加...** 以创建“端口组”。
4. 选择 **VMkernel**，然后单击**下一步**。
5. 使用以下信息填写“端口组属性”：
  * **网络标签：**端口组的相应名称。
  * **VLAN 标识（可选）：**用于 vMotion 流量的 VLAN 标识（示例中为 1101）。VLAN 标识将允许 VMware 对特定 VLAN 的流量进行标记。
  * 选择**将此端口组用于 vMotion**。
6. 单击**下一步**。
7. 输入 VLAN 的**可移植 IP 地址**。（可以从 SoftLayer 门户网站的**网络 > IP 管理 > VLAN** 获取端口 IP 地址。选择正确的 VLAN，然后在**子网**下，您将看到可移植 IP 地址范围。如果没有可用的可移植 IP 地址，或者如果已耗尽当前的池，请执行“订购专用子网/IP 地址”部分中的步骤以订购其他可移植 IP 地址。）
8. 单击**下一步**，然后单击**完成**以完成。

使用以下步骤来创建用于 VM 数据流量的端口组。

1. 单击 vSwitch0 的**属性...**，然后选择**添加 > 虚拟机**。
2. 使用以下信息填写**端口组属性**：
  * **网络标签：**输入端口组的名称，例如 VM Data。
  * **VLAN 标识（可选）：**输入 VLAN 标识；示例中我们使用的是 1101。VLAN 标识允许 VMware 对 VLAN 的流量进行标记。

### 可选 - 安装 VMware 附加组件许可证（NSX、vRealize、vSAN 等）

现在，VMware 环境已准备就绪，可以继续部署其他配置、访客 VM 或 VMware 附加组件。还可以通过 IBM Cloud 控制门户网站购买 VMware 附加组件的许可证，然后通过 vCenter 控制台添加这些许可证。有关订购和管理 VMware 附加组件许可证的更多信息，请参阅 [VMware vSphere 6 订购和管理许可证](vmware-vsphere-6-ordering-and-managing-licenses.html)。

## 后续步骤
现在，您具有在 IBM Cloud 数据中心运行的基本单站点 VMware 环境。基本配置只有一个本地数据存储器，这是简化配置，不包含 VMware DRS、HA、存储器 DRS 和防火墙等功能。

有关更多信息，请参阅[常见问题：VMware](vmware-faq.html)。 
