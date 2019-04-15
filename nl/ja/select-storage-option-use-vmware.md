---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# VMware システムで使用するストレージ
{: #vmware-storage}

ストレージに関するオプションは、いくつかあります。専用、共有、またはお客様所有のストレージ・ソリューションを選択できます。以下の情報を参考にして、ワークロードに最適なストレージ・ソリューションを決定します。

表 1 は、ストレージ層と対応するワークロードを示しています。
<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 1. ストレージ層</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>層 1</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>層 2</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>層 3</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>使用対象業務</strong></p>
			</td>
			<td style="width:160px;">
				<p>高性能および/または高可用性の実動アプリケーション、データベース、およびデータ</p>
			</td>
			<td style="width:160px;">
				<p>非ミッション・クリティカルのテストおよび開発アプリケーション、データベース、およびデータ</p>
			</td>
			<td style="width:160px;">
				<p>非ミッション・クリティカルのデータ・ストレージ、バックアップ、およびアーカイブ</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>パフォーマンス</strong></p>
			</td>
			<td style="width:160px;">
				<p>高 (SSD、SAS)</p>
			</td>
			<td style="width:160px;">
				<p>中 (SAS、SATA)</p>
			</td>
			<td style="width:160px;">
				<p>低 (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>保証された IOPS</strong></p>
			</td>
			<td style="width:160px;">
				<p>あり</p>
			</td>
			<td style="width:160px;">
				<p>なし</p>
			</td>
			<td style="width:160px;">
				<p>なし</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>高可用性 (HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>あり</p>
			</td>
			<td style="width:160px;">
				<p>なし</p>
			</td>
			<td style="width:160px;">
				<p>なし</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>レプリケーション</strong></p>
			</td>
			<td style="width:160px;">
				<p>あり</p>
			</td>
			<td style="width:160px;">
				<p>あり</p>
			</td>
			<td style="width:160px;">
				<p>なし</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>スナップショット</strong></p>
			</td>
			<td style="width:160px;">
				<p>あり</p>
			</td>
			<td style="width:160px;">
				<p>なし</p>
			</td>
			<td style="width:160px;">
				<p>なし</p>
			</td>
		</tr>
	</tbody>
</table>


## 専用および共有の VMware ストレージ・オプション

複数のストレージ・オプションから選択できます。専用ストレージの場合は、ローカル・ディスク・オプション、VSAN、または QuantaStor を選択できます。共有ストレージの場合は、エンデュランス・ストレージまたはパフォーマンス・ストレージを選択できます。お客様所有のストレージを使用する場合は、NetApp OnTap Edge、NetApp Private Storage (NPS)、{{site.data.keyword.IBM}} Spectrum Accelerate、Software Defined Storage など、いくつかの「専用」のオプションがあります。表 2 と表 3 では、分かりやすく、オプションを横並びにして比較しています。

## 専用ストレージ・オプション

以下に示すように、単一テナント環境で VMware に接続するためのストレージには複数のオプションがあります。 

* ローカル
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## ローカル・ストレージ

ESX とともに、{{site.data.keyword.baremetal_short}} を IBM Cloud カスタマー・ポータルから注文し、必要なディスク [SATA、シリアル接続 SCSI (SA SCSI)、または SSD] を選択します。
 
お客様所有の ESX ライセンスを使用することもできますが、サポートでチケットをオープンして変更を通知する必要があります。

* 推奨されるワークロード: 層 3
* パフォーマンス: 限定的: RAID とディスク・タイプに依存します。SSD では、パフォーマンス向上のためにコストが増加します。
* スケーラビリティー : シャーシ内のドライブ・スロットの数に制限されます。
* プロトコル: 適用外
* コスト: 低い資本支出 (CAPEX) と運用支出 (OPEX)
* HA: 使用不可
* レプリケーション: [vSphere Replication 仮想アプライアンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* 信頼性 : 複数の Single Point of Failure



## vSAN [1]

* 推奨されるワークロード: 層 1
* パフォーマンス: ホスト構成に応じて、ホスト当たり 90 K を超える IOPS
* スケーラビリティー: v5.5 では最大 2 TB の仮想マシン・ディスク (VMDK)。v6.0 では、最大 62 TB の VMDK。より多くのノードでスケールアウトします。
* プロトコル: プロプラエタリー
* コスト: CAPEX と OPEX のどちらも中程度です
* HA: ホストおよびディスクの両方の障害でサポートされます。障害ドメインは、VMware の v6 からサポートされています。
* レプリケーション: [vSphere Replication 仮想アプライアンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* レプリケーションと災害復旧:
    1. VMware vCenter Server 経由の VM バックアップのスケジュール
    2. VM スナップショットの作成
    3. VM に関するデータ DE の作成
    4. VM のリストア
 * 信頼性: 7 つ以上のホストで最大 3 つのホスト障害に耐えられます。障害ドメインは、VMware の v6 で導入されました。   

[1] vSAN 6.2 の新機能の拡張クラスターにより、同じデータ・センター内の異なるポッドにホストを配置できます (検証テストが進行中)。<!-- Should this in progress mention be removed? -->

vSAN 5.5 は、BYOL (ライセンスの持ち込み) でのみ使用可能です。これは、Avago LSI MegaRAID SAS 9361-8i ディスク・コントローラーを使用する場合にのみ、VMware によってサポートされます。

vSAN 6.0 は、CPU ライセンス請求ベースで IBM Cloud ポータルから直接使用可能です。

## QuantaStor

[OSNexus Solution Design Guide ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} を利用して、VMware を QuantaStor に接続することができます。

* 推奨されるワークロード: 層 2 および層 3 
* パフォーマンス: ドライブ数、RAID、ディスク使用 (iSCSI または NFS) によって変わります  
* スケーラビリティー: v3 シングル・フレームは 128 TB をサポートします。スケールアップおよびスケールアウトは行いません。 
* プロトコル: iSCSI、NFS、および SMB 
* コスト: CAPEX と OPEX のどちらも高くなります 
* HA: 使用不可  
* レプリケーション: 組み込みのレプリケーション機能。SRA は使用できません。vSphere Replication アプライアンスも使用できます。 
* 信頼性: エンクロージャーおよび RAID コントローラーの Single Point of Failure。


<a name="NetApp"></a>
## NetApp Data OnTap Edge

NetApp または IBM から NetApp デバイスの購入が必要です。{{site.data.keyword.BluSoftlayer}} データ・センターの {{site.data.keyword.baremetal_short}} にそれをインストールする必要があります。

VMware と NetApp の接続について詳しくは、以下のリンクを参照してください。
* [NetApp ONTAP Select ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: Build a data center on a server with NetApp fundamentals ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* 推奨されるワークロード: 層 2 および層 3
* パフォーマンス: ドライブ数と RAID によって変わります
* スケーラビリティー: 110 TB をサポートします。スケールアウトは行いません。
* プロトコル: iSCSI、NFS、および SMB
* コスト: CAPEX と OPEX のどちらも中程度です
* HA: 使用不可
* レプリケーション: SnapMirror をサポートします。[vRealize Automation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.vmware.com/products/vrealize-automation){: new_window} (vRA) を使用しても行えます。
* 信頼性: エンクロージャーおよび RAID コントローラーの Single Point of Failure。

<a name="NPS"></a>
## NetApp Private Storage

NetApp または IBM から NetApp デバイスの購入が必要です。これを IBM Cloud データ・センターの近くのコロケーション・サイトの 1 つにインストールし、Direct Link コロケーションまたは Direct Link クラウドを使用して接続する必要があります。

VMware と NetApp の接続について詳しくは、以下のリンクを参照してください。 
* [NetApp Private Storage for IBM Cloud ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Solution brief: NetApp Private Storage for IBM Cloud ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* 推奨されるワークロード: 層 1
* パフォーマンス : NetApp モデルに依存します
* スケーラビリティー: 容量と IOPS の向上のためにドライブおよびフレームの追加をサポートします
* プロトコル: iSCSI、NFS、および SMB
* コスト: CAPEX と OPEX のどちらも高くなります
* HA: デュアル・ヘッドおよびコントローラー
* レプリケーション: SnapVault および SnapMirror をサポートします。[vRealize Automation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.vmware.com/products/vrealize-automation) を使用しても行えます。
* 信頼性: 高い冗長性と MPIO サポート

<a name="IBM"></a>
## IBM Spectrum Accelerate

IBM Spectrum Accelerate 専用ストレージのオプションは、IBM Cloud カスタマー・ポータルでは使用できません。<!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* 推奨されるワークロード: 層 1
* パフォーマンス: ディスク数、SSD (オプション)、およびそれぞれの「ノード」 VM に与えられたメモリー量によって異なります。
* スケーラビリティー: 約 8 TB から 325 TB まで使用可能スペースを拡張できます
  * 最小容量: 3 VM x 6 ドライブ
  * 最大容量: 15 VM x 12 ドライブ
  * IBM Hyper-Scale Manager を使用して最大 144 の仮想アレイおよび 40 PB を超える使用可能スペースまで拡張できます
  * ノードの追加による、中断を伴わない容量の拡張
  * ノードごとに 1 x 500 または 800 GB の SSD がサポートされます
* プロトコル: iSCSI のみ
* コスト: 価格設定モデルと、ノードにデプロイされている物理マシンによって異なります。CAPEX は高くなります。OPEX は、ライセンスに応じて中程度から低い範囲になります。
  * 使用可能容量のバイナリー (TIB) 単位で価格設定されます
  * 特定のハードウェア構成には関連付けられていません。例: 200 TiB のライセンスをデプロイするには、1 個の 200 TiB インスタンス、2 個の 100 TiB インスタンス、または 4 個の 50 TiB インスタンスといった、さまざまな方法があります。
  * 永久ライセンス [1 年間のサブスクリプションおよびサービス (S&S) を含む] と、月次ライセンス (S&S を含む) の 2 つの方法があります
* HA: クラスター・ソリューション
* レプリケーション: [vRealize Automation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.vmware.com/products/vrealize-automation){: new_window}、
 または SRA を使用して実現します。SRA は、VMware の Site Recovery Manager (SRM) で物理的な IBM XIV から複製するために使用できます。
  * [vSphere Replication ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [IBM XIV Gen3 Storage System 向けの VMware vCenter Site Recovery Manager バージョン 5.x のガイドライン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* 信頼性: 高い冗長性と MPIO サポート。使用可能なすべてのノードでクラスターを管理できます。以下の機能は、ハードウェア・ベースの IBM XIV で IBM Spectrum Accelerate によってこの時点でサポートされていません。
  * 3 つのサイトのミラーリング
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG v6
  * 6 TB ディスク・ドライブ
  * Storage Management Initiative Specifications (SMI-S) 1.6
  * Data at Rest (保存されたデータ) の暗号化
  * vStorage for API Array Integration (VAAI) (Virtual Volumes (VVol) と並んで利用可能な場合)
  * vCenter Operations Manager (VCop)
  * IBM XIV Storage System の詳細については、[IBM XIV Storage System のプラットフォームおよびアプリケーションの統合 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window} を参照してください。

## 共有ストレージ・オプション

マルチテナント環境で VMware に接続するために使用できるストレージ・オプションには、ブロック・ストレージとファイル・ストレージの 2 つがあります。

### ブロック・ストレージとファイル・ストレージ

ESX とともに、{{site.data.keyword.baremetal_short}} を IBM Cloud カスタマー・ポータルから注文します。

VMware では、ユーザー名、パスワード (CHAP 認証の場合)、およびホスト IQN の、3 つの<!--**Authorize** (**Block** or **File**) **Storage SoftLayer** -->事前定義値が、**「ホスト・デバイス詳細ストレージ (Host Device Details Storage)」**タブで提供されます。

ブロック・ストレージのプロビジョンについて詳しくは、[ブロック・ストレージのプロビジョンと管理 (Provisioning and managing block storage)](/docs/infrastructure/BlockStorage/provisioning-block_storage.html) を参照してください。

ファイル・ストレージのプロビジョンについて詳しくは、[IBM File Storage for IBM Cloud のプロビジョンと管理 (Provisioning and Managing IBM File Storage for IBM Cloud)](/docs/infrastructure/FileStorage/provisioning-file-storage.html) を参照してください。

* 推奨されるワークロード: 層 1、層 2、および層 3
* パフォーマンスをプロビジョンする 2 つの方法:
    1. エンデュランス IOPS 層: 0.25、2、4、または 104 IOPS/GB で利用可能
    2. パフォーマンス割り振り IOPS: 容量とは別に、IOPS を指定します。パフォーマンス要件が明確なワークロードに推奨されます。
    * 予測可能なストレージ・パフォーマンス・パラメーター
    * より高い IOPS とスループットを実現するために、複数のボリュームを一緒にストライピングできます
* 待ち時間 <10 ms。最大 48,000 IOPS
* スケーラビリティー: 20 GB から 12 TB まで注文できます。注文後にボリュームのサイズを変更することはできません。
* プロトコル: iSCSI および NFS
* コスト: CAPEX と OPEX のどちらも高くなります。CAPEX は、同じサイズの SAN の 10 倍かかります。
* HA: デュアル・ヘッドおよびコントローラー
* レプリケーション: IBM Cloud プライベート・ネットワークを介して提供されるスナップショットとレプリケーション。[vRealize Automation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.vmware.com/products/vrealize-automation){: new_window} を使用しても行えますが、SRA は使用できません。
* 信頼性: 高い冗長性。iSCSI は MPIO 接続を使用します。NFS ベースのストレージは、TCP/IP 接続を介してルーティングされます。スナップショットとレプリケーションが使用可能です。

表 2 は、単一テナント環境における専用ストレージのメリットとデメリットを示しています。

<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 2. VMware 専用ストレージ・オプションのメリットとデメリット</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; 専用ストレージ (単一テナント)</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>キー要因/ ストレージ・オプション</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>ローカル</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>Virtual SAN</p>
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
				<p><strong>タイプ</strong></p>
			</td>
			<td style="width:87px;">
				<p>ローカル</p>
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
				<p>モノリシック</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>パフォーマンス</strong></p>
			</td>
			<td style="width:87px;">
				<p>SSD /SA-SCSI スペックに基づきます。RAID 5/10 を使用して読み取り/書き込みの向上を図ることもできます。</p>
			</td>
			<td style="width:95px;">
				<p>ホスト構成に応じて、ホスト当たり 90 K を超える IOPS。ホスト当たり 100 の VM、クラスター当たり 32 ホスト、クラスター当たり 3,200 VM、2,048 のみの保護 (v5.5)</p>
				<p>最大 20K IOPS、ホスト当たり 200 の VM、クラスター当たり 64 ホスト、およびクラスター当たり 6,000 の保護 VM (v6.0)。</p>
			</td>
			<td style="width:99px;">
				<p>選択されたディスクのタイプと数のほか、RAID 構成、および iSCSI または NFS の使用によって変わります。</p>
			</td>
			<td style="width:80px;">
				<p>選択されたディスクのタイプと数のほか、RAID 構成アクションによって変わります。</p>
			</td>
			<td style="width:80px;">
				<p>モデルによって異なります。</p>
			</td>
			<td style="width:96px;">
				<p>選択されたディスクのタイプと数のほか、RAID 構成、ハイパーバイザー・ノードごとの SSD ディスクの使用 (オプション) によって変わります。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>スケーラビリティー</strong></p>
			</td>
			<td style="width:87px;">
				<p>サイズとディスク入出力スループットの増加は制限されます。</p>
			</td>
			<td style="width:95px;">
				<p>v5.5 では最大 2 TB の仮想マシン・ディスク (VMDK)。v6.0 では、最大 62 TB。</p>
				<p>より多くのノードでスケールアウトします。</p>
			</td>
			<td style="width:99px;">
				<p>最大 128 TB のシングル QS (3.x)。スケールアップおよびスケールアウトは行いません。</p>
			</td>
			<td style="width:80px;">
				<p>最大 10 TB。スケールアウトは行いません。</p>
			</td>
			<td style="width:80px;">
				<p>あり。容量および IOPS のためにディスク・シェルフを追加します。</p>
			</td>
			<td style="width:96px;">
				<p>約 8 TB から 325 TB まで使用可能スペースを拡張できます。</p>
				<p>最小容量は 3 VM x 6 ドライブです。</p>
				<p>最大容量は 15 VM x 12 ドライブです。</p>
				<p>IBM Hyper-Scale Manager によって最大 144 の仮想アレイおよび 40 PB を超える使用可能スペースまで拡張できます。</p>
				<p>ノードの追加による、中断を伴わない容量の拡張。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>プロトコル</strong></p>
			</td>
			<td style="width:87px;">
				<p>適用外</p>
			</td>
			<td style="width:95px;">
				<p>プロプラエタリー</p>
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
				<p><strong>ユース・ケース</strong></p>
			</td>
			<td style="width:87px;">
				<p>層 2 および層 3 のワークロード</p>
			</td>
			<td style="width:95px;">
				<p>層 1 のワークロード</p>
			</td>
			<td style="width:99px;">
				<p>層 2 および層 3 のワークロード</p>
			</td>
			<td style="width:80px;">
				<p>層 2 および層 3 のワークロード</p>
			</td>
			<td style="width:80px;">
				<p>層 1 のワークロード</p>
			</td>
			<td style="width:96px;">
				<p>層 1 のワークロード</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>高可用性 (HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>RAID で使用可能</p>
			</td>
			<td style="width:95px;">
				<p>あり。ホストおよびディスクの障害、障害ドメイン (v6.0)</p>
			</td>
			<td style="width:99px;">
				<p>IBM Cloud では利用不可。</p>
			</td>
			<td style="width:80px;">
				<p>適用外</p>
			</td>
			<td style="width:80px;">
				<p>あり。デュアル・ヘッドおよびコントローラー。</p>
			</td>
			<td style="width:96px;">
				<p>あり。クラスター・ソリューション。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>構成可能性</strong></p>
			</td>
			<td style="width:87px;">
				<p>ディスクの数とタイプ、RAID レベル</p>
			</td>
			<td style="width:95px;">
				<p>特定のコントローラーが必要です。</p>
			</td>
			<td style="width:99px;">
				<p>CPU、メモリー、キャッシュ、ディスクの数とタイプ、および RAID レベル。</p>
			</td>
			<td style="width:80px;">
				<p>CPU、メモリー、キャッシュ、ディスクの数とタイプ、および RAID レベル。</p>
			</td>
			<td style="width:80px;">
				<p>(未定)</p>
			</td>
			<td style="width:96px;">
				<p>CPU、メモリー、キャッシュ、ディスクの数とタイプ、SSD、キャッシング、iSCSI ポート構成。マルチテナンシー QOS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>災害復旧およびレプリケーション</strong></p>
			</td>
			<td style="width:87px;">
				<p>vRA を使用して複製します。SRA は使用できません</p>
			</td>
			<td style="width:95px;">
				<p>vRA を使用して複製します。</p>
			</td>
			<td style="width:99px;">
				<p>組み込みのレプリケーション。SRA は使用できません。</p>
			</td>
			<td style="width:80px;">
				<p>vRA を使用して複製できます。SnapMirror がサポートされています。</p>
			</td>
			<td style="width:80px;">
				<p>vRA を使用して複製できます。SnapMirror、SnapVault がサポートされています。</p>
			</td>
			<td style="width:96px;">
				<p>vRA または SRA がサポートされています。SDS デバイスおよび/または物理 XIV デバイスの間のレプリケーション。</p>
				<p>スナップショットがサポートされています。IBM FlashCopy Manager によるアプリケーション・リカバリー。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>信頼性</strong></p>
			</td>
			<td style="width:87px;">
				<p>Single Point of Failure。HA はありません。</p>
			</td>
			<td style="width:95px;">
				<p>7 つ以上のホストで最大 3 つのホスト障害に耐えられます。</p>
				<p>障害のドメインは、v6.0 で導入されています。</p>
			</td>
			<td style="width:99px;">
				<p>Single Point of Failure (エンクロージャーと RAID コントローラー)。HA はありません。</p>
			</td>
			<td style="width:80px;">
				<p>Single Point of Failure (エンクロージャーと RAID コントローラー)。HA はありません。</p>
			</td>
			<td style="width:80px;">
				<p>冗長度が高いマルチパス入出力 (MPIO) 接続。</p>
			</td>
			<td style="width:96px;">
				<p>冗長度が高い iSCSI MPIO 接続。すべてのノードでクラスターを管理できます。</p>
			</td>
		</tr>
	</tbody>
</table>

表 2 の資料リンク:
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge: カスタマー・ポータルでは使用できません。お客様所有のソリューションとして使用します。
  * [Data ONTAP Installation and Administration Guide ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP Express Setup Guide ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate: カスタマー・ポータルでは使用できません。お客様所有のソリューションとして使用します。
  * [IBM Spectrum Accelerate システムでの作業 (Working with an IBM Spectrum Accelerate system) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

表 3 は、マルチテナント環境における共有ストレージのメリットとデメリットを示しています。

<table border="1" cellpadding="0" cellspacing="0">
        <caption>表 3. VMware 共有ストレージ・オプションのメリットとデメリット</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>VMware 共有ストレージ (マルチテナント)</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>キー要因/ ストレージ・オプション</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">ブロックとファイルのエンデュランス</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">ブロックとファイルのパフォーマンス</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>タイプ</strong></p>
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
				<p><strong>パフォーマンス</strong></p>
			</td>
			<td style="width:266px;">
				<p>0.25、2、4、または 104 IOPS/GB で利用可能</p>
				<p>予測可能なストレージ・パフォーマンス・パラメーター。</p>
				<p>より高い IOPS とスループットを実現するために、複数のボリュームを一緒にストライピングできます</p>
			</td>
			<td style="width:271px;">
				<p>お客様が、ワークロードのニーズまたは価格ポイントに基づいて、必要なパフォーマンス・レベルをプロビジョンします</p>
				<p>&nbsp;</p>
				<p>予測可能なストレージ・パフォーマンス・パラメーター。</p>
				<p>より高い IOPS とスループットを実現するために、複数のボリュームを一緒にストライピングできます</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>スケーラビリティー</strong></p>
			</td>
			<td style="width:266px;">
				<p>ボリューム・サイズの範囲は 20 GB から 12 TB です。一度注文したら、サイズ変更できません。</p>
			</td>
			<td style="width:271px;">
				<p>ボリューム・サイズの範囲は 20 GB から 12 TB です。一度注文したら、サイズ変更できません。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>プロトコル</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI および NFS。</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI および NFS。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>ホスト接続</strong></p>
			</td>
			<td style="width:266px;">
				<p>最大で iSCSI の場合は 8、NFS の場合は 64。</p>
			</td>
			<td style="width:271px;">
				<p>最大で iSCSI の場合は 8、NFS の場合は 64。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>ユース・ケース</strong></p>
			</td>
			<td style="width:266px;">
				<p>層 1、層 2、および層 3 のワークロード:</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 0.25 IOPS/GB: 低い入出力集中度。アプリケーションの例として、メールボックスの保管や部門レベルのファイル共有が挙げられます。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 2 IOPS/GB: 汎用。アプリケーションの例として、Web アプリケーションをバッキングする小規模なデータベースのホスティングや、ハイパーバイザーの仮想マシン・ディスク・イメージが挙げられます。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 4 IOPS/GB: 高い入出力集中度。アプリケーションの例として、トランザクション・データベースやその他の高いパフォーマンスを必要とするデータベースが挙げられます。</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 10 IOPS/GB: 高い入出力集中度。アプリケーションの例として、分析が挙げられます。</p>
			</td>
			<td style="width:271px;">
				<p>層 1、層 2、および層 3 のワークロード:</p>
				<p>MPIO iSCSI ベースのストレージは、予測可能なパフォーマンス・レベルを必要とするリレーショナル・データベースなどの入出力集中型アプリケーションに適しています。ストレージ・ボリュームのサイズは、20 GB から 12 TB で、ユーザーが選択可能な IOPS の範囲は、100 から 48,000 IOPS です。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>HA</strong></p>
			</td>
			<td style="width:266px;">
				<p>あり。デュアル・ヘッドおよびコントローラー。</p>
			</td>
			<td style="width:271px;">
				<p>あり。デュアル・ヘッドおよびコントローラー。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>構成可能性</strong></p>
			</td>
			<td style="width:266px;">
				<p>サイズと IOPS のみ。</p>
			</td>
			<td style="width:271px;">
				<p>サイズと IOPS のみ。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>災害復旧およびレプリケーション</strong></p>
			</td>
			<td style="width:266px;">
				<p>スナップショットとレプリケーションが提供されます。IBM Cloud プライベート・ネットワークを介して行われます。vRAを使用して、VM レベルで複製できます。SRA は使用できません。</p>
			</td>
			<td style="width:271px;">
				<p>スナップショットとレプリケーションが提供されます。IBM Cloud プライベート・ネットワークを介して行われます。vRAを使用して、VM レベルで複製できます。SRA は使用できません。</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>信頼性</strong></p>
			</td>
			<td style="width:266px;">
				<p>高い冗長性。MPIO 接続。NFS ベースのファイル・ストレージは、TCP/IP 接続を介してルーティングされます。スナップショットとレプリケーションが使用可能です。</p>
			</td>
			<td style="width:271px;">
				<p>高い冗長性。MPIO 接続。NFS ベースのファイル・ストレージは、TCP/IP 接続を介してルーティングされます。</p>
			</td>
		</tr>
	</tbody>
</table>

表 3 の資料リンク:
* [ブロック・ストレージ](/docs/infrastructure/BlockStorage/index.html)
* [ファイル・ストレージ](/docs/infrastructure/FileStorage/index.html)
