---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 與 VMware 系統搭配使用的儲存空間
您有數個儲存空間選項。它們可以選擇專用、共用或攜帶自己的儲存空間解決方案。使用下列資訊可協助您決定哪個儲存空間解決方案最適合您的工作負載。

「表 1」包含儲存空間層級，而您的工作負載可能會下降。
<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 1. 儲存空間層級</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>第 1 層</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>第 2 層</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>第 3 層</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>商業用途</strong></p>
			</td>
			<td style="width:160px;">
				<p>高效能及高可用性正式作業應用程式、資料庫和資料</p>
			</td>
			<td style="width:160px;">
				<p>非任務重要測試及開發應用程式、資料庫和資料</p>
			</td>
			<td style="width:160px;">
				<p>非任務重要資料儲存空間、備份及保存</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>效能</strong></p>
			</td>
			<td style="width:160px;">
				<p>高（SSD、SAS）</p>
			</td>
			<td style="width:160px;">
				<p>中（SAS、SATA）</p>
			</td>
			<td style="width:160px;">
				<p>低 (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>保證 IOPS</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>高可用性 (HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>抄寫</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Snapshot</strong></p>
			</td>
			<td style="width:160px;">
				<p>是</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
			<td style="width:160px;">
				<p>否</p>
			</td>
		</tr>
	</tbody>
</table>


## VMware 專用及共用儲存空間選項

您可以從數個儲存空間選項中進行選擇。對於專用儲存空間，您可以選取本端磁碟選項、VSAN 或 QuantaStor。對於共用儲存空間，您可以選取「耐久性」或「效能」儲存空間。如果您決定攜帶儲存空間，則有數個「專用」選項，包括 NetApp OnTap Edge、「NetApp 專用儲存空間 (NPS)」、{{site.data.keyword.IBM}} Spectrum Accelerate 及軟體定義的儲存空間。為方便使用，「表 2」及「表 3」提供選項的並列比較。

## 專用儲存空間選項

在單一承租戶環境中，有數個用於連接至 VMware 的儲存空間選項： 

* 本端
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## 本端儲存空間

使用 ESX 從 IBM Cloud 客戶入口網站訂購 {{site.data.keyword.baremetal_short}}，並選取想要的磁碟 [SATA、序列連接的 SCSI (SA SCSI) 或 SSD]。
 
您可以攜帶自己的 ESX 授權，但需要開啟具有「支援」的問題單，以通知他們發生變更。

* 建議的工作負載：第 3 層
* 效能：有限：根據 RAID 及磁碟類型。SSD 的成本會增加，以取得更好的效能。
* 可擴充性：限制機箱中的磁碟機槽數
* 通訊協定：不適用
* 成本：低資本支出 (CAPEX) 及營運支出 (OPEX)
* HA：無法使用
* 抄寫：[vSphere Replication Virtual Appliance ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* 可靠性：多個單一失敗點



## vSAN [1]

* 建議的工作負載：第 1 層
* 效能：根據主機配置，每個主機有 90K+ 個 IOPS
* 可擴充性：最多 2 TB 的 5.5 版虛擬機器磁碟 (VMDK)；最多 62 TB 的 6.0 版 VMDK。使用更多節點橫向擴充。
* 通訊協定：專有
* 成本：中，適用於 CAPEX 及 OPEX
* HA：支援主機及磁碟故障。VMware 第 6 版支援失敗網域。
* 抄寫：[vSphere Replication Virtual Appliance ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* 抄寫及災難回復：
    1. 透過 VMware vCenter Server 排定 VM 備份
    2. 建立 VM Snapshot
    3. 為 VM 建立的 Data DE
    4. 還原 VM
 * 可靠性：七個以上主機最多容忍三個主機故障。VMware 第 6 版已引進失敗網域。   

[1] vSan 6.2 新增特性、延伸叢集，容許主機位在相同資料中心的不同 Pod 中（正在進行驗證測試）。<!-- Should this in progress mention be removed? -->

vSAN 5.5 只適用於 BYOL（自帶授權）。如果您使用 Avago LSI MegaRAID SAS 9361-8i 磁碟控制器，則只有 VMware 會提供支援。

vSAN 6.0 可直接從具有 CPU 授權計費基礎的 IBM Cloud 入口網站取得。

## QuantaStor

[OSNexus 解決方案設計手冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} 可以用來協助使用 QuantaStor 連接 VMware。

* 建議的工作負載：第 2 層及第 3 層 
* 效能：根據磁碟機數目、RAID 及磁碟使用（iSCSI 或 NFS）的變數  
* 可擴充性：第 3 版單一機架支援 128TB；沒有擴增或橫向擴充。 
* 通訊協定：iSCSI、NFS 及 SMB 
* 成本：高，適用於 CAPEX 及 OPEX 
* HA：無法使用  
* 抄寫：內建抄寫特性；沒有可用的 SRA。也可以使用 vSphere Replication Appliance 
* 可靠性：機殼及 RAID 控制器的單一失敗點。


<a name="NetApp"></a>
## NetApp Data OnTap Edge

您必須從 NetApp 或 IBM 購買 NetApp 裝置。您需要將它安裝在 {{site.data.keyword.BluSoftlayer}} 資料中心的 {{site.data.keyword.baremetal_short}} 上。

如需使用 NetApp 連接 VMware 的相關資訊，請參閱下列鏈結：
* [NetApp ONTAP Select ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge：使用 NetApp 基本概念在伺服器上建置資料中心 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* 建議的工作負載：第 2 層及第 3 層
* 效能：根據磁碟機數目及 RAID 的變數
* 可擴充性：支援 110 TB；無橫向擴充。
* 通訊協定：iSCSI、NFS 及 SMB
* 成本：中，適用於 CAPEX 及 OPEX
* HA：無法使用
* 抄寫：支援 SnapMirror；也可以使用 [vRealize Automation ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.vmware.com/products/vrealize-automation){: new_window} (vRA) 達成。
* 可靠性：機殼及 RAID 控制器的單一失敗點。

<a name="NPS"></a>
## NetApp Private Storage

您必須從 NetApp 或 IBM 購買 NetApp 裝置。您需要將它安裝在 IBM Cloud 資料中心附近的其中一個主機託管網站內，然後使用「直接鏈結主機託管」或「直接鏈結雲端」進行連接。

如需使用 NetApp 連接至 VMware 的相關資訊，請參閱下列鏈結： 
* [NetApp Private Storage for IBM Cloud ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [解決方案簡述：NetApp Private Storage for IBM Cloud ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* 建議的工作負載：第 1 層
* 效能：根據 NetApp 模型
* 可擴充性：支援增加磁碟機及機架來提高容量及 IOPS
* 通訊協定：iSCSI、NFS 及 SMB
* 成本：高，適用於 CAPEX 及 OPEX
* HA：雙重磁頭及控制器
* 抄寫：支援 SnapVault 及 SnapMirror；也可以使用 [vRealize Automation ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.vmware.com/products/vrealize-automation) 達成。
* 可靠性：高備援及 MPIO 支援

<a name="IBM"></a>
## IBM Spectrum Accelerate

IBM Spectrum Accelerate 專用儲存空間選項不適用於 IBM Cloud 客戶入口網站。<!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* 建議的工作負載：第 1 層
* 效能：根據磁碟數目、SSD（選用）以及提供給每一個「節點」VM 的記憶體數量。
* 可擴充性：擴充 ~8 - 325 TB 可用
  * 最小容量：3 個 VM x 6 個磁碟機
  * 最大容量：15 個 VM x 12 個磁碟機
  * 透過 IBM Hyper-Scale Manager，擴增為 144 個虛擬陣列且有超過 40 PB 可用
  * 新增更多節點以擴充非干擾性容量
  * 每個節點支援 1 x 500 或 800 GB SSD
* 通訊協定：僅限 iSCSI
* 成本：取決於針對節點所部署的定價模型及實體機器。高 CAPEX；中到低 OPEX（視授權而定）。
  * 根據可用容量的二進位 (TiB) 定價
  * 未關聯至任何特定硬體配置。範例：200 TiB 授權可以使用各種方式進行部署 - 一個 200 TiB 實例、兩個 100 TiB 實例，或四個 50 TiB 實例
  * 提供兩種方式：長期授權 [包括一年的訂閱及服務 (S&S)] 及每月授權（包括 S&S）
* HA：叢集解決方案
* 抄寫：使用 [vRealize Automation ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.vmware.com/products/vrealize-automation){: new_window} 或 SRA 達成，這兩者都可以用來使用 VMware 的 Site Recovery Manager (SRM) 從實體 IBM XIV 進行抄寫
  * [vSphere Replication ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [IBM XIV Gen3 Storage System 的 VMware vCenter Site Recovery Manager 5.x 版準則 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* 可靠性：高備援及 MPIO 支援。任何可用節點都可以管理叢集。IBM Spectrum Accelerate 目前並未透過硬體式 IBM XIV 支援下列功能：
  * 三網站鏡映
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG 第 6 版
  * 6 TB 磁碟機
  * Storage Management Initiative Specifications (SMI-S) 1.6
  * 待用資料加密
  * vStorage for API Array Integration (VAAI) Licensing 現在與虛擬磁區 (VVol) 一起提供
  * vCenter Operations Manager (VCop)
  * 如需 IBM XIV Storage System 的相關資訊，請參閱 [IBM XIV Storage System 的平台及應用程式整合 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}

## 共用儲存空間選項

有兩個儲存空間選項，可用來在多方承租戶環境中連接至 VMware：「區塊儲存空間」及「檔案儲存空間」。

### 區塊及檔案儲存空間

使用 ESX 從 IBM Cloud 客戶入口網站訂購 {{site.data.keyword.baremetal_short}}。

在 VMware 中，**主機裝置詳細資料儲存空間**標籤上提供三個 <!--**Authorize** (**Block** or **File**) **Storage SoftLayer** --> 預先定義值：「使用者名稱」、「密碼」（適用於 CHAP 鑑別）及「主機 IQN」。

如需佈建區塊儲存空間的相關資訊，請參閱[佈建及管理區塊儲存空間](/docs/infrastructure/BlockStorage/provisioning-block_storage.html)。

如需佈建檔案儲存空間的相關資訊，請參閱[佈建及管理 IBM File Storage for IBM Cloud](/docs/infrastructure/FileStorage/provisioning-file-storage.html)。

* 建議的工作負載：第 1 層、第 2 層及第 3 層
* 兩種佈建效能方式：
    1. 耐久性 IOPS 層級：每個 GB 中提供 0.25、2、4 或 104 個 IOPS
    2. 效能配置 IOPS：指定與容量無關的 IOPS。建議用於具有良好定義效能需求的工作負載。
    * 可預測的儲存空間效能參數
    * 可以將多個磁區分段在一起，以達到較高的 IOPS 及更多的傳輸量
* 延遲 <10 毫秒，最多 48,000 個 IOPS
* 可擴充性：可訂購 20 GB 到 12 TB。在購買之後，就無法調整磁區大小。
* 通訊協定：iSCSI 及 NFS
* 成本：高，適用於 CAPEX（10x 適用於相同大小的 SAN）及 OPEX
* HA：雙重磁頭及控制器
* 抄寫：透過 IBM Cloud Private Network 提供的 Snapshot 及「抄寫」；也可以使用 [vRealize Automation ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.vmware.com/products/vrealize-automation){: new_window} 達成，但沒有 SRA。
* 可靠性：高備援；iSCSI 使用 MPIO 連線；NFS 型儲存空間是透過 TCP/IP 連線遞送。已啟用 Snapshot 及「抄寫」。

「表 2」提供單一承租戶環境中專用儲存空間的優缺點。

<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 2. VMware 專用儲存空間選項的優缺點</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; 專用儲存空間（單一承租戶）</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>重要因素/儲存空間選項</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>本端</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>虛擬 SAN</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:99px;">
				<p>QuantaStor</p>
			</td>
			<td bgcolor="#C6D9F1" colspan="2" style="width:159px;">
				<p align="center">NetApp</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p>IBM Spectrum Accelerate</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>OnTap Edge</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>NPS</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p align="center">&nbsp;</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>類型</strong></p>
			</td>
			<td style="width:87px;">
				<p>本端</p>
			</td>
			<td style="width:95px;">
				<p>SDS</p>
			</td>
			<td style="width:99px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>Monolithic</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>效能</strong></p>
			</td>
			<td style="width:87px;">
				<p>根據 SSD /SA-SCSI 規格；進一步 RAID 5/10 可以用於讀/寫增益。</p>
			</td>
			<td style="width:95px;">
				<p>取決於主機配置，每個主機有 90K+ 個 IOPS。每個主機有 100 個 VM、每個叢集有 32 個主機、每個叢集有 3,200 個 VM，僅保護 2,048 個（5.5 版）</p>
				<p>最多 20K IOPS、每個主機有 200 個 VM、每個叢集有 64 個主機，以及每個叢集有 6,000 個受保護 VM（6.0 版）。</p>
			</td>
			<td style="width:99px;">
				<p>根據所選取磁碟的類型及數目，以及 RAID 配置和 iSCSI 或 NFS 使用。</p>
			</td>
			<td style="width:80px;">
				<p>根據所選取磁碟的類型及數目，以及 RAID 配置動作。</p>
			</td>
			<td style="width:80px;">
				<p>取決於模型。</p>
			</td>
			<td style="width:96px;">
				<p>根據所選取磁碟的類型及數目，以及每個 Hypervisor 節點的 RAID 配置和選擇性使用 SSD 磁碟。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可擴充性</strong></p>
			</td>
			<td style="width:87px;">
				<p>大小及磁碟 I/O 傳輸量的有限成長。</p>
			</td>
			<td style="width:95px;">
				<p>5.5 版最多有 2TB 的虛擬機器磁碟 (VMDK)，而 6.0 版最多有 62TB。</p>
				<p>使用更多節點橫向擴充。</p>
			</td>
			<td style="width:99px;">
				<p>最多 128TB (3.x) 的單一 QS。無擴增或橫向擴充。</p>
			</td>
			<td style="width:80px;">
				<p>最多 10TB；無橫向擴充。</p>
			</td>
			<td style="width:80px;">
				<p>是，新增磁碟機架的容量及 IOPS。</p>
			</td>
			<td style="width:96px;">
				<p>從 ~8 擴充至 325TB 可用空間。</p>
				<p>容量下限是 3 個 VM x 6 個磁碟機。</p>
				<p>容量上限是 15 個 VM x 12 個磁碟機。</p>
				<p>透過 IBM Hyper-Scale Manager，擴增為 144 個虛擬陣列且有超過 40 PB 可用</p>
				<p>新增更多節點以擴充非干擾性容量。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>通訊協定</strong></p>
			</td>
			<td style="width:87px;">
				<p>NA</p>
			</td>
			<td style="width:95px;">
				<p>專有</p>
			</td>
			<td style="width:99px;">
				<p>iSCSI/NFS/SMB</p>
			</td>
			<td colspan="2" style="width:159px;">
				<p align="center">iSCSI/NFS/SMB</p>
			</td>
			<td style="width:96px;">
				<p>iSCSI</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>使用案例</strong></p>
			</td>
			<td style="width:87px;">
				<p>第 2 層及第 3 層工作負載</p>
			</td>
			<td style="width:95px;">
				<p>第 1 層工作負載</p>
			</td>
			<td style="width:99px;">
				<p>第 2 層及第 3 層工作負載</p>
			</td>
			<td style="width:80px;">
				<p>第 2 層及第 3 層工作負載</p>
			</td>
			<td style="width:80px;">
				<p>第 1 層工作負載</p>
			</td>
			<td style="width:96px;">
				<p>第 1 層工作負載</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>高可用性 (HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>可與 RAID 搭配使用</p>
			</td>
			<td style="width:95px;">
				<p>是；主機及磁碟故障；失敗網域（6.0 版）</p>
			</td>
			<td style="width:99px;">
				<p>在 IBM Cloud 中無法使用。</p>
			</td>
			<td style="width:80px;">
				<p>NA</p>
			</td>
			<td style="width:80px;">
				<p>是；雙重磁頭及控制器。</p>
			</td>
			<td style="width:96px;">
				<p>是；叢集解決方案。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可配置性</strong></p>
			</td>
			<td style="width:87px;">
				<p>磁碟數目及類型；RAID 層次</p>
			</td>
			<td style="width:95px;">
				<p>需要特定控制器。</p>
			</td>
			<td style="width:99px;">
				<p>CPU、記憶體、快取、磁碟數目和類型，以及 RAID 層次。</p>
			</td>
			<td style="width:80px;">
				<p>CPU、記憶體、快取、磁碟數目和類型，以及 RAID 層次。</p>
			</td>
			<td style="width:80px;">
				<p>TBD</p>
			</td>
			<td style="width:96px;">
				<p>CPU、記憶體、快取、磁碟數目和類型、SSD、快取、iSCSI 埠配置。多方承租戶 QOS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>災難回復及抄寫</strong></p>
			</td>
			<td style="width:87px;">
				<p>使用要抄寫的 vRA；無 SRA。</p>
			</td>
			<td style="width:95px;">
				<p>使用要抄寫的 vRA。</p>
			</td>
			<td style="width:99px;">
				<p>內建抄寫；沒有可用的 SRA。</p>
			</td>
			<td style="width:80px;">
				<p>可以使用要抄寫的 vRA、SnapMirror。</p>
			</td>
			<td style="width:80px;">
				<p>可以使用要抄寫的 vRA、SnapMirror、SnapVault。</p>
			</td>
			<td style="width:96px;">
				<p>支援 vRA 或 SRA；SDS 與實體 XIV 裝置之間的抄寫。</p>
				<p>支援 Snapshot；透過 IBM FlashCopy Manager 的應用程式回復。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可靠性</strong></p>
			</td>
			<td style="width:87px;">
				<p>不含 HA 的單一失敗點。</p>
			</td>
			<td style="width:95px;">
				<p>七個以上主機最多容忍三個主機故障。</p>
				<p>6.0 版已引進失敗網域。</p>
			</td>
			<td style="width:99px;">
				<p>單一失敗點（機殼及 RAID 控制器），且無 HA。</p>
			</td>
			<td style="width:80px;">
				<p>單一失敗點（機殼及 RAID 控制器），且無 HA。</p>
			</td>
			<td style="width:80px;">
				<p>高備援多路徑 I/O (MPIO) 連線。</p>
			</td>
			<td style="width:96px;">
				<p>高備援 iSCSI MPIO 連線：任何節點都可以管理叢集。</p>
			</td>
		</tr>
	</tbody>
</table>

表 2 文件鏈結：
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge：在客戶入口網站上無法使用 - 攜帶自己的解決方案。
  * [Data ONTAP 安裝及管理手冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP 快速設定手冊 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate：在客戶入口網站上無法使用 - 攜帶自己的解決方案。
  * [使用 IBM Spectrum Accelerate 系統 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

「表 3」提供多方承租戶環境中共用儲存空間的優缺點。

<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 3. VMware 共用儲存空間選項的優缺點</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>VMware 共用儲存空間（多方承租戶）</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>重要因素/儲存空間選項</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">區塊及檔案耐久性</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">區塊及檔案效能</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>類型</strong></p>
			</td>
			<td style="width:266px;">
				<p>SDS</p>
			</td>
			<td style="width:271px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>效能</strong></p>
			</td>
			<td style="width:266px;">
				<p>每個 GB 中提供 0.25、2、4 或 104 個 IOPS。</p>
				<p>可預測的儲存空間效能參數。</p>
				<p>可以將多個磁區分段在一起，以達到較高的 IOPS 及更多的傳輸量。</p>
			</td>
			<td style="width:271px;">
				<p>根據工作負載需求或價格點的用戶端佈建所需效能層次。</p>
				<p>&nbsp;</p>
				<p>可預測的儲存空間效能參數。</p>
				<p>可以將多個磁區分段在一起，以達到較高的 IOPS 及更多的傳輸量。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可擴充性</strong></p>
			</td>
			<td style="width:266px;">
				<p>磁區大小範圍是從 20 GB 到 12 TB。訂購後就無法調整大小。</p>
			</td>
			<td style="width:271px;">
				<p>磁區大小範圍是從 20 GB 到 12 TB。訂購後就無法調整大小。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>通訊協定</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI 及 NFS。</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI 及 NFS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>主機連線</strong></p>
			</td>
			<td style="width:266px;">
				<p>對於 iSCSI 最多有 8 個，而對於 NFS 最多有 64 個。</p>
			</td>
			<td style="width:271px;">
				<p>對於 iSCSI 最多有 8 個，而對於 NFS 最多有 64 個。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>使用案例</strong></p>
			</td>
			<td style="width:266px;">
				<p>第 1 層、第 2 層及第 3 層工作負載：</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 每個 GB 有 0.25 個 IOPS：低 I/O 強度。範例應用程式包括儲存信箱或部門層次檔案共用。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 每個 GB 有 2 個 IOPS：一般用途。範例應用程式包括管理支持小型資料庫的 Web 應用程式或 Hypervisor 的虛擬機器磁碟映像檔。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 每個 GB 有 4 個 IOPS：高 I/O 強度。範例應用程式包括交易式資料庫及其他效能相關資料庫。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 每個 GB 有 10 個 IOPS：高 I/O 強度。範例應用程式包括分析。</p>
			</td>
			<td style="width:271px;">
				<p>第 1 層、第 2 層及第 3 層工作負載：</p>
				<p>理論上，MPIO iSCSI 型儲存空間適合 I/O 密集應用程式，例如需要可預測效能層次的關聯式資料庫。儲存空間磁區的大小從 20 GB 到 12 TB，而且使用者可選取的 IOPS 範圍從 100 到 48,000 個 IOPS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>HA</strong></p>
			</td>
			<td style="width:266px;">
				<p>是，雙重磁頭及控制器。</p>
			</td>
			<td style="width:271px;">
				<p>是，雙重磁頭及控制器。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可配置性</strong></p>
			</td>
			<td style="width:266px;">
				<p>僅限大小及 IOPS。</p>
			</td>
			<td style="width:271px;">
				<p>僅限大小及 IOPS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>災難回復及抄寫</strong></p>
			</td>
			<td style="width:266px;">
				<p>提供的 Snapshot 及「抄寫」，這是透過 IBM Cloud Private Network 執行。可以在 VM 層次使用要抄寫的 vRA；無 SRA。</p>
			</td>
			<td style="width:271px;">
				<p>提供的 Snapshot 及「抄寫」，這是透過 IBM Cloud Private Network 執行。可以在 VM 層次使用要抄寫的 vRA；無 SRA。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>可靠性</strong></p>
			</td>
			<td style="width:266px;">
				<p>高備援、MPIO 連線、NFS 型檔案儲存空間已遞送 TCP/IP 連線。已啟用 Snapshot 及「抄寫」。</p>
			</td>
			<td style="width:271px;">
				<p>高備援、MPIO 連線、NFS 型檔案儲存空間已遞送 TCP/IP 連線。</p>
			</td>
		</tr>
	</tbody>
</table>

表 3 文件鏈結：
* [區塊儲存空間](/docs/infrastructure/BlockStorage/index.html)
* [檔案儲存空間](/docs/infrastructure/FileStorage/index.html)
