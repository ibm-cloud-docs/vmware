---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware のライセンス交付オプション 

VMware 管理者は、{{site.data.keyword.BluSoftlayer_full}} のエンタープライズ・グレード・グローバル・クラウドにデプロイすることにより、コスト効率の高いハイブリッド・クラウドの特性を素早く実現できます。 {{site.data.keyword.BluSoftlayer_notm}} の主な差別化要因は、VMware の VM またはゲストを変更せずに、{{site.data.keyword.BluSoftlayer_notm}} データ・センター内の VMware vSphere 環境に vSphere のワークロードおよびカタログをプロビジョンできる点です。これらのデプロイメントは、共通の vSphere ハイパーバイザーおよび管理 / オーケストレーション・プラットフォームを使用して可能になります。

vSphere 6 Enterprise Plus ライセンスの提供に加え、{{site.data.keyword.BluSoftlayer_notm}} では、vCenter、NSX、vRealize、vSAN、および Site Recovery Manager (SRM) の月次ライセンスも提供しています。

## VMware vSphere

**使用目的:** プロセッサー、メモリー、ストレージ、およびネットワーキングのリソースを抽象化して、単一の物理サーバー上に複数の仮想サーバーを作成するベア・メタル・サーバーの仮想化 OS プラットフォーム。複数の物理サーバーを一緒にクラスター化して、プライベート・クラウドを作成できます。

**ユーザー・インターフェース:** vCenter Client、VMware API、VMware CLI

**フィーチャー:**
* vMotion ライブ・マイグレーション
* 高可用性
* フォールト・トレランス
* レプリケーション
* Nvidia GRID vGPU 仮想化
* ワークロード容量の最適化
* Distributed Resources Scheduler (DRS)
* シン・プロビジョニング
* ネットワーク入出力制御

## VMware vCenter

**使用目的:** 各 vSphere Host 内の計算リソースの管理を一元化します。VSphere Host は個別に管理できますが、vCenter コントロールの下に置くと、以下の機能が使用可能になります。

**ユーザー・インターフェース:** Web クライアント、シック・クライアント、VMware API、VMware CLI

**フィーチャー:**
* 管理対象の vSphere Host およびゲスト仮想マシン内のすべてのアスペクトを集中して制御および表示できます。
* 計算ネットワークおよびストレージ管理に関して、vCenter Web クライアントを介した単一インターフェース・ビューを提供します。
* プロアクティブ最適化。vSphere Host 全体での効率性を最大限にするためにリソースの割り振りと最適化を使用可能にします。
* その他の組み込まれているアドオンおよびサービス (NSX、vRealize、vSAN、および Site Recovery Manager (SRM) など) の拡張管理機能。
* モニタリング、アラート、スケジューリング。クラウド管理者はイベントを表示し、vCenter Web クライアント内でアラートを発行し、スケジュール済みアクションを構成できます。
* 自動化エンジン。vCenter は、vSphere API Web インターフェースを介して提供されるタスクを実行するエンジンです。VMware vRealize Automation および vRealize Orchestration は、VMware API を介して vCenter アクションを実行するアプリケーションの例です。

## VMware NSX

**使用目的:** NSX は、クラウド・プラットフォームの運用に欠かせない Software-Defined Network (SDN) 機能を提供します。

**ユーザー・インターフェース:** vCenter Client、VMware API、VMware CLI

**フィーチャー:**
* ロード・バランシング
* ファイアウォール
* ルーティング
* 論理スイッチ
* VPN
* VxLAN セグメンテーション / トンネル・エンドポイント

## VMware vRealize

**使用目的:** VMware vRealize Suite は、異機種混合のハイブリッド・クラウドを管理するために使用できる、企業対応型のクラウド管理プラットフォームです。

**ユーザー・インターフェース:** vCenter Client、VMware API、VMware CLI

**ライセンス・モデル:** 1 カ月あたりでプロセッサー単位

**フィーチャー:**
* vRealize Automation: パーソナライズされたインフラストラクチャー、アプリケーション、およびカスタム IT サービスの自動配信
* vRealize Operations: インテリジェントなヘルス、パフォーマンス、容量、および構成管理のオーケストレーション
* vRealize Log Insight: リアルタイムのログ管理とログ分析

## VMware vSAN

**使用目的:** VMware vSAN は、各 vSphere Host 上のローカル・ストレージ・ドライブを、vSAN クラスター内のすべてのホストからアクセス可能なシェアード・ナッシング・ストレージ・デバイスに集約およびプールすることを可能にする分散ストレージ・テクノロジーです。

**ユーザー・インターフェース:** vCenter Client、VMware API、VMware CLI

**フィーチャー:**
* 分散ホスト・ベース・ストレージ
* シェアード・ナッシング・アーキテクチャー
* 最大 64 ノードまで拡張可能
* 低遅延
* 構成可能なフォールト・トレランス

## VMware Site Recovery Manager (SRM)

**使用目的:** VMware Site Recovery Manager (SRM) は、プライベート・クラウド環境内のサイト間でのアプリケーションの可用性と移動性を可能にします。仮想マシンのカプセル化と分離を十分に活用することで、Site Recovery Manager は、災害復旧の簡易自動化を使用可能にして復旧時間目標 (RTO) を達成します。また、SRM は、事業継続性計画に関連したコストを削減し、仮想環境のリカバリーにおいて低リスクかつ予測可能な結果の達成に役立ちます。

**ユーザー・インターフェース:** vCenter Client、VMware API、VMware CLI

**フィーチャー:**
* 稼働状態でのリカバリー・テスト
* 自動化オーケストレーション・ワークフロー
* ネットワーク設定とセキュリティー設定の自動リカバリー
* カスタム自動化の拡張性
* オーケストレーションされた Cross vCenter vMotion
* 一元管理されたリカバリー計画
* ポリシー・ベースの管理
