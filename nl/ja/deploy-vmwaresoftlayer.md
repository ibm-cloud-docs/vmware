---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware デプロイメント用のクックブックの使用

VMware 管理者は、エンタープライズ・グレードの {{site.data.keyword.BluSoftlayer_full}} グローバル・クラウドにデプロイすることで、費用対効果の高いハイブリッド・クラウドの特性を速やかに認識できます。VMware VM やゲストを変更することなく、vSphere ワークロードおよびカタログを {{site.data.keyword.cloud_notm}} データ・センター内の VMware vSphere 環境にプロビジョンできます。これらのデプロイメントは、共通の vSphere ハイパーバイザーおよび管理 / オーケストレーション・プラットフォームを使用して可能になります。vSphere の実装では、VMware vCloud Suite の他のコンポーネント (vCloud Automation Center、 vCenter Operations Management Suite、vSAN、 vCloud Network & Security、Site Recovery Manager、vCenter Orchestrator、NSX) を利用することもできます。

VMware クックブック・シリーズの中核となる目標は、IBM Cloud インフラストラクチャー内への VMware vSphere 環境のデプロイメントで vSphere 管理者を支援することです。クックブックは、vSphere の管理方法についてトレーニングするためのものではありません。vSphere の管理について詳しくは、『[VMware Education ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}』を参照してください。

{{site.data.keyword.cloud_notm}} は、VMware 管理者が柔軟にベア・メタル・インスタンス、ならびにネットワーク、ストレージ、およびバックアップとリカバリーの構成をセルフサービスで利用できるようにする複数の固有の機能を備えています。これらの構成を使用して、完全に機能する vSphere 実装をデプロイできます。この実装は、オンプレミスの vSphere 実装 (VMware@Home) を拡張または置換するために構築できます。

管理者は、以下のクックブックを使用できます。

* [シングル・サイト VMware 環境の構築](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html): vSphere 管理者に、エンデュランス/パフォーマンス・ブロック・ストレージまたは QuantaStor の使用を含む、環境を構築するステップが順に示されます。
* [vSphere ワークロードのマイグレーション ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window}: vSphere 実装を IBM Cloud データ・センターにデプロイした後にワークロード [仮想マシン (VM)] を VMwareにマイグレーションできるようにするシナリオが示されます。
* [NSX®  の利用 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window}: VMware NSX を利用して、ソフトウェア定義ネットワーキング (SDN) 構成を VMware@SoftLayer デプロイメントに提供できます。
* [Catalogic ECX ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window}: ハイブリッド IT インフラストラクチャーで CopyData を管理および分析できます。インフラストラクチャーは、Catalogic ソフトウェア・インテリジェント・コピー・データ管理プラットフォームの ECX を使用し、NetApp Private Storage および VMware vSphere インフラストラクチャーを使用することで、IBM Cloud インフラストラクチャーにデプロイされます。
* [VMware バックアップ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window}: このクックブックでは、VMware デプロイメントで実行されている VMware ベースのワークロード (VM) をバックアップ、リカバリー、アーカイブするための代替アプローチについて説明しています。
* [VMware 災害復旧 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window}: このクックブックでは、VMware を使用して災害復旧 (DR) ソリューションを設定する 2 つのユース・ケースについて詳述しています。最初のものでは、オンプレミスの VMware 環境とペアとなるようにし、オンプレミスのワークロードのリカバリー (およびその逆の操作) を可能にします。2 つ目のものでは、2 番目の {{site.data.keyword.cloud_notm}} データ・センターで VMware ワークロードをリカバリーします。
* [VMware の Vormetric 暗号化 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window}: 各ユース・ケースで、Vormetric が VM データを暗号化して VMware ワークロードをどのように保護するのかを示しています。
* [IBM、VMware、および HyTrust を使用した信頼できるクラウド・ソリューションのデプロイ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window}: 各種アーキテクチャー・エレメントを統合して、ハードウェアからハイパーバイザーおよび管理アプリケーションに至るまでのトラスト・チェーンを作成できます。


**注:** クックブックは、経験豊富な vSphere 管理者向けです。説明されている一部のトピックでは、読者が vSphere および vCenter をインストールおよび構成するための基本的なデプロイメント・スキルを備えているものと想定しています。
