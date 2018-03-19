---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  移轉及升級至 VMware vSphere 6

使用 VMware 管理控制台，快速並輕鬆地展開 VMware 雲端環境，或將其移至任何 {{site.data.keyword.BluSoftlayer_full}} 資料中心。若要移轉及升級 vSphere 工作負載，請使用下列步驟作為指引。
{:shortdesc}

1. 收集資料。
2. 檢閱現有架構：
  1. 資源使用率（CPU/記憶體/儲存空間）。
  2. 追蹤及專案成長率。
  3. 識別出即將到來的未來專案。
  4. 判定已部署了哪些指派的 VLAN/子網路等等（可在控制入口網站中取得）。
  5. 尋找解決方案使用中的自行定義 RFC1918（專用）子網路。
3. 檢閱「VMWare 6 文件」，並加入 VMWare 社群：
  1. [VMware vSphere 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [VMware Technology Network ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://communities.vmware.com/welcome){: new_window}
4. 更新管理團隊的訓練，以支援 VMWare 6。
5. 規劃及設計新的架構。
6. 選取根據相符性的[資料中心 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window}。與 IBM Cloud 銷售人員合作，以根據產品/服務可用性來調整候選位置。
7. 定義必要 VLAN 及子網路（可攜式公用及專用 IP）。
8. 設計 vSphere Server：
  1. 檢閱現行 IBM Cloud 伺服器型錄。針對本端（開機）磁碟，建議搭配使用 Intel Xeon Server 第 3 版與備援上行鏈路、備援電源供應器及 RAID-1。
  2. 大部分具有 VMWare 的客戶都會遵循 N+1 硬性容量上限（所有 VM 都可以配置給已移除單一節點（用於維護/故障等等）的伺服器。
  3. 相較於其他標準 60-75%，許多客戶都想要更高的「軟性上限」~80%（'n' 伺服器配置的 80% 容量），原因是運算的處理很簡短。
  4. 來自外部供應商的 vSphere 訪客可能需要外部 OS 授權（例如 Microsoft、Red Hat）。
  5. 檢閱 [VMware vSphere 6.0 效能最佳作法 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window}
9. 設計 vCenter Server：
  1. 一般而言，中型「虛擬伺服器實例 (VSI)」是小型環境 (8 vCPU + 16 GB RAM) 的進入點。而裸機用於較大型的環境。
  2. vCenter 可以部署至獨立式「VSI Windows 虛擬機器」，以作為 OS 附加程式或應用裝置。
    1. 參照鏈結：
        * [vCenter Server 6.0 安裝需求 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://kb.vmware.com/s/article/2107948){: new_window}
        * [VMware vCenter Server 效能及最佳作法 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}
        * [使用 VMware vSphere 6 部署及配置 vCenter Server Appliance (vCSA)](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. 非 VMWare Server：識別及規劃可能需要的任何非 VMWare Server（虛擬或裸機），並據以進行規劃。
11. 儲存空間：
  1. 開發環境的儲存空間方案。具有進行虛擬化之 Snapshot 空間的 Endurance 2 IOPS/GB 是良好的開始儲存空間方案，但是，如果使用虛擬資料庫或其他高效能應用程式，則 4 IOPS/GB 層級較適合。通常建議使用 NFS 儲存空間。  
  2. 在[與 VMware 系統搭配使用的儲存空間](select-storage-option-use-vmware.html)上，可以找到選擇矩陣。
  3. Snapshot 空間最常用作進行復原點還原的次要測量。10% 是良好的開始位置，因為處理程序非常有效率而且易於調整大小。
12. 備份：
  1. 確定現有備份策略可運作。如果備份策略不存在，則應該予以建立。
  2. 您可以使用自己的備份解決方案。您可以使用 vSphere Enterprise Plus 授權隨附的備份特性、最佳化協力廠商解決方案（例如 VEEAM）或傳統 IBM Cloud r1soft 備份。
13. 開發移轉策略：
  1. 檢閱[安裝或升級至 ESXi 6.0 的最佳作法 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://kb.vmware.com/s/article/2109712){: new_window}。
  2. 檢閱現有 DNS 及（或）IP 配置，並視需要縮短 TTL。
  3. 開發方案，讓 VM 包括「來源」主機、目的地主機、來源 IP、目的地 IP 及關聯的 DNS 項目。
  4. 在大部分情境下，最好是逐一移轉 VM，然後更新公用及專用網路配置。當您從舊版本移至新版本時，通常只需要關閉 VM 並在環境之間執行 _detach/attach_，以對 VM 進行「快速處理」。如果您在位置之間移動，則可能是長距離 vMotion。
  5. 開發測試方案來驗證環境。
  6. 與使用者協調變更/維護時間。個別 VM 維護時間可考慮傳送資料、配置 VM、變更和延伸 DNS，以及進行疑難排解的時間。
14. 部署新的環境：
  1. [開始使用 VMware vSphere 6](vmware-vsphere-6-getting-started.html)。
  2. 訂購新的 vSphere 及 vCenter Server（以及您需要的任何其他伺服器）。
      **附註：**確定已選取適當的「未結合」網路上行鏈路。
  3. 訂購及配置適當的儲存空間：[IBM File Storage for IBM Cloud（含 VMware）架構手冊](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html)
  4. 訂購新的 VLAN 及可攜式子網路（詳細架構圖，而且可能需要進行調整）。
  5. 配置 vCenter 以與 vSphere Server 進行通訊，並配置環境。
  6. 在即時環境中進行備份。
  7. 執行移轉方案及關聯的測試方案。
  8. 在新環境中實作備份。
  9. 操作新環境。
  10. 解除舊環境的任務。
