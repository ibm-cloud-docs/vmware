---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  VMware vSphere 6 へのマイグレーションおよびアップグレード

VMware 管理コントロール・パネルを使用して、VMware クラウド環境を、任意の {{site.data.keyword.BluSoftlayer_full}} データ・センターに、素早くかつ容易に拡張または移動します。vSphere のワークロードをマイグレーションおよびアップグレードするには、以下の手順を参考にしてください。
{:shortdesc}

1. データを収集します。
2. 以下の既存のアーキテクチャーを確認します。
  1. リソース使用率 (CPU / メモリー / ストレージ)。
  2. 成長率の追跡と予想。
  3. 今後のプロジェクトの特定。
  4. デプロイされている割り当て済み VLAN / サブネット / その他の判別 (コントロール・ポータルから使用可能)。
  5. ソリューションに使用されている自己定義 RFC1918 (プライベート) サブネットの検出。
3. 以下に示す VMWare 6 の資料を確認し、VMWare コミュニティーに参加します。
  1. [VMware vSphere の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [VMware Technology Network ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://communities.vmware.com/welcome){: new_window}
4. VMWare 6 をサポートするための管理チームのトレーニングを更新します。
5. 新規アーキテクチャーを計画および設計します。
6. コンプライアンスに基づく[データ・センター ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window} を選択します。IBM Cloud の販売担当員と協力し、製品 / サービスの可用性に基づいて候補ロケーションを絞り込みます。
7. 必要な VLAN とサブネット (移植可能なパブリック IP およびプライベート IP) を定義します。
8. 以下のようにして vSphere Server を設計します。
  1. 現在の IBM Cloud サーバーのカタログを確認します。冗長アップリンク、予備電源機構、および RAID-1 (ローカル (ブート) ディスク用) とともに Intel Xeon v3 サーバーが推奨されます。
  2. VMWare の多くのお客様は、N+1 のハード容量上限 ((保守 / 障害などのために) 1 つのノードが除去された状態で、すべての VM を安心してサーバーに割り振ることができる) に従っています。
  3. 多くのお客様は、計算の所要時間が少ないため、より標準的な 60%-75% と比べて、より高い「ソフト上限」である ~80% (「n」サーバー構成で 80% の容量) を望んでいます。
  4. 外部ベンダーからの vSphere ゲストには、外部 OS ライセンス (Microsoft、Red Hat など) が必要になる場合があります。
  5. [Performance Best Practices for VMware vSphere 6.0 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window} を確認します。
9. 以下のようにして vCenter Server を設計します。
  1. 通常、中規模の仮想サーバー・インスタンス (VSI) は、小規模環境 (8 個の vCPU および 16 GB RAM) のエントリー・ポイントです。一方、大規模環境ではベア・メタルが使用されます。
  2. vCenter は、OS アドオンまたはアプライアンスとしてスタンドアロンの VSI Windows 仮想マシンにデプロイできます。
    1. 参照リンク:
        * [vCenter Server 6.0 requirements for installation ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://kb.vmware.com/s/article/2107948){: new_window}
        * [VMware vCenter Server Performance and Best Practices ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}
        * [VMware vSphere 6 での vCenter Server Appliance (vCSA) のデプロイと構成](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. 非 VMWare サーバー: 必要な可能性がある非 VMWare サーバー (仮想またはベア・メタル) を特定し、それに従って適切に計画を立てます。
11. ストレージ:
  1. 環境のストレージ計画を作成します。仮想化のためのスナップショット・スペースを持つエンデュランス 2 IOPS/GB は開始ストレージ計画としてはすぐれていますが、仮想データベースやその他のハイパフォーマンス・アプリケーションが使用される場合は、4 IOPS/GB 層がより適しています。通常は、NFS ストレージが推奨されます。  
  2. [VMWare システムで使用するストレージ (Storage to use with VMware Systems) ](select-storage-option-use-vmware.html)に選択マトリックスがあります。
  3. スナップショット・スペースは、通常、ポイント・イン・タイム・リストアの 2 次手段として使用されます。このプロセスは非常に効率的であり、容易にサイズを増加できるため、出発点としては 10% が適しています。
12. バックアップ:
  1. 既存のバックアップ・ストラテジーが機能することを確認します。バックアップ・ストラテジーがない場合は、作成する必要があります。
  2. 独自のバックアップ・ソリューションを使用できます。vSphere Enterprise Plus のライセンスに組み込まれているバックアップ機能、VEEAM などの最適化されたサード・パーティー・ソリューション、または従来型の IBM Cloud r1soft バックアップを使用できます。
13. 以下のようにしてマイグレーション・ストラテジーを作成します。
  1. [Best practices to install or upgrade to ESXi 6.0 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://kb.vmware.com/s/article/2109712){: new_window} を確認します。
  2. 既存の DNS または IP の構成 (あるいはその両方) を確認し、必要に応じて TTL を短縮します。
  3. VM の計画を作成し、ソース・ホスト、宛先ホスト、ソース IP、宛先 IP、および関連する DNS エントリーを組み込みます。
  4. ほとんどのシナリオでは、VM ごとにマイグレーションしてから、パブリック・ネットワークおよびプライベート・ネットワークの構成を更新することをお勧めします。古いバージョンから新しいバージョンに移動する場合は、通常、VM をシャットダウンし、環境間で_切り離し/接続_ を実行して、単純に VM を「リップ・アンド・シップ (rip and ship)」するのが最良の方法です。ロケーション間を移動する場合は、長距離の vMotion が可能です。
  5. 環境の検査を行うためのテスト計画を作成します。
  6. 変更 / 保守期間をユーザーと調整します。個別の VM 保守期間は、データの転送、VM の構成、DNS の変更と伝搬、およびトラブルシューティングのための時間で占めることができます。
14. 以下のようにして、新しい環境をデプロイします。
  1. [VMware vSphere 6 入門](vmware-vsphere-6-getting-started.html)。
  2. 新規の vSphere サーバーと vCenter サーバー (およびその他の必要なサーバー) をオーダーします。
      **注:** 適切な「未結合」ネットワーク・アップリンクが選択されていることを確認します。
  3. 適切なストレージをオーダーして構成します。[Architecture Guide for IBM File Storage for IBM Cloud with VMware](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html)
  4. 新しい VLAN とポータブル・サブネットをオーダーします (詳細なアーキテクチャー図と位置調整が必要な可能性があります)。
  5. vSphere Server と通信するように vCenter を構成し、環境を構成します。
  6. 稼働環境でバックアップを取ります。
  7. マイグレーション計画および関連のテスト計画を実行します。
  8. 新しい環境でバックアップを実施します。
  9. 新しい環境を作動します。
  10. レガシー環境を廃棄します。
