---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 透過遠端主控台及虛擬媒體安裝 VMware vSphere ESXi

從安裝媒體部署 ESX 在所有版本中都很類似，而且可以在 BYOL（自帶授權）情況下使用。

## 需求
* 可存取「專用網路」的虛擬機器 (VM) 實例 [例如，雲端運算實例 (VSI)，其與 Windows 或 Linux 一起安裝、具有已啟用 Java 的瀏覽器，且可透過 vpn.softlayer.com 或 public IP 存取]。VSI 必須位在伺服器的「智慧型平台管理介面 (IPMI)」位址所在的相同專用網路上。
* VMware ESXi VIM Installer ISO 副本。

<!--## Steps -->

## 連接至 IPMI
1. 將 VMware ISO 上傳至「需求」中所指定的 VSI（VSI 應當有公用 Web 存取）。
2. 從客戶入口網站中收集 IPMI 位址及登入資訊。
3. 選取**裝置** > **裝置清單** > **[伺服器]** > 及**遠端管理**標籤。
4. 使用「遠端桌面 (RDP)」或 Remote X 連接至用於儲存 ESXi 映像檔的 VSI。
5. 在 RDP 階段作業中開啟 Web 瀏覽器，並輸入您在步驟 2 收集的 IPMI 位址。
6. 使用也可在步驟 2 中找到的認證（通常是 root 使用者）登入 IPMI 主控台。
* 記下您的 IPMI 使用者存取層次。它可能是「管理者」。如果將遠端儲存空間設為**操作員**，則在裝載遠端儲存空間時可能會發生問題。如果無法裝載媒體，則可以開立支援問題單，以提升您的 IPMI 認證。
7. 確認您位於首頁登入頁面，然後按一下**遠端控制** > **主控台重新導向** > **啟動主控台**。

## 連接 ISO
1. 在核心型虛擬機器 (KVM) 檢視器上，選取**虛擬媒體** > **虛擬儲存空間**。您的作業系統及 Java 版本可能需要您容許啟動 Java 型檢視器的存取權。
2. 在「虛擬儲存空間」視窗中，按一下 **CDROM & ISO** 標籤。針對「邏輯磁碟機類型」，選取 **ISO 檔案**，然後按一下**開啟映像檔**。
3. 移至 ESXi ISO，然後按一下**確定**。然後，按一下**外掛程式**。
4. 將 ISO 插入階段作業之後，請按一下**確定**。
* 回到 IPMI 網頁，然後按一下**遠端** > **控制** > **重設伺服器** > **執行動作**來重新啟動伺服器。

### 安裝及完成網路配置
1. 安裝 ESXi。
* 安裝完成之後，請務必**移除** ISO，以重新啟動伺服器。
2. 重新啟動伺服器。
3. 在伺服器重新啟動之後配置伺服器的 IP 位址。
4. 從裝置的「配置」標籤中收集詳細資料。

您現在可以管理 ESXi 主機。

如需如何設定「耐久性」或「效能」區塊儲存空間的相關資訊，請參閱[佈建及管理區塊儲存空間](/docs/infrastructure/BlockStorage/provisioning-block_storage.html)。

如需設定 QuantaStor 的相關資訊，請參閱 [QuantaStor 架構手冊](architecture-guide-quantastor-vmwaresoftlayer.html)。
