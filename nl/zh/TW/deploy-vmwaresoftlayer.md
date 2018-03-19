---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 使用錦囊妙計來進行 VMware 部署

透過部署至 {{site.data.keyword.BluSoftlayer_full}} 企業級全球雲端，VMware 管理者即可快速實現符合成本效益的混合式雲端特徵。vSphere 工作負載及型錄可以佈建至 {{site.data.keyword.cloud_notm}} 資料中心內的 VMware vSphere 環境，而不需要修改 VMware VM 或訪客。這些部署可以使用一般 vSphere Hypervisor 及管理/編排平台進行。vSphere 實作也可以運用 VMware vCloud Suite 的其他元件 - vCloud Automation Center、vCenter Operations Management Suite、vSAN、vCloud Network & Security、Site Recovery Manager、vCenter Orchestrator 及 NSX。

VMware 錦囊妙計系列的核心目標是協助 vSphere 管理者在 IBM Cloud 基礎架構內部署 VMware vSphere 環境。此錦囊妙計不是用來訓練如何管理 vSphere。如需管理 vSphere 的相關資訊，請參閱 [VMware Education ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}。

{{site.data.keyword.cloud_notm}} 具有數個特定功能，可讓 VMware 管理者彈性利用自助方式使用裸機實例及網路、儲存空間以及備份及回復建構。然後，您可以使用這些建構來部署完整功能的 vSphere 實作，而這些實作可以建置成延伸或取代內部部署 vSphere 實作 (VMware@Home)。

下列錦囊妙計可供管理者使用：

* [建置單一網站 VMware 環境](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html)：作為 vSphere 管理者，您將逐步執行環境建置步驟（包括使用 Endurance 或 Performance Block Storage 或是 QuantaStor）。
* [移轉 vSphere 工作負載 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window}：在 IBM Cloud 資料中心內部署 vSphere 實作之後，即會呈現情境以協助您將工作負載 [虛擬機器 (VM)] 移轉至 VMware。
* [運用 NSX® ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window}：您可以運用 VMware NSX，將軟體定義網路 (SDN) 建構提供給 VMware@SoftLayer 部署。
* [Catalogic ECX ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window}：您可以在混合式 IT 基礎架構中管理及分析 CopyData。使用 Catalogic Software 智慧型 Copy Data 管理平台、ECX，以及使用 NetApp Private Storage 和 VMware vSphere 基礎架構，將此基礎架構部署至 IBM Cloud 基礎架構。
* [VMware 備份 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window}：此錦囊妙計說明可備份、回復及保存 VMware 部署中所執行之 VMware 型工作負載 (VM) 的替代方法。
* [VMware 災難回復 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window}：此錦囊妙計詳述使用 VMware 建立災難回復 (DR) 解決方案的兩個使用案例。第一個會與內部部署 VMware 環境配對，而此環境容許回復內部部署工作負載（反之亦然）。第二個則會回復第二個 {{site.data.keyword.cloud_notm}} 資料中心內的 VMware 工作負載。
* [VMware 的 Vormetric 加密 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window}：使用案例說明 Vormetric 如何透過加密 VM 資料來保護 VMware 工作負載。
* [使用 IBM、VMware 及 HyTrust 部署信任雲端解決方案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window}：您可以整合各種架構元素，以透過 Hypervisor 及管理應用程式從硬體建立信任鏈。


**附註：**這些錦囊妙計是為經驗豐富的 vSphere 管理者所設計的。涵蓋的一些主題，考量讀者具有安裝及配置 vSphere 與 vCenter 的基本部署技能。
