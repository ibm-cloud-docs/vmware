---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# VMware ESX 仮想マシンの作成

新しい仮想マシンを作成するには、以下の手順を実行します。
{:shortdesc}

1. VSphere Client の「インベントリー (Inventory)」ペインでホスト・ノードの IP アドレスを右クリックします。
2. 構成ウィンドウで**「カスタム (Custom)」**をクリックします。
3. 仮想マシンに適切な名前を付け、**「次へ (Next)」**をクリックします。
4. 仮想マシン・ファイルのストレージ・ロケーションを選択し、**「次へ (Next)」**をクリックします。
5. **「仮想マシンのバージョン (Virtual Machine Version)」**から、**「仮想マシンのバージョン 8 (Virtual Machine Version 8」**を選択します。 <!-- since we are using vSphere instead of the Web Client to create it (in which case we would use version 11 instead).-->
6. **「オペレーティング・システム (Operating System)」**を選択します。
7. 仮想プロセッサーの数 (**「CPU」ページ**) と、仮想マシンを作成する**メモリー**の量を選択します。**注:** プロセッサー数とメモリー量は、リソースが使用可能であれば、後で変更できます。ネットワーク・セクションで、2 つの NIC (NIC 1 はプライベート・ネットワークで、NIC 2 はパブリック・ネットワーク) を接続する必要があります。アダプター・タイプは「フレキシブル (Flexible)」になります。**「電源投入時に接続 (Connect at Power On)」**が選択されていることを確認します。
8. **「SCSI コントローラー (SCSI Controller)」**画面は、デフォルトの「LSI 論理並列 (LSI Logic Parallel)」のままにします。**「ディスクの選択 (Select a Disk)」**画面で、**「新規仮想ディスクの作成 (Create a new virtual disk)」**を選択します。**「詳細オプション (Advanced Options)」**画面および**「終了準備の完了 (Ready to Complete)」**画面もデフォルトのままにします。これで新規仮想マシンの作成が完了しました。 

インストール・メディアのロードを開始するには、インベントリー・リストでサーバー名をクリックします。次に、**「基本タスク (Basic Tasks)」**の下で**「仮想マシンの設定の編集 (Edit Virtual machine Settings)」**をクリックします。

9. **「CD/DVD ドライブ 1 (CD/DVD Drive 1)」**が選択された状態で、「デバイス状況 (Device Status)」の下の**「電源投入時に接続 (Connect at power)」**チェック・ボックスにチェック・マークを付けます。データ・ストアにある ISO ファイルを指定するには、**「参照 (Browse)」**をクリックします。
10. ここで、デフォルトの Storage1 データ・ストアにアップロードされる ISO ファイルを選択できます。また、(「新規仮想マシンの作成」プロセスの「ステップ 3」の**「データ・ストア」**セクション時にセットアップされた、) すべてのサーバー仮想マシンの構成ファイル / ログ・ファイルを含むフォルダーも表示されます。

ISO イメージを選択したら、各 OS のインストール・プロセスを開始できます。

仮想マシン・ネットワークのセットアップについて詳しくは、[仮想マシン・ネットワークのセットアップ (Setting up a Virtual Machine Network) ](/docs/infrastructure/virtualization/virtual-machine-network-setup.html){:new_window}を参照してください。
