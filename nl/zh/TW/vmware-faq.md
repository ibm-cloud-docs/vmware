---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 常見問題：VMware 

## 從 IBM Cloud 入口網站部署 vSphere 時，啟用了哪些授權層次？

Enterprise Plus，最高的 vSphere 授權層次。

## VMware vSphere 6 的授權方式為何？

授權方式與部署機制相關。您有兩種方法可部署 VMware 6：

1. 從控制入口網站部署 vSphere 時，會自動啟用 VMware Service Provider Program 授權 (VSPP)。部署時，會將預設使用者 "slvmadmin" 新增至控制入口網站中的 Host for vSphere 管理及整合服務。

2. 手動部署 vSphere 時，您可以自帶授權及媒體 (BYOL/BYOM)，以容許您將標準授權套用至這些主機。**附註：**如果您要使用自己的 VMWare 授權，則建議使用免費的 OS（例如 CentOS）或作為「無 OS」來訂購伺服器。然後，透過 IPMI [虛擬 ISO](../bare_metal/mount-iso-bare-metal-server.html) 安裝 VMWare OS

## 我可以建立隔離的專用 VMware 雲端嗎？

是，您可以部署裸機系統，並在這些主機上安裝任何支援的 Hypervisor（包括 VMware ESX）。您也可以使用原生管理工具來部署虛擬機器。依預設，系統是針對隔離及網路元件（例如閘道、路由器及防火牆）而部署在 VLAN 中，並且可用來建立幾乎所有拓蹼。

## VMware 的授權方式為何？

授權方式與部署機制相關。您有兩種方法可部署 VMware：

1. 從入口網站部署 ESX 時，會自動啟用 VMware Service Provider Program 授權 (VSPP)。部署時，會將預設使用者 'vmadmin' 新增至 ESX 伺服器，以進行資料收集。請不要刪除此預設使用者。VSPP 會收取保留並用於所有「已開啟電源」虛擬機器（而非「每個 Socket」，如標準主機授權）之 RAM 的費用。

2. 手動部署 ESX 時，您可以 BYOL（自帶授權），因此可以將標準授權套用至這些主機。**附註：**BYOL 無法用於透過入口網站所部署的主機。預期要啟用 VSPP。

    * 此外，不需要 vCenter Server 實例，VSPP 就可以運作。

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## 我可以直接從 IBM Cloud 入口網站部署 VMware 元件嗎？

是，您有兩個選項：

1. 使用每月裸機系統，以自動選取及部署 ESX Hypervisor<!-- (Figure 2)-->。您也可以使用虛擬機器或裸機系統（僅限 Windows），自動部署 vCenter 管理。

2. 使用免費作業系統（例如 CentOS）部署裸機主機，然後使用主機的「遠端主控台」及虛擬媒體存取來手動安裝 ESX。您接著可以手動安裝 vCenter Server，或部署在 Linux 上運作的 VMware vCenter Server Appliance。

