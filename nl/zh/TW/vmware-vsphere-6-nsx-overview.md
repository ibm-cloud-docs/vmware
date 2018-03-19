---
copyright:
  years: 1994, 2017
lastupdated: "2017-06-12"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 NSX 概觀

VMware NSX&reg; 是一種軟體網路及安全虛擬化平台，可為網路提供虛擬機器的作業模型。虛擬網路可在軟體中重新產生第 2 層 - 第 7 層網路模型，以在幾秒鐘內透過程式設計方式建立及佈建複雜的多層網路拓蹼，而不需要其他「{{site.data.keyword.BluSoftlayer_notm}} 專用網路」。NSX 也提供新的網路安全模型。安全設定檔會配送至虛擬埠並由虛擬埠強制執行，並與虛擬機器一起移動。

NIX 支援 VMware 的軟體定義資料中心策略。透過在所有資料中心資源與服務間進行抽象化、集中儲存及自動化的虛擬化功能，軟體定義的資料中心架構會透過原則驅動自動化，來簡化及加速運算、儲存和網路資源的佈建和管理。透過虛擬化網路，NSX 可提供全新的網路作業模式，以突破目前的實際網路屏障，並讓 VMware 及 {{site.data.keyword.BluSoftlayer_notm}} 可以更快速且更靈活地降低成本。

NSX 包括邏輯網路服務的程式庫 - 邏輯交換器、邏輯路由器、邏輯防火牆、邏輯負載平衡器、邏輯 VPN 及分散式安全。您不需要修改即可在支援現有應用程式的隔離軟體型虛擬網路中建立這些服務的自訂組合，或提供新應用程式工作負載的唯一需求。虛擬網路是以程式設計方式進行佈建及管理，與 {{site.data.keyword.BluSoftlayer_notm}} 網路建構無關。這項硬體取消連結引進可轉換資料中心作業的靈活性、速度及作業效率。NSX 的好處包括下列特性：
* DataCenter 自動化
* 自助式網路服務
* 利用自動化網路及服務佈建進行快速應用程式部署
* 在相同的裸機基礎架構上隔離開發、測試及正式作業環境
* 單一帳戶多方承租戶雲端

NSX 可以透過 vSphere Web Client、指令行介面 (CLI) 及 REST API 進行配置。NSX 所提供的核心網路服務如下：

## 邏輯交換器
雲端部署或虛擬資料中心在多個承租戶之間可能具有各種應用程式。基於安全、錯誤隔離以及避免出現重疊的 IP 位址問題，這些應用程式及承租戶需要彼此隔離。NSX 邏輯交換器會建立可邏輯佈線之應用程式或承租戶虛擬機器的邏輯播送網域或區段 (VXLAN vWires)。這讓部署更具彈性且更快速，同時仍然提供實體網路播送網域 (VLAN) 的所有特徵，而沒有實體層 2 的雜亂。邏輯交換器容許將數千個承租戶網路佈建至單一「{{site.data.keyword.BluSoftlayer_notm}} 專用網路 (VLAN)」。邏輯交換器是分散式的，而且可以跨越任意大型運算叢集，甚至可以跨相同資料中心內的 Pod。這容許資料中心內具有虛擬機器行動性，而不需要限制跨 Pod 的實體層 2 (VLAN) 界限。

## 邏輯路由器
動態遞送提供第 2 層播送網域（VXLAN vWires/邏輯交換器）之間的必要轉遞資訊，因此可讓您降低第 2 層播送網域，並改善網路效率及擴充。NSX 將這項智慧擴充至工作負載所在的位置，以提供「東-西」遞送功能。這容許更多的直接虛擬機器對虛擬機器通訊，而不需要昂貴或及時地擴充中繼站。同時，NSX 也提供 {{site.data.keyword.BluSoftlayer_notm}} 資料中心的「北-南」連線功能入埠/出埠，進而讓承租戶安全且有效率地存取公用網路。

## 邏輯防火牆
「邏輯防火牆」提供動態虛擬資料中心的安全機制。「NSX 邏輯防火牆」的「分散式防火牆」元件容許您根據 VM 名稱及屬性、使用者身分、vCenter 物件（例如 DataCenter 及主機）以及傳統網路屬性（例如 IP 位址、VLAN 等等）來分段虛擬資料中心實體（例如虛擬機器）。「Edge 防火牆」元件可協助您達成主要周邊安全需求，例如根據 IP/VLAN 建構、多方承租戶虛擬資料中心內的承租戶對承租戶隔離、「網址轉換 (NAT)」、VPN 及使用者型 SSL VPN 來建置 DMZ。「Edge 防火牆」可以與 {{site.data.keyword.BluSoftlayer_notm}} 中的 Vyatta & Fortinet 服務搭配運用，或將其取代，以進行周邊保護。「防火牆流程監視」特性會顯示應用程式通訊協定層次的虛擬機器之間的網路活動。您可以使用這項資訊來審核網路資料流量、定義並修正防火牆原則，以及識別對網路的威脅。

## 邏輯虛擬專用網路 (VPN)
SSL VPN-Plus 容許遠端使用者存取專用公司應用程式。IPSec VPN 提供 NSX Edge 實例與遠端網站（在 {{site.data.keyword.BluSoftlayer_notm}} 上執行的 VMware）之間的網站間連線功能。L2 VPN 容許您擴充資料中心，方法是讓虛擬機器可以跨越地理界限以及 {{site.data.keyword.BluSoftlayer_notm}} 資料中心和本端 VMware 環境來保留網路連線功能。

