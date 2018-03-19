---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware のための EVaultバックアップ・クライアントのインストール

VMware サーバーへの EVault バックアップ・クライアントのインストールは、ターゲット ESX サーバー内のシェルまたは端末で一連のコマンドを使用して実行できます。この手順では、VMware サーバーに EVault バックアップ・クライアントをインストールするために必要なステップの概要を示します。
{:shortdesc}

エージェントをインストールするために、以下のコマンドを使用して `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` パッケージをダウンロードし、ターゲット ESX Server にコピーします。

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**注:** 以下のステップは、ターゲット ESX Server のローカルで実行する必要があります。

1. パッケージからファイルを解凍します。そのために、以下のコマンドを使用します (ここで、「PACKAGENAME」は「Agent-VMware-ESX-Server-6.71」などです)。<br/>`tar xvfz PACKAGENAME.tar.gz`
2. パッケージを解凍したディレクトリーに移動します。
3. 以下のように、インストール・スクリプトを実行します。<br />`# ./install.sh`<br/><br/>
**注:** インストール・スクリプトから、Web 登録 (アドレス、ポート番号、および認証) やログ・ファイル名などの構成情報が対話式に求められます。

このサーバーの WebCC ユーザー名を入力します。

4. WebCC ユーザー名を要求するプロンプトに対する入力として、**EVault バックアップ・ユーザー名**を入力します。EVault バックアップ・ユーザー名を表示する手順については、『[EVault バックアップ・ストレージの詳細の表示 (EVault Backup Storage Details)](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal)』の手順を参照してください。
5. WebCC パスワードを要求するプロンプトに対する入力として、EVault バックアップ・パスワードを入力します。
6. インストールが終了すると、完了メッセージが表示され、エージェント・デーモンが実行されています。


その他のインストールに関する注:<br/>
インストールが成功した場合、Install.log がインストール・ディレクトリーにあります。<br/>
例: `/opt/BUAgent/Install.log`

インストールが失敗してロールバックした場合、インストール・ログは、`<Installation Failure directory> にあります。`<br/>
失敗したが、ロールバックしなかった場合、インストール・ログは、`<Installation Kit directory>` にあります。<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
上記リンクを表示するには、{{site.data.keyword.BluSoftlayer_full}} VPN に接続されていることを確認してください。IBM Cloud VPN への接続について詳しくは、『[IBM Cloud インフラストラクチャー・プライベート・ネットワークへのアクセスの有効化 (Enable access to the IBM Cloud infrastructure private network)](/docs/customer-portal/getting-started.html#enable-private-network)』を参照してください。
