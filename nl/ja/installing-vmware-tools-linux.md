---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# VMware Tools のインストール - Linux

VMware ツールは、仮想マシンのゲスト・オペレーティング・システムのパフォーマンスを向上させ、仮想マシンの管理を改善するためのユーティリティー・スイートです。ゲスト・オペレーティング・システムへの VMware Tools のインストールは、必要不可欠です。ゲスト・オペレーティング・システムは VMware Tools なしで実行可能ですが、重要な機能や利便性が失われます。

Linux、FreeBSD、および Solaris ゲストでは、サービスの名前は `vmware-guestd` です。`vmware-guestd` サービスは、ゲスト・オペレーティング・システム内の以下の作業を実行します。

* ホスト・オペレーティング・システムのメッセージをゲスト・オペレーティング・システムに渡す。
* ワークステーションで電源操作が選択されると、オペレーティング・システムでコマンドを実行して、Linux、FreeBSD、または Solaris システムを正常にシャットダウンまたは再始動する。
* ゲスト・オペレーティング・システムの時刻をホスト・オペレーティング・システムの時刻に同期する。
* ゲスト・オペレーティング・システム操作の自動化に役立つスクリプトを実行する。スクリプトは、仮想マシンの電源状態の変更時に実行されます。

ゲスト・オペレーティング・システムが開始すると、サービスが開始します。

Linux サーバーに VMware ツールをインストールするために、vSphere クライアントで該当するサーバーを右クリックし、**「ゲスト」**の上に移動し、**「VMware Tools のインストール/アップグレード」**をクリックします。

このリンクにより、VMware Tools の rpm が入った仮想 CD-ROM ドライブがマウントされます。仮想 CD-ROM ドライブのマウント後に Tools をインストールするには、以下のステップに従います。
1. コマンド `mount /dev/cdrom /mnt` を使用して、CD-ROM ドライブをマウントします。
2. マウントしたディレクトリーに対して `ls /mnt` コマンドを使用して、ファイルが存在していて正しくマウントされていることを確認します。ファイル `VMWareTools-4.0.0-208167.i386.rpm` が表示されます。 
3. コマンド `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm` を実行します。
4. コマンド `/usr/bin/vmware-config-tools.pl` を実行して、実行中のカーネルに対して VMware Tools を構成します。**注:** 構成の更新の途中で 1 回、**ENTER** キーを押すように求められます。
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**注:** VMware Tools のインストール後に VM を再始動する必要はありませんが、再始動することをお勧めします。

VMware Tools が正常にインストールされると、vSphere Client インターフェース内に「OK」が表示されます。
