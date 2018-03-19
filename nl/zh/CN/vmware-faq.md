---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 常见问题：VMware 

## 通过 IBM Cloud 门户网站部署 vSphere 时，将启用哪种许可级别？

Enterprise Plus，这是最高 vSphere 许可级别。

## VMware vSphere 6 是如何获得许可的？

许可方法与部署机制相关。有两种方法可部署 VMware 6：

1. 通过控制门户网站部署 vSphere 时，VMware 服务提供者计划许可 (VSPP) 会自动启用。部署时，会将缺省用户“slvmadmin”添加到控制门户网站中用于 vSphere 管理和集成服务的“主机”。

2. 手动部署 vSphere 时，您可以使用自带许可证和介质 (BYOL/BYOM)，这允许您将标准许可证应用于这些主机。**注：**如果要使用您自己的 VMWare 许可，建议您订购使用免费操作系统（例如 CentOS）的服务器，或订购无操作系统的服务器。然后，通过 IPMI [虚拟 ISO](../bare_metal/mount-iso-bare-metal-server.html) 来安装 VMWare 操作系统。

## 可以创建隔离的私有 VMware 云吗？

可以，您可以部署裸机系统并在这些主机上安装任何支持的系统管理程序（包括 VMware ESX）。您还可以使用本机管理工具来部署虚拟机。缺省情况下，系统部署在具有隔离和联网组件（例如，网关、路由器和防火墙）的 VLAN 中，并用于创建几乎任何拓扑。

## VMware 是如何获得许可的？

许可方法与部署机制相关。有两种方法可部署 VMware：

1. 通过门户网站部署 ESX 时，VMware 服务提供者计划许可 (VSPP) 会自动启用。部署时，会将缺省用户“vmadmin”添加到 ESX 服务器以进行数据收集。请勿删除此缺省用户。VSPP 会针对保留并用于所有“打开电源”的虚拟机的 RAM 收费（而不是像标准主机许可证那样“按套接字”收费）。

2. 手动部署 ESX 时，您可以使用自带许可证 (BYOL)，这样您可以将标准许可证应用于这些主机。**注：**BYOL 不能用于通过门户网站部署的主机。VSPP 应该处于启用状态。

    * 此外，无需 vCenter Server 实例即可使 VSPP 生效。

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## 可以直接通过 IBM Cloud 门户网站部署 VMware 组件吗？

可以，您有两个选项：

1. 使用按月计费的裸机系统，自动选择并部署 ESX 系统管理程序<!-- (Figure 2)-->。您还可以使用虚拟机或裸机系统（仅限 Windows）自动部署 vCenter 管理。

2. 部署使用免费操作系统（例如 CentOS）的裸机主机，随后使用远程控制台和该主机的虚拟介质访问权来手动安装 ESX。然后，可以手动安装 vCenter Server 或部署在 Linux 上运行的 VMware vCenter Server Appliance。

