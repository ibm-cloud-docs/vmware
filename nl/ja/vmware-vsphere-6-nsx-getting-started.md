---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 NSX 入門 

NSX は、ご使用のインフラストラクチャーに適用するライセンス資格としてデプロイされます。{{site.data.keyword.BluSoftlayer_full}} は、プロセッサーごとにライセンスを提供します (CPU 当たりのコアの数で価格設定が変わることはありません)。NSX ライセンスは、NSX コンポーネント (管理プレーン、制御プレーン、またはデータ・プレーン) を使用するすべてのサーバーに必要です。NSX は、追加のネットワーキング機能をプラットフォームに追加します。システム・セキュリティーやテナント・セグメンテーションのため、および複数のプロバイダーにわたる、またはオンプレミスのプライベート・クラウドから拡張するハイブリッド・クラウド環境のための堅固なオーバーレイ・ネットワークを作成できます。
{:shortdesc}

RESTful API を介した自動化のサポートによって、ご使用環境にファイアウォール、ロード・バランシング、VPN、NAT サービス、VXLAN ベースのマイクロ・セグメンテーションを追加できます。

## ライセンスの追加
ライセンスは、以下のプロセスを使用してサーバーに追加されます。
1. vCenter Client により vCenter Server にログインします。
* **「管理 (Administration)」**の下で**「ライセンス (Licensing)」**をクリックします。
* **「ソリューション (Solutions)」**をクリックします。
* 製品リストから、**「VMware NSX for vSphere」**をクリックします。
* **「ライセンス・キー (License Key)」**または**「新規ライセンス・キーの入力 (Enter New license key)｣**をクリックします。
* **「OK」**をクリックします。

## NSX のインストール

1. NSX Manager をデプロイします。
* NSX Manager を vCenter Server に登録します。
* vSphere Web Client は、NSX Manager を介して NSX Controller インスタンスをデプロイします。
* NSX Manager を使用してクラスター内のホストに VIB をインストールして、vSphere Host を準備します。
* 適用可能なすべてのホストに NSX Controller がデプロイされたら、Edge ゲートウェイ、ロード・バランサー、およびファイアウォールなどの NSX コンポーネントを定義して構成します。

## デプロイメントに関する考慮事項

ソリューションで NSX を使用可能にするには、標準の計算ノードに加え、追加の vSphere ノードを使用する必要があります。

**NSX Manager**<br />
管理クラスター上の IBM Informix Virtual Appliance は、vCenter と 1:1 の関係を持っています。通常の HA vSphere 機能が推奨されています。NSX Manager には、スケジュール済み / オンデマンドのバックアップ機能が含まれており、vCenter、コントローラー、NSX Edge リソース、および ESXi ホストへの IP 接続が必要です。NSX Manager は vCenter と同じサブネット / VLAN にデプロイされますが、厳密には必要ありません。標準的な VM のサイズ設定は、以下のとおりです。

|NSX リリース|vCPU|メモリー|OS ディスク|
|---|---|---|---|
|6.2 Small|4|12 GB|60 GB|
|6.2 Default|4|16 GB|60 GB|
|6.2 Large Scale|4|24 GB|60 GB|
{: caption="表 1. NSX Manager の標準的な VM サイズ設定" caption-side="top"}

**NSX Controller ノード**<br />
NSX Controller ノードは、NSX Manager UI から仮想アプライアンスとしてデプロイされます。各アプライアンスは、通常、NSX Manager と同じサブネット内にある別個の IP アドレスを介して通信しますが、これは厳密な要件ではありません。少なくとも 3 つのコントローラー VM を、少なくとも 3 つの別々の物理 vSphere ノードにデプロイすることが推奨されています。これらは、NSX Manager によって定義されるジョブ描写で active-active-active として機能します。ノードで障害が発生すると、「多数決ルール」のフェイルオーバーが発生して、残りのコントローラーにワークロードが再配布されます。NSX は、この設計慣例をネイティブには実施しません。ネイティブの vSphere 反親和性ルールを使用して、同じ ESXi サーバー上に複数のコントローラー・ノードをデプロイするのを回避できます。VM 当たりの標準的な VM サイズ設定は以下のとおりです。

|Controller VM|vCPU|予約|メモリー|OS ディスク|
|---|---|---|---|---|
|3|4|2048 Mhz|4 GB|20 GB|
{: caption="表 2. NSX Controller の標準的な VM サイズ設定" caption-side="top"}

**NSX Switch**
アップグレードされた仮想分散スイッチ (VDS) は、分散機能を実装するためにすべてのホストにデプロイされます。

**NSX Edge Services Gateway**<br />
必要に応じて、多機能 VM アプライアンスとして環境にデプロイされます。ルーティングのみの場合、最大 8 つのゲートウェイのアクティブ・クラスターをデプロイできます。その他のサービスの場合はすべて、アクティブ・スタンバイ・デプロイメントにデプロイされます。VM 環境の外部の通信には、NAT プール、VIP、および VPN エンドポイントを含むために、IBM Cloud によって割り当てられた移植可能な IP が必要です。

|ゲートウェイ・フォーム|vCPU|メモリー|具体的な使用法|
|---|---|---|---|
|X-Large|6|8 GB|L7 のハイパフォーマンス LB に適しています|
|Quad-Large|4|1 GB|ハイパフォーマンスの ECMP および FW デプロイメントに適しています|
|Large|2|1 GB|小規模な DC およびシングル・サービス|
|Compact|1|512 MB|小規模なデプロイメントまたはシングル・サービスの使用または PoC|
{: caption="表 3. NSX Edge サービス" caption-side="top"}

