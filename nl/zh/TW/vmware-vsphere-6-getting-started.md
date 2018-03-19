---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 VMware vSphere 6 

使用下列指令來開始使用 vSphere 6。

## 瞭解環境及配置

若要最佳化 VMware 解決方案，建議您將「專用網路 VLAN」及「公用」（如果不需要，則可以選擇性地停用「公用埠」）用於 VMware vSphere 環境。此佈建設定檔容許下列第 2 層區段傳輸界限：

|範例 VLAN ID|說明|類型|其他詳細資料|
|---|---|---|---|
|VLAN1 - **1101**|管理、VxLAN|專用 BCR|訂購時在其中部署「VMWare 主機」的原生無標籤 VLAN、原始原生 VLAN|
|VLAN4 - **2200**|公用網際網路存取 DMZ|公用 FCR|訂購時在其中部署「VMWare 主機」的原生無標籤 VLAN、原始原生 VLAN|
{: caption="表 1. 專用及公用 VLAN 範例" caption-side="top"}

## 訂購 vSphere Server
1. 登入 [{{site.data.keyword.slportal_full}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://control.softlayer.com/){: new_window}。
2. 按一下**帳戶 > 訂購**。
3. 在**裸機伺服器**區段中，按一下**每月**。
4. 選取伺服器。如需最低需求，請參閱「VMware 支援中心」出版品：
  * 已針對此範例選取下列伺服器。**附註：**具有雙重未結合公用及專用上行鏈路是備援的需求。請確認您建立 VLAN 的資料中心具有未結合的上行鏈路。
  * 容量叢集（數量：2）
    * 伺服器配置：從「雙處理器多核心伺服器」區段中選取 Intel Xeon 第 3 版伺服器
    * 軟體：OS = vSphere Enterprise Plus 6
    * OS 儲存空間：2 x 1 TB SATA（配置為 RAID 1）
    * 資料儲存空間：建議訂購 2 TB SATA 或 1.2 TB SSD 或耐久性/效能 NFS SAN 儲存空間
      * 如果您對其他儲存空間類型感興趣，請參閱[與 VMware 系統搭配使用的儲存空間](select-storage-option-use-vmware.html)
      * 上行鏈路埠速度：1 Gbps 雙重公用及專用網路（未結合）
        * 針對 VMware vSAN 解決方案，建議使用「10 Gbps 上行鏈路」
5. 如果您要在新的 IBM Cloud 資料中心內建立新的部署，請繼續步驟 6。如果這是擴充或部署至現有「資料中心」，請選取偏好的「後端 BCR VLAN + 前端 FCR VLAN」。例如，「後端 BCR VLAN」為 1101，而「前端 FCR VLAN」為 2200。**附註：**如果這是新部署或新 DC 中的新部署，則會在訂購伺服器時建立「後端 BCR VLAN」及「前端 FCR VLAN」。
6. 輸入**主機名稱**及**網域**。
7. 檢閱訂單，然後按一下**完成訂單**來啟動佈建處理程序。

## 訂購 vCenter Server

vCenter 是 Windows Server 的附加程式。此配置會擴增為 20 個 vSphere 主機。對於較大的實作，建議直接將 vCenter Server Appliance (VCSA) [部署及配置 vCenter Server Appliance (vCSA)](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html) 部署至 vSphere 叢集。

使用下列步驟，以訂購已安裝 vCenter 的虛擬伺服器：

1. 登入 {{site.data.keyword.slportal_short}}。
2. 按一下**帳戶 > 訂購**。
3. 訂購「虛擬伺服器」下的**每月**裸機或虛擬伺服器公用/專用節點實例 (VSI)。
  1. 若要讓「SoftLayer 虛擬伺服器實例 (VSI)」符合 vCenter 6.0 的資格，您必須至少部署於 **4 x 2.0 GHz 核心**及 **4 GB RAM**
  2. 如需 vCenter「部署」建議清單，請參閱 [VMware vCenter Server&trade; 6.0 部署手冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}。
4. 輸入下列資訊：
  * 根據「建議的最低伺服器配置」
    * vCPU 核心配置：4 x 2.0 GHz 核心
    * RAM 配置：12 GB RAM
    * 軟體：OS = Windows Server 2012 R2 Standard Edition（64 位元）
    * OS 特定附加程式：vCenter 6
    * 第一個磁碟：1 x 100 GB (SAN)
    * 第二個磁碟：1 x  50 GB (SAN)
    * 上行鏈路埠速度：1 Gbps 公用及專用網路上行鏈路

5. 如果這是新的「IBM Cloud 資料中心」中的新部署，請繼續進行下面的步驟 6。如果此部署是擴充或部署至現有「資料中心」，請選取偏好的「後端 BCR VLAN + 前端 FCR VLAN」。在範例中，「後端 BCR VLAN」為 1101，而「前端 FCR VLAN」為 2200（如果這是全新部署或新 DC 中的新部署，則會在訂購伺服器時建立「後端 BCR VLAN」及「前端 FCR VLAN」）。
6. 輸入**主機名稱**及**網域**。
7. 檢閱訂單，然後按一下**完成訂單**來啟動佈建處理程序。

## 訂購可攜式公用及專用子網路/IP 位址

**附註：**如果 VLAN 尚未完整佈建，請不要繼續進行。

子網路用於處理 VMware Guest Virtual Machine (VM) 及 VMware Host 核心型資料流量。

1. 從「控制入口網站」中，按一下**網路 > IP 管理 > 子網路**。
2. 按一下畫面右上方的**訂購 IP 位址**。
3. 選取**可攜式專用**。
4. 選取適當的 VLAN（範例：bcr01.wdc04：1101）
5. 按一下**繼續**。
6. 完成**訂購 IP 位址**表單。
7. 按一下畫面右上方的**訂購 IP 位址**。
8. 按一下**訂購**。
9. 針對每一個適用的 VLAN（例如 1101、2200），請遵循此處理程序
  1. 如需 VLAN 的相關資訊，請參閱[開始使用 VLAN](/docs/infrastructure/vlans/getting-started.html)。

|子網路類型|子網路大小|連結 VLAN|vSphere 主機用法|
|---|---|---|---|
|可攜式 - 專用|/27 32 位址|**1101**|管理 VM|
|可攜式 - 專用|/27 32 位址|**1101**|iSCSI 及 vMotion 的 VM 核心埠|
|可攜式 - 專用|/27 32 位址|**1101**|訪客 VM 的專用 IP|
|可攜式 - 公用|/27 32 位址|**2200**|訪客 VM 的公用 IP（選用）|
{: caption="表 2. 子網路" caption-side="top"}

### 選用 - 在 vSphere 主機上停用公用介面

如果您不要使用 vSphere 公用介面，則可以基於安全考量而停用這些介面。

1. 從「控制入口網站」中，按一下**裝置 > 裝置清單**。
2. 按一下「vSphere 主機」的名稱。
3. 按一下「配置」表格，然後向下捲動至「網路」區段。
4. 對於所有主機，針對每一個適用的 vSphere 主機 eth1 及 eth3 配對，選取**中斷連線**

這也可以透過 [{{site.data.keyword.slapi_full}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window} 執行。

## 建立及配置 vSphere 資料中心叢集 <!-- create and configure should be separate tasks-->

您現在可以登入 vCenter 伺服器並配置「vSphere 叢集」。

1. 從「控制入口網站」中，按一下**裝置 > 裝置清單**
2. 尋找 vCenter 裝置，然後按一下其名稱。
3. 將**裝置詳細資料**畫面向下捲動至伺服器的**網路**區段，並記下**專用 IP 位址**。
4. 向下捲動**裝置詳細資料**畫面，並記下 Windows OS 及「vCenter 軟體」的**密碼**。
5. 開啟「Microsoft 遠端桌面 (RDP)」階段作業，並透過其「公用 IP 位址」連接至 vCenter Server。
6. 使用您在步驟 4 中取得的密碼來登入。**附註：**如果使用「專用 IP 位址」來存取 vCenter，則需要有連接至 IBM Cloud 的作用中 VPN 連線。如需 VPN 存取的相關資訊，請參閱[啟用存取 IBM Cloud 基礎架構專用網路](/docs/customer-portal/getting-started.html#enable-private-network)。
7. 下載並安裝傳統 [vSphere Client ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window}，或透過鏈結 `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/` 使用 vSphere Web Client。
8. 使用您在步驟 3 及 4 中取得的 IP 位址和密碼，來登入 vCenter。
9. 用滑鼠右鍵按一下左窗格中的 vCenter 伺服器名稱，然後選取**新建資料中心**。
10. 輸入資料中心的適當名稱。
11. 用滑鼠右鍵按一下資料中心，然後選取**新建叢集**。
12. 輸入叢集名稱。此時，請不要開啟「叢集特性」：vSphere HA 或 vSphere DRS。
13. 按**下一步**。
14. 保持 **EVC** 的已停用狀態，然後按**下一步**。
15. 接受_預設值，將 swapfile 儲存至與虛擬機器相同的目錄_，然後按**下一步**。
16. 按一下**完成**來完成叢集。
17. 用滑鼠右鍵按一下您剛才建立的新叢集，然後選取**新增主機**。
18. 輸入其中一個 vSphere 主機的 IP 位址或「主機名稱」，並在**使用者名稱**欄位中輸入 **Root**，然後在**密碼**欄位中輸入主機的密碼。
19. 按一下「主機摘要」、「指派授權」、「鎖定模式」畫面中的**下一步**，然後按一下**完成**以完成將主機新增至「叢集」
20. 針對叢集中的每一個其他 vSphere 主機，重複步驟 18 及 19。完成之後，將會在新叢集下看到每一個 vSphere 主機。

### 配置 vSphere 主機的基本網路建構

使用下列步驟，以配置叢集中 vSphere 主機的基本建構。

1. 選取第一個 vSphere 主機，然後按一下**配置**標籤。
2. 在**硬體**區段下，選取**網路**。您應該已有 vSwitch0 及 vmnic0；請按一下 vSwitch0 旁的**內容**。
3. 在 **vSwitch 內容**視窗上選取**網路配接卡**，然後按一下**新增**按鈕。
4. 選取 vmnic2 以新增至 vSwitch0，然後按**下一步**。
5. 確定兩個 vmnic 都是**作用中配接卡**，然後按**下一步**。
6. 按一下**完成**。
7. 按一下**埠**標籤，並確定已強調顯示 vSwitch；按一下**編輯**。
8. 按一下**一般**標籤，並將 **MTU** 變更為 9000（巨大訊框）。
9. 按一下 **NIC 團隊**標籤，並將負載平衡變更為**根據 IP 遞送**雜湊，然後按一下**確定**。
10. 使用步驟 1 到 8，為叢集中的其他 vSphere 主機配置 vmnic。

現在需要為 vMotion 新增埠群組。群組可以建立為「虛擬標準交換器 (VSS)」或「虛擬分散式交換器 (VDS)」。基於範例用途，我們將建立 VSS 交換器。

1. 選取**配置**標籤，然後選取**網路**。
2. 按一下 vSwitch0 的**內容...**。
3. 按一下**新增...**來建立「埠群組」。
4. 選取 **VMkernel**，然後按**下一步**。
5. 在「埠群組內容」中，填入下列資訊：
  * **網路標籤：**埠群組的適當名稱。
  * **VLAN ID（選用）：**vMotion 資料流量的 VLAN ID（例如 1101）。VLAN ID 容許 VMware 為特定 VLAN 標記資料流量。
  * 選取**將此埠群組用於 vMotion**。
6. 按**下一步**。
7. 輸入 VLAN 的**可攜式 IP 位址**（您可以從 SoftLayer 入口網站、**網路 > IP 位址 > VLAN** 取得埠 IP 位址）。選取正確的 VLAN，然後您會在**子網路**下看到可攜式 IP 位址範圍。如果您沒有可用的「可攜式 IP 位址」，或已耗盡現行儲存區，請遵循「訂購專用子網路/IP 位址」小節中的步驟來訂購其他「可攜式 IP 位址」。
8. 按**下一步**，然後按一下**完成**來完成。

使用下列步驟，以建立 VM 資料流量的「埠群組」。

1. 按一下 vSwitch0 的**內容...**，然後選取**新增、虛擬機器**。
2. 在**埠群組內容**中，填入下列資訊：
  * **網路標籤：**輸入「埠群組」的名稱（例如，VM Data）。
  * **VLAN ID（選用）：**輸入 VLAN ID；我們已使用 1101 作為範例。VLAN ID 容許 VMware 為 VLAN 標記資料流量。

### 選用 - 安裝 VMware Add On 授權（NSX、vRealize、vSAN 等等）

既然 VMware 環境已啟動，您就已準備好繼續部署其他配置、訪客 VM 或 VMware Add On。VMware Add On 授權也可以透過 IBM Cloud 控制入口網站進行購買，以及透過「vCenter 主控台」予以新增。如需訂購及管理 VMware Add On 授權的相關資訊，請參閱 [VMware vSphere 6 訂購及管理授權](vmware-vsphere-6-ordering-and-managing-licenses.html)。

## 後續步驟
您現在具有在 IBM Cloud 資料中心內執行的基本單一網站 VMware 環境。基本配置只有本端資料儲存庫，使得它成為不包含 VMware DRS、HA、Storage DRS 及防火牆這類特性的簡化配置。

如需相關資訊，請參閱[常見問題：VMware](vmware-faq.html)。 
