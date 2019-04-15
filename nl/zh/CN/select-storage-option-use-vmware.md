---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 要用于 VMware 系统的存储器
{: #vmware-storage}

您有多个存储器选项。通过这些选项，可以选择专用存储器、共享存储器或自带存储器的解决方案。使用以下信息可帮助您确定哪种存储器解决方案最适合您的工作负载。

表 1 包含存储层以及您的工作负载可能所属的层。
<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 1. 存储层</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>第 1 层</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>第 2 层</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>第 3 层</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>商业用途</strong></p>
			</td>
			<td style="width:160px;">
				<p>高性能和/或高可用性生产应用程序、数据库和数据</p>
			</td>
			<td style="width:160px;">
				<p>非任务关键型测试和开发应用程序、数据库和数据</p>
			</td>
			<td style="width:160px;">
				<p>非任务关键型数据存储、备份和归档</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>性能</strong></p>
			</td>
			<td style="width:160px;">
				<p>高（SSD 和 SAS）</p>
			</td>
			<td style="width:160px;">
				<p>中 (SAS 和 SATA)</p>
			</td>
			<td style="width:160px;">
				<p>低 (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>保证 IOPS</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>高可用性 (HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>复制</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>快照</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
	</tbody>
</table>


## VMware 专用和共享存储器选项

您可以从多个存储器选项中进行选择。对于专用存储器，可以选择本地磁盘选项：VSAN 或 QuantaStor。对于共享存储器，可选择“耐久性”或“高性能”存储器。如果您决定使用自带存储器，那么有若干“专用”选项，包括 NetApp OnTap Edge、NetApp Private Storage (NPS)、{{site.data.keyword.IBM}} Spectrum Accelerate 和软件定义的存储器。表 2 和表 3 提供了各选项的并排比较以方便您参考。

## 专用存储器选项

对于连接到单租户环境中 VMware 的存储器，有多个选项： 

* 本地
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## 本地存储器

在 IBM Cloud 客户门户网站中通过 ESX 订购{{site.data.keyword.baremetal_short}}，并选择所需的磁盘 [SATA、串行连接的 SCSI (SA SCSI) 或 SSD]。
 
您可以使用自带 ESX 许可证，但需要向支持人员开具凭单以向其通知这一更改。

* 建议的工作负载：第 3 层
* 性能：受限：取决于 RAID 和磁盘类型。使用 SSD 会使成本增加，但可提高性能。
* 可扩展性：受机箱中驱动器插槽数的限制
* 协议：不适用
* 成本：资本支出 (CAPEX) 和运营支出 (OPEX) 低
* HA：不可用
* 复制：[vSphere Replication 虚拟设备 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* 可靠性：多个单点故障



## vSAN [1]

* 建议的工作负载：第 1 层
* 性能：每个主机超过 90,000 IOPS，具体取决于主机配置
* 可扩展性：V5.5 虚拟机磁盘 (VMDK) 最大 2 TB；V6.0 VMDK 最大 62 TB。可通过更多节点向外扩展。
* 协议：专有
* 成本：CAPEX 和 OPEX 中等
* HA：同时支持主机故障和磁盘故障。从 VMware V6 开始，支持故障域。
* 复制：[vSphere Replication 虚拟设备 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* 复制和灾难恢复：
    1. 通过 VMware vCenter Server 安排 VM 备份
    2. 创建 VM 快照
    3. 为 VM 创建数据 DE
    4. 复原 VM
 * 可靠性：对于 7 个或更多主机，最多容许其中 3 个主机故障。在 VMware V6 中引入了故障域。   

[1] vSan 6.2 的新功能“延伸集群”允许主机位于同一数据中心的不同 pod 中（验证测试正在进行中）。<!-- Should this in progress mention be removed? -->

vSAN 5.5 仅可以使用 BYOL（自带许可证）。仅当使用 Avago LSI MegaRAID SAS 9361-8i 磁盘控制器时，才受 VMware 支持。

vSAN 6.0 直接通过 IBM Cloud 门户网站提供，并基于 CPU 许可证计费。

## QuantaStor

[OSNexus Solution Design Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} 可用于帮助将 VMware 与 QuantaStor 进行连接。

* 建议的工作负载：第 2 层和第 3 层 
* 性能：根据驱动器数、RAID 和使用的磁盘（iSCSI 或 NFS）而有所不同  
* 可扩展性：V3 单机架支持 128 TB；无向上或向外扩展。 
* 协议：iSCSI、NFS 和 SMB 
* 成本：CAPEX 和 OPEX 高 
* HA：不可用  
* 复制：内置复制功能；无 SRA 可用。还可以使用 vSphere Replication 设备 
* 可靠性：机柜和 RAID 控制器单点故障。


<a name="NetApp"></a>
## NetApp Data OnTap Edge

您必须向 NetApp 或 IBM 购买 NetApp 设备。您需要将其安装在 {{site.data.keyword.BluSoftlayer}} 数据中心的{{site.data.keyword.baremetal_short}}上。

有关将 VMware 与 NetApp 相连接的更多信息，请参阅以下链接：
* [NetApp ONTAP Select ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: Build a data center on a server with NetApp fundamentals ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* 建议的工作负载：第 2 层和第 3 层
* 性能：根据驱动器数和 RAID 而有所不同
* 可扩展性：支持 110 TB；无向外扩展。
* 协议：iSCSI、NFS 和 SMB
* 成本：CAPEX 和 OPEX 中等
* HA：不可用
* 复制：支持 SnapMirror；还可使用 [vRealize Automation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.vmware.com/products/vrealize-automation){: new_window} (vRA) 来实现。
* 可靠性：机柜和 RAID 控制器单点故障。

<a name="NPS"></a>
## NetApp 专用存储器

您必须向 NetApp 或 IBM 购买 NetApp 设备。您需要将其安装在 IBM Cloud 数据中心附近的其中一个主机托管站点中，并使用“直接链接主机托管”或“直接链接云”进行连接。

有关将 VMware 与 NetApp 相连接的更多信息，请参阅以下链接： 
* [NetApp Private Storage for IBM Cloud ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Solution brief: NetApp Private Storage for IBM Cloud ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* 建议的工作负载：第 1 层
* 性能：取决于 NetApp 型号
* 可扩展性：支持添加驱动器和机架来提高容量和 IOPS
* 协议：iSCSI、NFS 和 SMB
* 成本：CAPEX 和 OPEX 高
* HA：双头和控制器
* 复制：支持 SnapVault 和 SnapMirror；还可使用 [vRealize Automation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.vmware.com/products/vrealize-automation) 来实现。
* 可靠性：高冗余和支持 MPIO

<a name="IBM"></a>
## IBM Spectrum Accelerate

IBM Spectrum Accelerate 专用存储器选项在 IBM Cloud 客户门户网站上不可用。<!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* 建议的工作负载：第 1 层
* 性能：取决于磁盘数、SSD（可选）以及为每个“节点”VM 提供的内存量。
* 可扩展性：可扩展约 8 - 325 TB 可用容量
  * 最小容量：3 个 VM x 6 个驱动器
  * 最大容量：15 个 VM x 12 个驱动器
  * 通过 IBM Hyper-Scale Manager，最多可扩展到 144 个虚拟阵列，可用容量超过 40 PB
  * 通过添加更多节点实现非中断性容量扩展
  * 支持每个节点 1 个 500 或 800 GB SSD
* 协议：仅限 iSCSI
* 成本：取决于为节点部署的定价模型和物理计算机。CAPEX 高；OPEX 中到低，具体取决于许可内容。
  * 按二进制 (TiB) 可用容量定价
  * 与任何特定的硬件配置都无关。示例：200 TiB 许可证可以通过多种方法进行部署 - 一个 200 TiB 实例，两个 100 TiB 实例或四个 50 TiB 实例
  * 提供了两种方式：永久许可证 [含 1 年预订和服务 (S&S)] 和每月许可证（含 S&S）
* HA：集群解决方案
* 复制：使用 [vRealize Automation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.vmware.com/products/vrealize-automation){: new_window} 或 SRA（可用于通过 VMware 的 Site Recovery Manager (SRM) 从物理 IBM XIV 进行复制）来实现
  * [vSphere Replication ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [VMware vCenter Site Recovery Manager version 5.x guidelines for IBM XIV Gen3 Storage System ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* 可靠性：高冗余和支持 MPIO。任何可用节点都可以管理集群。目前，使用基于硬件的 IBM XIV 时，IBM Spectrum Accelerate 不支持以下功能：
  * 三站点镜像
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG V6
  * 6 TB 磁盘驱动器
  * 存储管理初始规范 (SMI-S) 1.6
  * 静态数据加密
  * vStorage for API Array Integration (VAAI) 许可现在与 Virtual Volumes (VVol) 一致
  * vCenter Operations Manager (VCop)
  * 有关 IBM XIV Storage System 的更多信息，请参阅 [Platform and application integration for IBM XIV Storage System ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}

## 共享存储器选项

有两个存储器选项可用于连接到多租户环境中的 VMware：块存储器和文件存储器。

### 块存储器和文件存储器

在 IBM Cloud 客户门户网站中通过 ESX 订购{{site.data.keyword.baremetal_short}}。

在 VMware 中的<!--**Authorize** (**Block** or **File**) **Storage SoftLayer** -->**主机设备详细信息存储器**选项卡上，提供了三个预定义的值 - 用户名、密码（用于 CHAP 认证）和主机 IQN。

有关供应块存储器的更多信息，请参阅[供应和管理块存储器](/docs/infrastructure/BlockStorage/provisioning-block_storage.html)。

有关供应文件存储器的更多信息，请参阅[供应和管理 IBM Cloud 的 IBM 文件存储器](/docs/infrastructure/FileStorage/provisioning-file-storage.html)。

* 建议的工作负载：第 1 层、第 2 层和第 3 层
* 供应性能的两种方法：
    1. 耐久性 IOPS 层：可用项为 0.25、2、4 或 104 IOPS/GB
    2. 高性能分配的 IOPS：指定独立于容量的 IOPS。建议用于明确定义性能需求的工作负载。
    * 可预测的存储器性能参数
    * 可以对多个卷一起进行条带分割，以实现更高的 IOPS 和更大吞吐量
* 等待时间少于 10 毫秒，最高可达 48,000 IOPS
* 可扩展性：订购范围从 20 GB 到 12 TB。订购卷后，即无法再调整该卷的大小。
* 协议：iSCSI 和 NFS
* 成本：CAPEX（对于同样大小的 SAN，CAPEX 将增加 10 倍）和 OPEX 高
* HA：双头和控制器
* 复制：快照和复制通过 IBM Cloud 专用网络提供；还可使用 [vRealize Automation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.vmware.com/products/vrealize-automation){: new_window} 来实现，但没有 SRA。
* 可靠性：高冗余；iSCSI 使用 MPIO 连接；基于 NFS 的存储器通过 TCP/IP 连接进行路由。快照和复制已启用。

表 2 提供单租户环境中专用存储器的优缺点。

<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 2. VMware 专用存储器选项的优缺点</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; 专用存储器（单租户）</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>关键因素/存储器选项</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>本地</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>虚拟 SAN</p>
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
				<p><strong>类型</strong></p>
			</td>
			<td style="width:87px;">
				<p>本地</p>
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
				<p>整体</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>性能</strong></p>
			</td>
			<td style="width:87px;">
				<p>基于 SSD/SA-SCSI 规范；可以进一步使用 RAID 5/10 以实现读/写性能增益。</p>
			</td>
			<td style="width:95px;">
				<p>每个主机超过 90,000 IOPS，具体取决于主机配置。每个主机 100 个 VM，每个集群 32 个主机，每个集群 3,200 个 VM，仅 2,048 个受保护 (V5.5)</p>
				<p>最多 20,000 IOPS，每个主机 200 个 VM，每个集群 64 个主机，每个集群有 6,000 个受保护 VM (V6.0)。</p>
			</td>
			<td style="width:99px;">
				<p>基于所选磁盘的类型和数量，以及 RAID 配置和使用的是 iSCSI 还是 NFS。</p>
			</td>
			<td style="width:80px;">
				<p>基于所选磁盘的类型和数量以及 RAID 配置操作。</p>
			</td>
			<td style="width:80px;">
				<p>取决于型号。</p>
			</td>
			<td style="width:96px;">
				<p>基于所选磁盘的类型和数量，以及 RAID 配置和每个系统管理程序节点对 SSD 磁盘的可选使用。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可扩展性</strong></p>
			</td>
			<td style="width:87px;">
				<p>大小和磁盘 I/O 吞吐量的增长受到限制。</p>
			</td>
			<td style="width:95px;">
				<p>虚拟机磁盘 (VMDK) 最高 2 TB (V5.5) 和最高 62 TB (V6.0)。</p>
				<p>可通过更多节点向外扩展。</p>
			</td>
			<td style="width:99px;">
				<p>单个 QS 最高 128 TB (3.x)。无向上或向外扩展。</p>
			</td>
			<td style="width:80px;">
				<p>最高 10 TB；无向外扩展。</p>
			</td>
			<td style="width:80px;">
				<p>是，添加磁盘架可扩展容量和 IOPS。</p>
			</td>
			<td style="width:96px;">
				<p>可用空间可从约 8 TB 扩展到 325 TB。</p>
				<p>最小容量为 3 个 VM x 6 个驱动器。</p>
				<p>最大容量为 15 个 VM x 12 个驱动器。</p>
				<p>通过 IBM Hyper-Scale Manager，最多可扩展到 144 个虚拟阵列，可用容量超过 40 PB。</p>
				<p>通过添加更多节点实现非中断性容量扩展。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>协议</strong></p>
			</td>
			<td style="width:87px;">
				<p>不适用</p>
			</td>
			<td style="width:95px;">
				<p>专有</p>
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
				<p><strong>用例</strong></p>
			</td>
			<td style="width:87px;">
				<p>第 2 层和第 3 层工作负载</p>
			</td>
			<td style="width:95px;">
				<p>第 1 层工作负载</p>
			</td>
			<td style="width:99px;">
				<p>第 2 层和第 3 层工作负载</p>
			</td>
			<td style="width:80px;">
				<p>第 2 层和第 3 层工作负载</p>
			</td>
			<td style="width:80px;">
				<p>第 1 层工作负载</p>
			</td>
			<td style="width:96px;">
				<p>第 1 层工作负载</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>高可用性 (HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>通过 RAID 提供</p>
			</td>
			<td style="width:95px;">
				<p>是；主机和磁盘故障；故障域 (V6.0)</p>
			</td>
			<td style="width:99px;">
				<p>在 IBM Cloud 中不可用。</p>
			</td>
			<td style="width:80px;">
				<p>不适用</p>
			</td>
			<td style="width:80px;">
				<p>是；双头和控制器。</p>
			</td>
			<td style="width:96px;">
				<p>是；集群解决方案。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可配置性</strong></p>
			</td>
			<td style="width:87px;">
				<p>磁盘的数量和类型；RAID 级别</p>
			</td>
			<td style="width:95px;">
				<p>需要特定控制器。</p>
			</td>
			<td style="width:99px;">
				<p>CPU、内存、高速缓存、磁盘的数量和类型以及 RAID 级别。</p>
			</td>
			<td style="width:80px;">
				<p>CPU、内存、高速缓存、磁盘的数量和类型以及 RAID 级别。</p>
			</td>
			<td style="width:80px;">
				<p>待定</p>
			</td>
			<td style="width:96px;">
				<p>CPU、内存、高速缓存、磁盘的数量和类型、SSD、缓存以及 iSCSI 端口配置。多租户 QOS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>灾难恢复和复制</strong></p>
			</td>
			<td style="width:87px;">
				<p>使用 vRA 进行复制；无 SRA。</p>
			</td>
			<td style="width:95px;">
				<p>使用 vRA 进行复制。</p>
			</td>
			<td style="width:99px;">
				<p>内置复制功能；无 SRAs 可用。</p>
			</td>
			<td style="width:80px;">
				<p>可使用 vRA 进行复制，SnapMirror。</p>
			</td>
			<td style="width:80px;">
				<p>可使用 vRA 进行复制，SnapMirror，SnapVault。</p>
			</td>
			<td style="width:96px;">
				<p>支持 vRA 或 SRA；在 SDS 和/或物理 XIV 设备之间进行复制。</p>
				<p>支持快照；通过 IBM FlashCopy Manager 恢复应用程序。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可靠性</strong></p>
			</td>
			<td style="width:87px;">
				<p>没有 HA 的情况下的单点故障。</p>
			</td>
			<td style="width:95px;">
				<p>对于 7 个以上的主机，最多容许其中 3 个主机故障。</p>
				<p>在 V6.0 中引入了故障域。</p>
			</td>
			<td style="width:99px;">
				<p>单点故障（机柜和 RAID 控制器），无 HA。</p>
			</td>
			<td style="width:80px;">
				<p>单点故障（机柜和 RAID 控制器），无 HA。</p>
			</td>
			<td style="width:80px;">
				<p>高冗余多路径 I/O (MPIO) 连接。</p>
			</td>
			<td style="width:96px;">
				<p>高冗余 iSCSI MPIO 连接：任何节点都可以管理集群。</p>
			</td>
		</tr>
	</tbody>
</table>

表 2 文档链接：
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge：在客户门户网站上不可用 - 请使用自带解决方案。
  * [Data ONTAP Installation and Administration Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP Express Setup Guide ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate：在客户门户网站上不可用 - 请使用自带解决方案。
  * [Working with an IBM Spectrum Accelerate system ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

表 3 提供多租户环境中共享存储器的优缺点。

<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 3. VMware 共享存储器选项的优缺点</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>VMware 共享存储器（多租户）</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>关键因素/存储器选项</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">耐久性块存储器和文件存储器</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">高性能块存储器和文件存储器</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>类型</strong></p>
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
				<p><strong>性能</strong></p>
			</td>
			<td style="width:266px;">
				<p>可用项为 0.25、2、4 或 104 IOPS/GB。</p>
				<p>可预测的存储器性能参数。</p>
				<p>可以对多个卷一起进行条带分割，以实现更高的 IOPS 和更大吞吐量。</p>
			</td>
			<td style="width:271px;">
				<p>客户机根据工作负载需求或价格点，供应所需性能级别。</p>
				<p>&nbsp;</p>
				<p>可预测的存储器性能参数。</p>
				<p>可以对多个卷一起进行条带分割，以实现更高的 IOPS 和更大吞吐量。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可扩展性</strong></p>
			</td>
			<td style="width:266px;">
				<p>卷大小的范围从 20 GB 到 12 TB。订购后即无法调整大小。</p>
			</td>
			<td style="width:271px;">
				<p>卷大小的范围从 20 GB 到 12 TB。订购后即无法调整大小。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>协议</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI 和 NFS。</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI 和 NFS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>主机连接</strong></p>
			</td>
			<td style="width:266px;">
				<p>对于 iSCSI，最多 8 个；对于 NFS，最多 64 个。</p>
			</td>
			<td style="width:271px;">
				<p>对于 iSCSI，最多 8 个；对于 NFS，最多 64 个。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>用例</strong></p>
			</td>
			<td style="width:266px;">
				<p>第 1 层、第 2 层和第 3 层工作负载：</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 0.25 IOPS/GB：I/O 强度低。示例应用包括存储邮箱或部门级文件共享。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 2 IOPS/GB：一般用途。示例应用包括托管支持 Web 应用程序的小型数据库或用于系统管理程序的虚拟机磁盘映像。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 4 IOPS/GB：I/O 强度高。示例应用包括事务型数据库和其他性能敏感型数据库。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 10 IOPS/GB：I/O 强度高。示例应用包括分析。</p>
			</td>
			<td style="width:271px;">
				<p>第 1 层、第 2 层和第 3 层工作负载：</p>
				<p>基于 MPIO iSCSI 的存储器，非常适合需要可预测性能级别的 I/O 密集型应用程序（例如，关系数据库）。存储卷的大小为 20 GB 到 12 TB，用户可选择的 IOPS 范围为 100 到 48,000 IOPS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>HA</strong></p>
			</td>
			<td style="width:266px;">
				<p>是，双头和控制器。</p>
			</td>
			<td style="width:271px;">
				<p>是，双头和控制器。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可配置性</strong></p>
			</td>
			<td style="width:266px;">
				<p>仅限大小和 IOPS。</p>
			</td>
			<td style="width:271px;">
				<p>仅限大小和 IOPS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>灾难恢复和复制</strong></p>
			</td>
			<td style="width:266px;">
				<p>提供快照和复制，通过 IBM Cloud 专用网络来执行。可以使用 vRA 在 VM 级别进行复制；无 SRA。</p>
			</td>
			<td style="width:271px;">
				<p>提供快照和复制，通过 IBM Cloud 专用网络来执行。可以使用 vRA 在 VM 级别进行复制；无 SRA。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可靠性</strong></p>
			</td>
			<td style="width:266px;">
				<p>高冗余，MPIO 连接，通过 TCP/IP 连接路由的基于 NFS 的文件存储器。快照和复制已启用。</p>
			</td>
			<td style="width:271px;">
				<p>高冗余，MPIO 连接，通过 TCP/IP 连接路由的基于 NFS 的文件存储器。</p>
			</td>
		</tr>
	</tbody>
</table>

表 3 文档链接：
* [块存储器](/docs/infrastructure/BlockStorage/index.html)
* [文件存储器](/docs/infrastructure/FileStorage/index.html)
