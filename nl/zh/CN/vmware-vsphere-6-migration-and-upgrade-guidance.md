---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  迁移和升级到 VMware vSphere 6

使用 VMware 管理控制面板可快速、轻松地将 VMware 云环境扩展或移动到任何 {{site.data.keyword.BluSoftlayer_full}} 数据中心。要迁移和升级 vSphere 工作负载，请使用以下步骤作为指南。
{:shortdesc}

1. 收集数据。
2. 查看现有体系结构：
  1. 资源利用率（CPU/内存/存储器）。
  2. 跟踪和预测增长率。
  3. 确定即将到来的未来项目。
  4. 确定部署了哪些分配的 VLAN/子网等（在控制门户网站中提供）。
  5. 找到正在用于解决方案的自定义 RFC1918（专用）子网。
3. 查看 VMWare 6 文档并加入 VMWare 社区：
  1. [VMware vSphere 文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [VMware Technology Network ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://communities.vmware.com/welcome){: new_window}
4. 更新管理员团队的培训以支持 VMWare 6。
5. 规划和设计新的体系结构。
6. 选择基于合规性的[数据中心 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window}。与 IBM Cloud 销售部合作，根据产品/服务的可用性来优化您的候选位置。
7. 定义必需的 VLAN 和子网（可移植公共和专用 IP）。
8. 设计 vSphere 服务器：
  1. 查看当前 IBM Cloud 服务器目录。建议将 Intel Xeon V3 服务器与冗余上行链路、冗余电源以及用于本地（引导）磁盘的 RAID-1 一起使用。
  2. 大多数具有 VMWare 的客户都采用 N+1 硬容量上限（所有 VM 都可以轻松地分配给因维护/故障等原因而除去了单个节点的服务器）。
  3. 由于计算的周转时间短，因此许多客户需要更高的“软上限”，约为 80%（即“n”服务器配置上的 80% 容量），而更标准的软上限为 60-75%。
  4. 可能需要外部供应商为 vSphere 访客提供外部操作系统许可（例如，Microsoft 和 Red Hat）。
  5. 查看 [Performance Best Practices for VMware vSphere 6.0 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window}。
9. 设计 vCenter Server：
  1. 通常，中型虚拟服务器实例 (VSI) 是小型环境（8 个 vCPU + 16 GB RAM）的入口点，而裸机用于更大型的环境。
  2. vCenter 可以作为操作系统附加组件或作为设备部署在独立的 VSI Windows 虚拟机上。
    1. 参考资料链接：
        * [vCenter Server 6.0 requirements for installation ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://kb.vmware.com/s/article/2107948){: new_window}
        * [VMware vCenter Server Performance and Best Practices ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}
        * [使用 VMware vSphere 6 部署和配置 vCenter Server Appliance (vCSA)](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. 非 VMWare 服务器：确定可能需要的任何非 VMWare 服务器（虚拟或裸机）并进行相应规划。
11. 存储器：
  1. 为环境制定存储计划。一开始使用具有用于虚拟化的快照空间的耐久性 2 IOPS/GB 是不错的存储计划，但如果使用了虚拟数据库或其他高性能应用程序，那么 4 IOPS/GB 层会更适合。通常建议使用 NFS 存储器。  
  2. 可以在[可用于 VMware 系统的存储器](select-storage-option-use-vmware.html)中找到选择矩阵。
  3. 快照空间最常用作时间点复原的辅助度量。一开始最好使用 10%，因为该过程非常高效，并且可以轻松向上调整大小。
12. 备份：
  1. 确保现有备份策略有效。如果备份策略不存在，应该进行创建。
  2. 您可以使用自己的备份解决方案。可以使用 vSphere Enterprise Plus 许可随附的备份功能、优化的第三方解决方案（例如 VEEAM）或传统 IBM Cloud R1Soft 备份。
13. 制定迁移策略：
  1. 查看 [Best practices to install or upgrade to ESXi 6.0 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://kb.vmware.com/s/article/2109712){: new_window}。
  2. 查看现有 DNS 和/或 IP 配置，并根据需要缩短 TTL。
  3. 为 VM 制定计划，以包含源主机、目标主机、源 IP、目标 IP 以及关联的 DNS 条目。
  4. 在大多数方案下，最好是逐个 VM 进行迁移，然后更新公用和专用网络配置。从旧版本移至较新版本时，通常最好通过将 VM 关闭，并在环境之间执行_拆离/连接_，从而简单地“拆除并处置”VM。如果要在不同位置之间移动，那么可以使用远距离 vMotion。
  5. 制定测试计划以验证环境。
  6. 与用户协调更改/维护时段。各个 VM 维护时段可以说明传输数据、配置 VM、更改和传播 DNS 的时间以及故障诊断的时间。
14. 部署新环境：
  1. [VMware vSphere 6 入门](vmware-vsphere-6-getting-started.html)。
  2. 订购新的 vSphere 服务器和 vCenter Server（以及您需要的其他任何服务器）。
      **注：**请确保选择正确的“未结合的”网络上行链路。
  3. 订购并配置相应的存储器：[使用 VMware 的 IBM File Storage for IBM Cloud 的体系结构指南](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html)
  4. 订购新的 VLAN 和可移植子网（可能需要详细体系结构图和调整）。
  5. 配置 vCenter 以与 vSphere 服务器通信并配置环境。
  6. 在实时环境中执行备份。
  7. 运行迁移计划和关联的测试计划。
  8. 在新环境中实施备份。
  9. 运行新环境。
  10. 使旧环境退役。
