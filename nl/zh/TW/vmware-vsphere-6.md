---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware 授權選項 

透過部署至 {{site.data.keyword.BluSoftlayer_full}} 企業級全球雲端，VMware 管理者即可快速實現符合成本效益的混合式雲端特徵。關鍵 {{site.data.keyword.BluSoftlayer_notm}} 差異因子在於 vSphere 工作負載及型錄可以佈建至 {{site.data.keyword.BluSoftlayer_notm}} 資料中心內的 VMware vSphere 環境，而不需要修改 VMware VM 或訪客。這些部署可以使用一般 vSphere Hypervisor 及管理/編排平台進行。

除了提供 vSphere 6 Enterprise Plus 授權以外，{{site.data.keyword.BluSoftlayer_notm}} 還提供對 vCenter、NSX、vRealize、vSAN 及 Site Recovery Manager (SRM) 的每月授權。

## VMware vSphere

**預期用法：**裸機伺服器會虛擬化 OS 平台來抽象化處理器、記憶體、儲存空間及網路資源，以在單一實體伺服器上建立多部虛擬伺服器。多部實體伺服器可以一起形成叢集，以建立專用雲端。

**使用者介面：**vCenter Client、VMware API、VMware CLI

**特性：**
* vMotion 即時移轉
* 高可用性
* 容錯
* 抄寫
* Nvidia GRID vGPU 虛擬化
* 工作負載容量最佳化
* 分散式資源排程器 (DRS)
* 精簡佈建
* 網路 I/O 控制

## VMware vCenter

**預期用法：**集中管理每一個 vSphere 主機內的運算資源。雖然可以個別管理 vSphere 主機，但將它們置於 vCenter 控制項下即可啟用下列功能：

**使用者介面：**Web Client、Thick Client、VMware API、VMware CLI

**特性：**
* 受管理 vSphere 主機及訪客虛擬機器內所有層面的集中控制及可見性。
* 透過 vCenter Web 用戶端提供玻璃介面視圖的單一窗格，來進行運算網路及儲存空間管理。
* 主動最佳化。啟用資源的配置及最佳化，讓 vSphere 主機具有最大效率。
* 其他整合附加程式及服務（例如 NSX、vRealize、vSAN 及 Site Recovery Manager (SRM)）的延伸管理功能。
* 監視、警示、排定。雲端管理者可以檢視事件、vCenter Web 用戶端內的警示，以及配置已排定的動作。
* 自動化引擎。vCenter 是執行透過 vSphere API Web 介面提供給它之作業的引擎。VMware vRealize Automation 及 vRealize Orchestration 是透過 VMware API 驅動 vCenter 動作的應用程式範例。

## VMware NSX

**預期用法：**NSX 提供支援雲端平台作業所需的重要「軟體定義網路 (SDN)」功能。

**使用者介面：**vCenter Client、VMware API、VMware CLI

**特性：**
* 負載平衡
* 防火牆
* 遞送
* 邏輯交換器
* VPN
* VxLAN 分段/通道端點

## VMware vRealize

**預期用法：**VMware vRealize Suite 是一種企業級雲端管理平台，可用來管理異質混合式雲端。

**使用者介面：**vCenter Client、VMware API、VMware CLI

**授權模型：**每個月的每個處理器

**特性：**
* vRealize Automation：自動交付個人化基礎架構、應用程式及自訂 IT 服務
* vRealize Operations：智慧型性能、效能、容量及配置管理編排
* vRealize Log Insight：即時日誌管理及日誌分析。

## VMware vSAN

**預期用法：**VMware vSAN 是一種分散式儲存技術，可將每一個 vSphere 主機上的本端儲存磁碟機聚集並聯合排存至 vSAN 叢集中所有主機都可以存取的無共用儲存裝置。

**使用者介面：**vCenter Client、VMware API、VMware CLI

**特性：**
* 分散式主機型儲存空間
* 無共用架構
* 擴增為 64 個節點
* 低延遲
* 可配置的容錯

## VMware Site Recovery Manager (SRM)

**預期用法：**VMware Site Recovery Manager (SRM) 可在專用雲端環境中的網站之間啟用應用程式可用性及行動性。透過充分運用虛擬機器的封裝及隔離，Site Recovery Manager 可簡化災難回復的自動化，以符合回復時間目標 (RTO)。SRM 也有助於減少與業務持續方案相關聯的成本，並達到回復虛擬環境的低風險且可預測的結果。

**使用者介面：**vCenter Client、VMware API、VMware CLI

**特性：**
* 非干擾性回復測試
* 自動編排工作流程
* 自動回復網路及安全設定
* 自訂自動化的延伸
* 已編排的跨 vCenter vMotion
* 集中化回復計劃
* 原則型管理
