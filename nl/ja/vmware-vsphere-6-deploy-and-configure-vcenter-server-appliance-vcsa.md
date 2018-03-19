---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere 6 での vCenter Server Appliance (vCSA) のデプロイと構成  

VMware vCenter Server Appliance をデプロイするには、以下の手順を使用します。
{:shortdesc}

**前提条件**
* 互換性のあるブラウザーがインストールされた Windows システム
  * Internet Explorer / Firefox / Chrome
* VMware vCenter Server Appliance をサポートするのに十分なリソースがある vSphere Host
  * 必要なシステム・リソースについて詳しくは、[Minimum requirements for the VMware vCenter Server 6.0 Appliance ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://kb.vmware.com/s/article/2106572){: new_window} を参照してください。
* VCSA ISO イメージ
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* ISO をマウントする能力
* IBM Cloud プライベート・ネットワークへのアクセス権限を持つ VPN セッション

**vCenter Server Appliance のデプロイと構成**

1. vCenter Server Appliance (vCSA) の ISO をマウントします。
2. 互換性のあるブラウザーで vcsa-setup.html を開きます。
3. VMware Client Integration プラグインのインストールを確認し、同意します。
4. **「許可 (Allow)」**をクリックします。
5. **「インストール (Install)」**をクリックします。
6. ご使用条件を確認して受諾し、**「次へ (Next)」**をクリックします。
7. vCSA をインストールする VMware Host の FQDN またはプライベート IP アドレス、およびユーザー名とパスワードを入力します。**「次へ (Next)」**をクリックします。
8. **「はい (Yes)」**をクリックして、証明書の警告を受け入れます。
9. 適切なアプライアンス名と OS パスワードを入力し、**「次へ (Next｣**をクリックします。
10. デプロイメント・タイプとして「Platform Services Controller が組み込まれた vCenter Server をインストールする (Install vCenter Server with an Embedded Platform Services Controller)」を選択し、**「次へ (Next)」**をクリックします。
11. 「SSO ドメインの作成 (Create an SSO domain)」をクリックし、**「次へ (Next)」**をクリックします。 <!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. アプライアンスのサイズを選択し、**「次へ (Next)」**をクリックします。
13. データ・ストアを選択し、**「次へ (Next)」**をクリックします。
14. 「組み込みデータベース (PostgreSQL) の使用 (Use an embedded database (PostgreSQL))」を選択し、「**次へ (Next)*」をクリックします。
15. 以下の情報を入力して、ネットワーク構成をセットアップします。
  1. ネットワーク (Network)
  * IP アドレス・ファミリー (IP address Family)
  * ネットワーク・タイプ (Network Type)
  * ネットワーク・アドレス (Network Address)
  * システム名 (System name)
  * サブネット・マスク (Subnet mask)
  * ネットワーク・ゲートウェイ (Network gateway)
  * ネットワーク DNS サーバー (Network DNS Servers)
      * 詳細情報については、[ローカル DNS リゾルバーとは (What are Local DNS Resolvers) ](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-)を参照してください。
  * 時間同期を構成します。
  * **「次へ (Next)」**をクリックします。
16. 設定を確認し、次に**「完了 (Finish)」**をクリックします。vCSA インスタンスがプロビジョンされました。

