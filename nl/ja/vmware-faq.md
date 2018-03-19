---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# FAQ : VMWare 

## IBM Cloud ポータルから vSphere をデプロイするとき、どのライセンス・レベルが有効になりますか? 

vSphere ライセンスの最上位レベルである Enterprise Plus が有効になります。

## VMware vSphere 6 のライセンス交付はどのように行われますか? 

ライセンス交付方法は、お客様のデプロイメント・メカニズムに結合されています。VMware 6 をデプロイするには、以下の 2 つの方法があります。

1. コントロール・ポータルから vSphere をデプロイすると、VMware Service Provider Program (VSPP) ライセンスが自動的に有効になります。デプロイメント時に、デフォルト・ユーザー「slvmadmin」が、コントロール・ポータルで vSphere の管理および統合サービスのホストに追加されます。

2. vSphere を手動でデプロイする場合は、ユーザー自身のライセンスおよびメディア (BYOL/BYOM) を使用できます。それにより、ご使用の標準ライセンスをこれらのホストに適用することができます。**注:** ユーザー自身の VMWare ライセンスを使用する場合は、CentOS や NO OS などの無料 OS を使用してサーバーをオーダーすることをお勧めします。それから、IPMI の [Virtual ISO](../bare_metal/mount-iso-bare-metal-server.html) を介して VMWare OS をインストールしてください。

## 単独のプライベート VMware クラウドを作成できますか? 

はい、できます。ベア・メタル・システムをデプロイし、それらのホストに、サポートされるハイパーバイザー (VMware ESX を含む) をインストールできます。また、ネイティブ管理ツールを使用して仮想マシンをデプロイすることもできます。デフォルトでは、システムは、分離とネットワーキングのコンポーネント (ゲートウェイ、ルーター、およびファイアウォールなど) のために VLAN にデプロイされ、ほとんどすべてのトポロジーの作成に使用されます。

## VMware のライセンス交付はどのように行われますか? 

ライセンス交付方法は、お客様のデプロイメント・メカニズムに結合されています。VMware をデプロイするには、以下の 2 つの方法があります。

1. ポータルから ESX をデプロイすると、VMware Service Provider Program (VSPP) ライセンスが自動的に有効になります。デプロイメント時に、デフォルト・ユーザー「vmadmin」が、データ収集のために ESX サーバーに追加されます。このデフォルト・ユーザーは削除しないでください。VSPP は、すべての「電源投入された」仮想マシン用に予約および使用されている RAM を対象にして料金を請求します (標準のホスト・ライセンスのように、「ソケット当たり」の請求ではありません)。

2. ESX を手動でデプロイするとき、Bring Your Own License (BYOL) が可能なため、標準ライセンスをこれらのホストに適用することができます。**注:** BYOL は、ポータルを介してデプロイされるホストには使用できません。VSPP が有効化されるようになっています。

    * さらに、VSPP が機能するために、vCenter Server インスタンスは必要ありません。

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## VMware のコンポーネントを IBM Cloud ポータルから直接デプロイできますか? 

はい、できます。以下の 2 つのオプションがあります。

1. 月次ベア・メタル・システム<!-- (Figure 2)--> を使用して、ESX ハイパーバイザーを自動的に選択してデプロイします。また、仮想マシンまたはベア・メタル・システム (Windows のみ) を使用して vCenter 管理を自動的にデプロイすることもできます。

2. CentOS などの無料オペレーティング・システムを使用してベア・メタル・ホストをデプロイし、その後、ホストのリモート・コンソールと仮想メディア・アクセスを使用して、ESX を手動でインストールします。次に、vCenter Server を手動でインストールするか、Linux 上で作動する VMware vCenter Server Appliance をデプロイすることができます。