## 邏輯負載平衡器
NSX Edge 負載平衡器可讓網路資料流量遵循特定目的地的多條路徑。它會將送入的服務要求平均配送到多部伺服器，如此，使用者可以很清楚負載分佈狀況。因此，負載平衡有助於達成最佳資源使用率、最大化傳輸量、最小化回應時間，以及避免超載。NSX Edge 提供最高到第 7 層的負載平衡。

## 服務編製器
「服務編製器」可協助您將網路及安全服務佈建及指派給虛擬基礎架構中的應用程式。這些服務可以對映並套用至安全群組中的虛擬機器。「資料安全」可讓您看到組織之虛擬化及雲端環境（包括 {{site.data.keyword.BluSoftlayer_notm}}）內所儲存的機密資料。根據「NSX 資料安全」所報告的違規，您可以確保機密資料受到適當保護，並評量與全球規定的相符性。

## NSX 延伸
VMware 夥伴可以將其網路服務解決方案與 NSX 平台整合，讓客戶在 VMware 產品及夥伴解決方案之間具有整合體驗。資料中心操作員可以在幾秒鐘內佈建複雜的多層虛擬網路，這與來自 {{site.data.keyword.BluSoftlayer_notm}} 的基礎網路拓蹼或元件無關。

## NSX 核心元件
本節說明將部署於 {{site.data.keyword.BluSoftlayer_notm}} 的核心 NSX 元件。這些元件可以透過 vSphere Web Client、指令行介面 (CLI) 及 REST API 進行配置/管理。VMware NSX 需要至少已部署 vSphere & vCenter 第 6 版的運作中 {{site.data.keyword.BluSoftlayer_notm}} 環境。本節中說明的所有元件都會部署為 {{site.data.keyword.BluSoftlayer_notm}} 上執行的 VMware Appliance VM。「NSX 元件」不支援作為「虛擬伺服器實例 (VSI)」。建議遵循指引來建立專用「ESX 管理叢集」，此外可能還需要有 Edge Services 叢集，這在本文件中會進一步討論。

<!-- ![Figure 1](images/vmware6_nsx_overview_1.png)-->

## NSX Manager
NSX Manager 是 NSX 的集中化網路管理元件，並安裝為 vCenter Server 環境的 ESX 主機上的虛擬應用裝置。{{site.data.keyword.BluSoftlayer_notm}} Architecture 建議將此 VM 部署至專用「管理 ESX 叢集」。其中一個 NSX Manager 會對映至單一 vCenter Server 環境及多個 NSX Edge、「vShield 端點」及「NSX 資料安全」實例。

## NSX vSwitch
NSX vSwitch 是在 {{site.data.keyword.BluSoftlayer_notm}} ESX 主機上運作的軟體，可以在伺服器與實體網路之間形成軟體抽象層。隨著資料中心需求不斷地增加並加速，與速度及資料本身存取相關的需求也會繼續成長。在大部分的基礎架構中，虛擬機器存取及行動性通常取決於實體網路基礎架構，以及它們所在的實體網路環境。這會強制虛擬工作負載進入較不理想的環境，原因是可能有第 2 層或第 3 層界限，例如關聯至特定 Pod 中的特定「{{site.data.keyword.BluSoftlayer_notm}} 專用網路 (VLAN)」。NSX vSwitch 可讓您將這些虛擬工作負載放在資料中心的任何可用基礎架構上，不論基礎實體網路基礎架構情況。這不僅可增加彈性及行動性，也可以提高可用性及復原力。

## NSX 控制器 
NSX 控制器是一種進階分散式狀態管理系統，可控制虛擬網路及 VXLAN 重疊傳輸通道。NSX 控制器是網路內所有邏輯交換器的中央控制點，可維護所有虛擬機器、主機、邏輯交換器及 VXLAN 的資訊。控制器支援三個邏輯交換器控制平面模式：「多重播送」、「單點播送」及「混合式」。這些模式會取消 NSX 與實體網路的連結。{{site.data.keyword.BluSoftlayer_notm}} 需要「單點播送」模式，因為「{{site.data.keyword.BluSoftlayer_notm}} 專用網路 (VLAN)」未提供「多重播送」或「混合式」模式的 IGMP 服務。「NSX 控制器」將搭配使用「單點播放」模式與虛擬通道端點 (VTEPS)，來提供 Mac 學習及其他功能，以容許在邏輯交換器內的「VXLAN 播送」、「不明」單點播放及「多重播送 (BUM)」資料流量。單點播送模式可本端抄寫主機上的所有 BUM 資料流量，而且在 VTEPS 之間的第 3 層連線功能外面不需要任何實體網路配置。NSX Manager 會將「NSX 控制器」部署為最少有 3 個控制器節點的集合，以及搭配各種其他節點來支援（分散式）第 3 層遞送服務。所有節點都會部署為虛擬機器，而且是透過位於 {{site.data.keyword.BluSoftlayer_notm}} 之「ESX 管理叢集」上的 NSX Manager 進行管理。

## NSX Edge
NSX Edge 提供網路邊緣安全及閘道服務，以隔離虛擬化網路。您可以將 NSX Edge 安裝為邏輯（分散式）路由器或服務閘道。NSX Edge 邏輯（分散式）路由器提供使用承租戶 IP 位址空間及資料路徑隔離的「東-西」分散式遞送。位於不同子網路的相同主機上的虛擬機器或工作負載可以彼此通訊，而不需要遍訪傳統遞送介面。NSX Edge Gateway 藉由提供一般閘道服務（例如 DHCP、VPN、NAT、動態遞送及「負載平衡」），將隔離的 Stub 網路連接至共用（上行鏈路）網路。NSX Edge 的一般部署包括在 DMZ、VPN Extranets 及多方承租戶雲端環境中，而在這些環境中，NSX Edge 會建立每一個承租戶的虛擬界限。
