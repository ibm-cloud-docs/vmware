---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 訂購 VMware 授權

透過部署至 {{site.data.keyword.BluSoftlayer_full}}，VMware 管理者瞭解他們可以快速實現符合成本效益的混合式雲端特徵。其中一個特徵是將 vSphere 工作負載及型錄佈建至 {{site.data.keyword.cloud_notm}} 資料中心內的 VMware vSphere 環境，而不需要修改 VMware VM 或訪客。使用一般 vSphere Hypervisor 及管理/編排平台即可進行這些部署。
{:shortdesc}

vSphere 實作也允許使用其他元件。表 1 包含可透過 {{site.data.keyword.slportal}} 訂購的 VMware 產品清單。您可以在 [IBM Cloud for VMware 解決方案](http://www.softlayer.com/vmware-solutions)下找到定價資訊。

|產品名稱|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard 第 1 層 (0 - 20 TB)|
|Virtual SAN Standard 第 2 層 (21 - 64 TB)|
|Virtual SAN Standard 第 3 層 (65 - 124 TB)|
|VMware Site Recovery Manager (SRM)|
{: caption="表 1. 客戶入口網站中可用的 VMware 產品" caption-side="top"}

請使用下列步驟來訂購表 1 中所列出之 VMware 產品的授權：
1. 登入 [{{site.data.keyword.slportal_short}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window}。
2. 按一下**裝置 > 受管理 > VMware 授權**。
3. 按一下右上角的**訂購 VMware 授權**。
4. 按一下**新增授權...** 下的下拉清單，以列出您要訂購之授權的 VMware 產品及 CPU 數目。
  * **附註：**VMware vSphere Enterprise Plus (ESXi 6.0) 不是透過此處理程序訂購。當您訂購裸機伺服器時，它將作為所要求的 OS 進行訂購。
5. 您可以在畫面最右側看到所選取 VMware 產品的價格。
6. 按一下**繼續**以訂購授權，或按一下**新增授權**以新增其他授權。
  * 按一下**繼續**之後，您會回到 **VMware 授權**頁面，該頁面顯示您的 VMware 產品及授權碼。
7. 從提供的鏈結中下載**安裝檔案**。您需要具有與 IBM Cloud 專用網路連接的 SSL 連線，才能存取下載頁面。
8. 下載正確的 VMware 產品，然後手動將它們安裝至 vSphere 環境。
