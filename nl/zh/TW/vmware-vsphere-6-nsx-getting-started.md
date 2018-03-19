---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 VMware vSphere 6 NSX 

NSX 會部署為您要套用至基礎架構的授權。{{site.data.keyword.BluSoftlayer_full}} 根據每個處理器來提供授權（定價不會因每個 CPU 的核心數目而變更）。在使用 NSX 元件（「管理」、「控制項」或「資料平面」）的每部伺服器上，都需要 NSX 授權。NSX 會將額外的網路功能新增至平台。您可以針對跨提供者或內部部署專用雲端中範圍的系統安全、承租戶分段及混合式雲端環境，建立健全的覆蓋網路。
{:shortdesc}

您可以透過 RESTful API，將防火牆、負載平衡、VPN、NAT 服務、VXLAN 型微型分段新增至支援自動化的環境。

## 新增授權
使用下列處理程序，將授權新增至伺服器：
1. 使用 vSphere Client 登入 vCenter Server。
* 按一下**管理**下的**授權**。
* 按一下**解決方案**。
* 在產品清單中，按一下 **VMware NSX for vSphere**。
* 按一下**授權碼**或**輸入新的授權碼**。
* 按一下**確定**。

## 安裝 NSX

1. 部署 NSX Manager。
* 向 vCenter Server 登錄 NSX Manager。
* vSphere Web Client 會透過 NSX Manager 部署「NSX 控制器」實例。
* 使用 NSX Manager 在叢集的主機上安裝 VIB，以準備「vSphere 主機」。
* 在所有適用的「主機」上部署「NSX 控制器」之後，請定義並配置「NSX 元件」（例如「Edge 閘道」、「負載平衡器」及「防火牆」）。

## 部署考量

除了標準運算節點之外，啟用解決方案的 NSX 還需要使用額外的 vSphere 節點。

**NSX Manager**<br />
「管理叢集」上的 IBM Informix Virtual Appliance 與 vCenter 具有 1:1 關係。建議使用一般 HA vSphere 特性。NSX Manager 包含已排定/隨選備份功能，而且需要與 vCenter、控制器、NSX Edge 資源及 ESXi 主機的 IP 連線。NSX Manager 會部署至與 vCenter 相同的子網路/VLAN，但並非絕對必要。一般的 VM 大小如下：

|NSX 版本|vCPU|記憶體|OS 磁碟|
|---|---|---|---|
|6.2 Small|4|12 GB|60 GB|
|6.2 Default|4|16 GB|60 GB|
|6.2 Large Scale|4|24 GB|60 GB|
{: caption="表 1. NSX Manager 一般 VM 大小" caption-side="top"}

**NSX 控制器節點**<br />
「NSX 控制器節點」會從 NSX Manager 使用者介面部署為虛擬應用裝置。每一個應用裝置都會透過特殊 IP 位址進行通訊，而這些 IP 位址通常位在與 NSX Manager 相同的子網路內，但不是硬性需求。建議至少將三個控制器 VM 部署至至少三個個別的實體 vSphere 節點。這些節點為主動-主動-主動，其具有 NSX Manager 所定義的工作說明。如果節點失敗，則會發生「大多數規則」失效接手，以將工作負載重新配送至其餘的控制器。NSX 本身並不會強制執行此設計實務。您可以使用原生 vSphere 反親緣性規則，以避免在相同的 ESXi 伺服器上部署多個控制器節點。每個 VM 的一般 VM 大小如下：

|控制器 VM|vCPU|保留|記憶體|OS 磁碟|
|---|---|---|---|---|
|3|4|2048 Mhz|4 GB|20 GB|
{: caption="表 2. NSX 控制器一般 VM 大小" caption-side="top"}

**NSX Switch**
會將已升級的 Virtual Distributed Switch (VDS) 部署至所有主機，以實作分散式功能。

**NSX Edge Services 閘道**<br />
在環境中，視需要部署為多功能 VM 應用裝置。針對「僅限遞送」，最多可以部署八個閘道的作用中叢集。針對任何/所有其他服務，則會將它部署至主動-待命部署。VM 環境的外部通訊需要 IBM Cloud 指派可攜式 IP，以包括任何 NAT 儲存區、VIP 及 VPN 端點。

|閘道表單|vCPU|記憶體|特定用法|
|---|---|---|---|
|X-Large|6|8 GB|適用於 L7 高效能 LB|
|Quad-Large|4|1 GB|適用於高效能 ECMP 及 FW 部署|
|Large|2|1 GB|小型 DC 及單一服務|
|Compact|1|512 MB|小型部署或單一服務使用或 PoC|
{: caption="表 3. NSX Edge 服務" caption-side="top"}

