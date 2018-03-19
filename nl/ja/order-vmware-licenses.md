---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware ライセンスの注文

VMware 管理者は、{{site.data.keyword.BluSoftlayer_full}} にデプロイすることによって、コスト効率の高いハイブリッド・クラウドの特性を迅速に実現できることが分かります。この特性の 1 つは、vSphere ワークロードおよびカタログが、VMware VM またはゲストを変更せずに、{{site.data.keyword.cloud_notm}} データ・センター内の VMware vSphere 環境にプロビジョンされることです。共通 vSphere ハイパーバイザーおよび管理/オーケストレーション・プラットフォームを使用すると、これらのデプロイメントが可能になります。
{:shortdesc}

また、vSphere 実装では、他のコンポーネントの使用も可能です。表 1 には、{{site.data.keyword.slportal}} を介して注文できる VMware 製品のリストが含まれています。料金情報は、[IBM Cloud for VMware Solutions](http://www.softlayer.com/vmware-solutions) の下にあります。

|製品名|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard Tier 1 (0 - 20 TB)|
|Virtual SAN Standard Tier 2 (21 - 64 TB)|
|Virtual SAN Standard Tier 3 (65 - 124 TB)|
|VMware Site Recovery Manager (SRM)|
{: caption="表 1. カスタマー・ポータルで使用可能な VMware 製品" caption-side="top"}

表 1 にリストされている VMware 製品のライセンスを注文するには、以下の手順を使用します。
1. [{{site.data.keyword.slportal_short}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://control.softlayer.com/){: new_window} にログインします。
2. **「デバイス」>「管理対象」>「VMware ライセンス」**をクリックします。
3. 右上隅にある**「VMware ライセンスの注文」**をクリックします。
4. **「ライセンスの追加...」**の下のドロップダウン・リストをクリックして、注文するライセンスの VMware 製品および CPU 数をリストします。
  * **注:** VMware vSphere Enterprise Plus (ESXi 6.0) は、このプロセスで注文は行われません。ベア・メタル・サーバーの注文時に、要求する OS として注文されます。
5. 画面の右端に、選択した VMware 製品の価格が表示されます。
6. ライセンスを注文する場合は**「続行」**をクリックします。または、**「ライセンスの追加」**をクリックしてライセンスを追加することができます。
  * **「続行」**をクリックすると、**「VMware ライセンス」**」ページに戻り、ご使用の VMware 製品およびライセンス・キーが表示されます。
7. 提供されたリンクから**インストール・ファイル**をダウンロードします。ダウンロード・ページにアクセスするには、IBM Cloud プライベート・ネットワークへの SSL 接続が必要です。
8. 正しい VMware 製品をダウンロードし、手動で vSphere 環境にインストールします。
