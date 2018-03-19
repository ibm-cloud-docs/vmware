---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 入門 

vSphere 6 を開始するには、以下を使用します。

## 環境と構成について理解

VMware ソリューションを最適化するには、VMware vSphere 環境にプライベート・ネットワーク VLAN およびパブリック (オプションで、必要な場合、パブリック・ポートを使用不可にできます) を使用することをお勧めします。このプロビジョニング・プロファイルにより、以下のレイヤー 2 のセグメント・トラフィック境界を使用できます。

|サンプル VLAN ID|説明|タイプ|追加詳細|
|---|---|---|---|
|VLAN1 - **1101**|管理、VxLAN|プライベート BCR|ネイティブの、タグ付けされていない VLAN。発注時に VMWare Host がデプロイされる、元のネイティブ VLAN|
|VLAN4 - **2200**|パブリック・インターネット・アクセス DMZ|パブリック FCR|ネイティブの、タグ付けされていない VLAN。発注時に VMWare Host がデプロイされる、元のネイティブ VLAN|
{: caption="表 1. プライベートおよびパブリックの VLAN の例" caption-side="top"}

## vSphere Server の注文
1. [{{site.data.keyword.slportal_full}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){: new_window} にログインします。
2. **「アカウント」>「注文」**をクリックします。
3. **「ベア・メタル・サーバー」**セクションで、**「月次」**をクリックします。
4. サーバーを選択します。最小要件については、VMware のサポート資料を参照してください。
  * 以下のサーバーが例として選択されました。**注:** 冗長性のために、デュアル・パブリック・アップリンクおよびプライベート・アップリンク (未結合) が必要です。VLAN を作成したデータ・センターが未結合アップリンクを持っていることを確認してください。
  * キャパシティー・クラスター (数量: 2)
    * サーバー構成: 「デュアル・プロセッサー・マルチ・コア・サーバー」セクションから、Intel Xeon v3 サーバーを選択します。
    * ソフトウェア: OS = vSphere Enterprise Plus 6
    * OS ストレージ: 2 x 1 TB SATA (RAID 1 として構成済み)
    * データ・ストレージ : 2 TB SATA か 1.2 TB SSD、または Endurance / Performance NFS SAN Storage をオーダーすることをお勧めします。
      * 他のストレージ・タイプに関心がある場合は、[VMware システムで使用するストレージ (Storage to use with VMware Systems)](select-storage-option-use-vmware.html) を参照してください。
      * アップリンク・ポートの速度: 1 Gbps デュアル・パブリックおよびプライベート・ネットワーク (未結合)
        * VMware vSAN ソリューションには、10 Gbps のアップリンクをお勧めします。
5. 新しい IBM Cloud データ・センター内に新規デプロイメントを作成する場合は、ステップ 6 に進んでください。拡張、または既存のデータ・センターへのデプロイメントの場合は、望ましいバックエンド BCR VLAN とフロントエンド FCR VLAN を選択してください。例えば、バックエンド BCR VLAN は 1101 で、フロントエンド FCR VLAN は 2200 など。**注:** 新規デプロイメント、または新規 DC への新規デプロイメントの場合は、サーバーをオーダーするときにバックエンド BCR VLAN とフロントエンド FCR VLAN が作成されます。
6. **「ホスト名」**と**「ドメイン」**を入力します。
7. オーダーを確認し、**「注文を確定する」**をクリックしてプロセスのプロビジョニングを開始します。

## vCenter Server の注文

vCenter は、Windows サーバーのアドオンです。この構成は、最大 20 台の vSphere Host まで拡大できます。より大規模な実装の場合は、vSphere クラスターへの直接の vCenter Server Appliance (VCSA) のデプロイメント ([vCenter Server Appliance (vCSA) のデプロイおよび構成](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)) をお勧めします。

vCenter がインストールされた仮想サーバーをオーダーするには、以下の手順を実行します。

1. {{site.data.keyword.slportal_short}}にログインします。
2. **「アカウント」>「注文」**をクリックします。
3. 「仮想サーバー」の下で、**月次**のベア・メタルまたは仮想サーバー (パブリック・ノード / プライベート・ノード) インスタンス (VSI) のいずれかをオーダーします。
  1. SoftLayer 仮想サーバー・インスタンス (VSI) を vCenter 6.0 で適格にするには、少なくとも **4 x 2.0 GHz コア**および **4 GB の RAM** にデプロイする必要があります。
  2. vCenter デプロイメントの推奨事項のリストについては、[VMware vCenter Server&trade; 6.0 Deployment Guide ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・外部リンク")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window} を参照してください。
4. 以下の情報を入力します。
  * 推奨の最小サーバー構成に基づく
    * vCPU コア構成: 4 x 2.0 GHz コア
    * RAM 構成: 12 GB RAM
    * ソフトウェア: OS = Windows Server 2012 R2 Standard Edition (64 ビット)
    * OS 固有のアドオン: vCenter 6
    * 第 1 ディスク : 1 x 100 GB (SAN)
    * 第 2 ディスク : 1 x  50 GB (SAN)
    * アップリンク・ポートの速度: 1 Gbps のパブリックおよびプライベート・ネットワーク・アップリンク

5. 新しい IBM Cloud データ・センターへの新規デプロイメントの場合は、以下のステップ 6 に進んでください。このデプロイメントが拡張、または既存のデータ・センターへのデプロイメントの場合は、望ましいバックエンド BCR VLAN とフロントエンド FCR VLAN を選択してください。この例では、バックエンド BCR VLAN は 1101 で、フロントエンド FCR VLAN は 2200 です。(完全に新規のデプロイメント、または新規 DC へのデプロイメントの場合は、サーバーをオーダーするときにバックエンド BCR VLAN とフロントエンド FCR VLAN が作成されます。
6. **「ホスト名」**と**「ドメイン」**を入力します。
7. オーダーを確認し、**「注文を確定する」**をクリックしてプロセスのプロビジョニングを開始します。

## ポータブル・パブリックおよびプライベート・サブネット / IP アドレスのオーダー

**注:** VLAN が完全にプロビジョンされていない場合は、先に進まないでください。

VMware ゲスト仮想計算機 (VM) と VMware ホスト・カーネル・ベースのトラフィックに対応するために、サブネットが使用されます。

1. コントロール・ポータルから、**「ネットワーク」>「IP 管理」>「サブネット」**をクリックします。
2. 画面右上の**「IP アドレスの注文」**をクリックします。
3. **「ポータブル・プライベート」**を選択します。
4. 該当する VLAN を選択します (例: bcr01.wdc04: 1101)。
5. **「続行」**をクリックします。
6. **「IP アドレスの注文」**フォームに入力します。
7. 画面右上の**「IP アドレスの注文」**をクリックします。
8. **「注文」**をクリックします。
9. 該当する VLAN (例: 1101、2200) ごとに、このプロセスに従います。
  1. VLAN について詳しくは、[VLAN 入門](/docs/infrastructure/vlans/getting-started.html)を参照してください。

|サブネット・タイプ|サブネット・サイズ|バインド済み VLAN|vSphere ホストの使用法|
|---|---|---|---|
|ポータブル - プライベート|/27 32 アドレス|**1101**|管理 VM|
|ポータブル - プライベート|/27 32 アドレス|**1101**|iSCSI および VMotion の VM カーネル・ポート|
|ポータブル - プライベート|/27 32 アドレス|**1101**|ゲスト VM のプライベート IP|
|ポータブル - パブリック|/27 32 アドレス|**2200**|ゲスト VM のパブリック IP (オプション)|
{: caption="表 2. サブネット" caption-side="top"}

### オプション – vSphere Host でのパブリック・インターフェースの使用不可化

vSphere パブリック・インターフェースを使用しない場合は、セキュリティー目的でそれらを使用不可にすることができます。

1. コントロール・ポータルから、**「デバイス」>「デバイス・リスト」**をクリックします。
2. vSphere Host の名前をクリックします。
3. 「構成」表をクリックし、「ネットワーク」セクションまでスクロールダウンします。
4. すべてのホストについて、該当する vSphere Host の eth1 と eth3 のペアごとに**「切断」**を選択します。

これは、[{{site.data.keyword.slapi_full}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window} を介して実行することもできます。

## vSphere データ・センター・クラスターの作成および構成 <!-- create and configure should be separate tasks-->

vCenter Server にログインし、vSphere Cluster を構成することができます。

1. コントロール・ポータルから、**「デバイス」>「デバイス・リスト」**をクリックします。
2. ご使用の vCenter デバイスを見つけ、その名前をクリックします。
3. **「デバイスの詳細」**画面で、サーバーの**「ネットワーク」**セクションまでスクロールダウンし、**「プライベート IP アドレス」**をメモします。
4. **「デバイスの詳細」**画面をスクロールダウンし、Windows OS と vCenter ソフトウェア両方の**「パスワード」**をメモします。
5. Microsoft リモート・デスクトップ (RDP) セッションを開き、パブリック IP アドレスを介して vCenter Server に接続します。
6. ステップ 4 で取得したパスワードを使用してログインします。**注:** プライベート IP アドレスを使用して vCenter にアクセスする場合は、IBM Cloud へのアクティブな VPN 接続が必要になります。VPN アクセスについて詳しくは、[IBM Cloud インフラストラクチャーのプライベート・ネットワークへのアクセスの有効化 (Enable access to the IBM Cloud infrastructure private network) ](/docs/customer-portal/getting-started.html#enable-private-network)を参照してください。
7. 従来型の [vSphere Client ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window} をダウンロードするか、リンク `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/` を介して vSphere Web クライアントを使用します。
8. ステップ 3 と 4 で取得した IP アドレスとパスワードを使用して vCenter にログインします。
9. 左側のペインで vCenter サーバーの名前を右クリックし、**「新規データ・センター (New Datacenter)」**を選択します。
10. データ・センターの適切な名前を入力します。
11. データ・センターを右クリックし、**「新規クラスター (New Cluster)」**を選択します。
12. クラスター名を入力します。この時点では、クラスター機構、vSphere HA、または vSphere DRS をオンにしないでください。
13. **「次へ (Next)」**をクリックします。
14. **「EVC」**は無効のままにし、**「次へ (Next)」**をクリックします。
15. _「デフォルトでスワップ・ファイルを仮想マシンと同じディレクトリーに保管する (default to store the swapfile in the same directory as the virtual machine)」_を受け入れ、**「次へ (Next)」**をクリックします。
16. **「完了 (Finish)」**をクリックしてクラスターを完了します。
17. 作成したばかりの新規クラスターを右クリックし、**「ホストの追加 (Add Host)」**を選択します。
18. いずれかの vSphere ホストの　IP アドレスまたはホスト名を入力し、**「ユーザー名 (Username)」**フィールドに**「Root」**、**「パスワード (Password)」**フィールドにホストのパスワードを入力します。
19. ホスト要約、ライセンスの割り当て、およびロックダウン・モードの画面で**「次へ (Next)」**をクリックし、**「完了 (Finish)」**をクリックしてクラスターへのホストの追加を完了します。
20. クラスター内の他の vSphere ホストごとに、ステップ 18 と 19 を繰り返します。完了すると、新規クラスターの下にそれぞれの vSphere ホストが表示されます。

### vSphere Host のための基本ネットワーク構成体の構成

クラスター内の vSphere Host の基本構成体を構成するには、以下の手順を実行します。

1. 最初の vSphere Host を選択し、**「構成 (Configuration)」**タブをクリックします。
2. **「ハードウェア (Hardware)」**セクションの下で、**「ネットワーキング (Networking)」**を選択します。vmnic0 の vSwitch0 が既にあるはずです。vSwitch0 の横の**「プロパティー (Properties)」**をクリックします。
3. **「vSwitch プロパティー (vSwitch Properties)」**ウィンドウで**「ネットワーク・アダプター (Network Adapters)」**を選択し、**「追加 (Add)」**ボタンをクリックします。
4. vmnic2 を選択して vSwitch0 に追加し、**「次へ (Next)」**をクリックします。
5. 両方の vmnic が**「アクティブ・アダプター (Active Adapters)」**であることを確認し、**「次へ (Next)」 **をクリックします。
6. **「完了 (Finish)」**をクリックします。
7. **「ポート (Ports)」**タブをクリックして vSwitch が強調表示されていることを確認し、**「編集 (Edit)」**をクリックします。
8. **「一般 (General)」**タブをクリックし、**「MTU」**を 9000 (ジャンボ・フレーム) に変更します。
9. **「NIC チーミング (NIC Teaming)」**タブをクリックし、ロード・バランシングを**「IP ハッシュに基づいたルート (Route Based on IP hash)」**に変更し、**「OK」**をクリックします。
10. ステップ 1 から 8 を使用して、クラスター内の他の vSphere Host の vmnic を構成します。

次に、vMotion 用ポート・グループを追加する必要があります。グループは、仮想標準スイッチ (VSS) または仮想分散スイッチ (VDS) として作成できます。この例の目的のために、VSS スイッチを作成します。

1. **「構成 (Configuration)」**タブを選択し、**「ネットワーキング (Networking)」**を選択します。
2. vSwitch0 の**「プロパティー... (Properties...)｣**をクリックします。
3. **「追加... (Add...)」**をクリックしてポート・グループを作成します。
4. **「VMkernel」**を選択し、**「次へ (Next)｣**をクリックします。
5. ポート・グループのプロパティーに、以下の情報を入力します。
  * **ネットワーク・ラベル:** ポート・グループの適切な名前。
  * **VLAN ID (オプション):** vMotion トラフィックの VLAN ID (この例では 1101)。この VLAN ID により、VMware は特定の VLAN のトラフィックにタグ付けすることができます。
  * **「このポート・グループを vMotion で使用 (Use this port group for vMotion)｣**を選択します。
6. **「次へ (Next)」**をクリックします。
7. VLAN の**「ポータブル IP アドレス (Portable IP address)｣**を入力します。(SoftLayer ポータルから**「ネットワーク」>「IP 管理」>「VLAN」**を選択して、ポータブル IP アドレスを取得できます。正しい VLAN を選択すると、**「サブネット (Subnets)」**の下にポータブル IP アドレスの範囲が表示されます。使用可能なポータブル IP アドレスがない場合や現在のプールを使い尽くした場合は、「プライベート・サブネット / IP アドレスのオーダー (Order Private Subnets / IP Addresses)」の手順に従って、追加のポータブル IP アドレスをオーダーしてください。
8. **「次へ (Next)」**をクリックし、次に**「完了 (Finish)」**をクリックして完了します。

VM データ・トラフィック用のポート・グループを作成するには、以下の手順を実行します。

1. vSwitch0 の**「プロパティー... (Properties...)」**をクリックし、**「追加、仮想マシン (Add, Virtual Machine)」**を選択します。
2. **ポート・グループのプロパティー**に、以下の情報を入力します。
  * **ネットワーク・ラベル:** ポート・グループの名前 (例えば、VM Data) を入力します。
  * **VLAN ID (オプション):** VLAN ID を入力します。この例では、1101 を使用しています。この VLAN ID により、VMware は VLAN のトラフィックにタグ付けすることができます。

### オプション - アドオン VMware ライセンス (NSX、vRealize、vSAN など) のインストール

これで VMware 環境が稼働中になったので、追加構成、ゲスト VM、または VMware アドオンのデプロイメントを続行できます。VMware アドオンのライセンスは、IBM Cloud コントロール・ポータルから購入し、vCenter Console を介して追加することもできます。VMware アドオン・ライセンスのオーダーについて詳しくは、[VMware vSphere 6 ライセンスのオーダーおよび管理 (VMware vSphere 6 Ordering and Managing Licenses)](vmware-vsphere-6-ordering-and-managing-licenses.html) を参照してください。

## 次のステップ
これで、IBM Cloud データ・センター内で稼働する基本的な単一サイトの VMware 環境が準備できました。基本構成にはローカル・データ・ストアしか含まれていないため、VMware DRS、HA、Storage DRS、およびファイアウォールなどのフィーチャーを含まない、単純化された構成になります。

詳細情報については、[FAQ: VMware](vmware-faq.html) を参照してください。 
