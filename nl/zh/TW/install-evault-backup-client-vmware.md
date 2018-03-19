---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 安裝 EVault Backup Client for VMware

您可以透過目標 ESX 伺服器內 Shell 或終端機中的一系列指令，在 VMware 伺服器上安裝 EVault Backup 用戶端。此程序概述在 VMware 伺服器上安裝 EVault Backup 用戶端所需的步驟：
{:shortdesc}

若要安裝「代理程式」，請使用下列指令將 `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` 套件下載並複製到目標 ESX Server：

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**附註：**您必須在目標 ESX Server 上本端執行下列步驟。

1. 從套件解壓縮檔案。若要這樣做，請使用以下指令（在此指令中，"PACKAGENAME" 可以是 "Agent-VMware-ESX-Server-6.71"）：<br/>`tar xvfz PACKAGENAME.tar.gz`
2. 移至您在其中解壓縮套件的目錄。
3. 執行安裝 Script：<br />`# ./install.sh`<br/><br/>
**附註：**安裝 Script 會以互動方式提示您輸入 Web 登錄（位址、埠號及鑑別）和日誌檔名稱之類的配置資訊。

請輸入此伺服器的 WebCC 使用者名稱。

4. 輸入 **EVault Backup 使用者名稱**作為提示要求 WebCC 使用者名稱的輸入。如需檢視「EVault Backup 使用者名稱」的指示，請參閱[檢視 EVault Backup 儲存空間詳細資料](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal)程序。
5. 輸入「EVault Backup 密碼」作為提示要求 WebCC 密碼的輸入。
6. 安裝完成時，會出現完成訊息，並且會執行「代理程式」常駐程式。


其他安裝注意事項：<br/>
如果安裝成功，則 Install.log 會位在安裝目錄中。<br/>
例如：`/opt/BUAgent/Install.log`

如果安裝失敗並回復，則安裝日誌會位在 `<Installation Failure directory> 中。`<br/>
如果安裝失敗且未回復，則安裝日誌會位在 `<Installation Kit directory>` 中。<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
請確定您已連接至 {{site.data.keyword.BluSoftlayer_full}} VPN，以檢視上述鏈結。如需連接至 IBM Cloud VPN 的相關資訊，請參閱[啟用存取 IBM Cloud 基礎架構專用網路](/docs/customer-portal/getting-started.html#enable-private-network)。
