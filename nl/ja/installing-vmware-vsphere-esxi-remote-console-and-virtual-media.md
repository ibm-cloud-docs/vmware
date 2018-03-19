---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Remote Console および仮想メディアを介した VMware vSphere ESXi のインストール

インストール・メディアからの ESX のデプロイは、すべてのバージョンで同様であり、BYOL (Bring Your Own License: ライセンス持ち込み) シナリオで使用できます。

## 要件
* プライベート・ネットワークにアクセスできる仮想マシン (VM) インスタンス [vpn.softlayer.com やパブリック IP を介してアクセス可能な、Java 対応ブラウザーを備えた、Windows または Linux でインストールされたクラウド・コンピュート・インスタンス (VSI) など]。VSI は、サーバーの Intelligent Platform Management Interface (IPMI) アドレスが配置されているのと同じプライベート・ネットワーク上になければなりません。
* VMware ESXi VIM インストーラー ISO のコピー。

<!--## Steps -->

## IPMI への接続
1. 要件で示されている VSI に VMware ISO をアップロードします (VSI は、パブリック Web アクセス権限を備えている必要があります)。
2. カスタマー・ポータルから IPMI アドレスおよびログインの情報を収集します。
3. **「デバイス」**>**「デバイス・リスト」**>**[サーバー]**>**「リモート管理」**タブを選択します。
4. リモート・デスクトップ (RDP) または Remote X により、ESXi イメージを保管する VSI に接続します。
5. RDP セッションで Web ブラウザーを開き、ステップ 2 で収集した IPMI アドレスを入力します。
6. 同じくステップ 2 で確認した資格情報 (通常、root) を使用して、IPMI コンソールにログインします。
* IPMI ユーザー・アクセス・レベルをメモします。管理者である可能性があります。**オペレーター**に設定されている場合、リモート・ストレージのマウント時に問題が発生する可能性があります。メディアをマウントできない場合は、サポート・チケットをファイルして、IPMI 資格情報の昇格を依頼してください。
7. ホーム・ログイン・ページが表示されていることを確認し、**「リモート・コントロール (Remote Control)」**>**「コンソール・リダイレクト (Console Redirection)」**>**「コンソールの起動 (Launch Console)」**をクリックします。

## ISO の接続
1. KVM (Kernel-based Virtual Machine) ビューアーで、**「仮想メディア (Virtual Media)」**>**「仮想ストレージ (Virtual Storage)」**を選択します。ご使用のオペレーティング・システムと Java バージョンによっては、Java ベースのビューアーを開始するためのアクセスを許可する必要がある場合があります。
2. 「仮想ストレージ (Virtual Storage)」ウィンドウで**「CDROM」&「ISO」**タブをクリックします。「論理ドライブ・タイプ (Logical Drive Type)」で**「ISO ファイル (ISO File)」**を選択し、**「イメージを開く (Open Image)」**をクリックします。
3. ESXi ISO に移動し、**「OK」**をクリックします。次に、**「プラグイン (Plug in)」**をクリックします。
4. ISO がセッションにプラグインされたら、**「OK」**をクリックします。
* IPMI Web ページに戻り、**「リモート (Remote)」**>**「制御 (Control)」**>**「サーバーのリセット (Reset Server)」**>**「アクションの実行 (Perform Action)」**をクリックしてサーバーを再始動します。

### インストールおよびネットワーキング構成の実行
1. ESXi をインストールします。
* インストールが完了したら、サーバーを再始動できるように、必ず ISO を**プラグアウト**してください。
2. サーバーを再始動します。
3. 再始動後にサーバーの IP アドレスを構成します。
4. デバイスの「構成 (Configuration)」タブから詳細を収集します。

ESXi ホストを管理できるようになりました。

エンデュランスまたはパフォーマンス・ブロック・ストレージをセットアップする方法について詳しくは、『[ブロック・ストレージのプロビジョンおよび管理 (Provisioning and Managing Block Storage)](/docs/infrastructure/BlockStorage/provisioning-block_storage.html)』を参照してください。

QuantaStor のセットアップについて詳しくは、『[QuantaStor のアーキテクチャー・ガイド](architecture-guide-quantastor-vmwaresoftlayer.html)』を参照してください。
