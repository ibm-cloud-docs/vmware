---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# QuantaStor を使用する VMware 環境のための Brocade vRouter (Vyatta) のセットアップ

QuantaStor を使用する VMware 環境内で Brocade vRouter (Brocade vRouter (Vyatta) アプライアンス [高可用性 (HA) 構成] を構成できます。以下の情報を『[拡張シングル・サイト VMware リファレンス・アーキテクチャー (Advanced Single-Site VMware Reference Architecture)](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html)』とともに使用して、VMware 環境で以下のストレージ・オプションのいずれかをセットアップします。{:shortdesc}

Brocade vRouter (Vyatta) ゲートウェイは、ご使用の環境のゲートウェイおよびルーターとして機能し、サブネットで構成されるゾーンを含んでいます。ゾーンが相互に通信できるように、ファイアウォール・ルールがゾーン間に配置されます。他のゾーンと通信する必要がないゾーンについては、すべてのパケットがドロップされるため、ファイアウォール・ルールは不要です。

構成例では、Brocade vRouter (Vyatta) で作成された以下の 5 つのゾーンがあります。

* SLSERVICE – {{site.data.keyword.BluSoftlayer_full}} サービス
* VMACCESS – 容量クラスター上の仮想マシン (VM)
* MGMT – 管理クラスターおよび容量クラスターと管理 VM
* STORAGE – ストレージ・サーバー
* OUTSIDE – パブリック・インターネット・アクセス

図 1 は、各ゾーン間の通信について説明しています。**注:** ご使用の環境はこれとは異なる可能性があり、別のゾーンやファイアウォール・ルールが必要になることがあります。

![図 1: Brocade vRouter (Vyatta) ゾーン構成](images/brocade_figure1.png "Brocade vRouter (Vyatta) ゾーン構成") 図 1. Brocade vRouter (Vyatta) ゾーン構成

## Brocade vRouter (Vyatta) の構成

Brocade vRouter (Vyatta) を構成するには、以下のステップに従います。

1. 「デバイスの詳細」画面にある root パスワードを使用して、アプライアンスに SSH で接続します。
2. 「Configure」と入力して構成モードに入り、後続のセクションのステップに従います。

### インターフェースのセットアップ

環境でサブネットにリンクする両方の Brocade vRouter (Vyatta) で結合インターフェースを構成します。VLAN (1101、1102、および 1103) を、ご使用の環境内の対応する VLAN に置き換える必要があります。また、'<>' で示されている指示を、ご使用の環境の詳細 ('<>' は削除) で置き換える必要があります。

以下のコマンドを使用して、Brocade vRouter (Vyatta) で結合インターフェースを構成します。`構成`モードでなければなりません。

#### Brocade vRouter (Vyatta) 1
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (VLAN 1101/管理にバインドされる 1 次プライベート・サブネットからの IP アドレスを入力)
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (VLAN 1101/管理 VM にバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (VLAN 1102/ストレージ・パス A にバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (VLAN 1102/ストレージ・パス B にバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力)
    set interfaces bonding bond0 vif 1103 address ‘##.###.###.###/##’ (VLAN 1103/仮想マシンにバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力)
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 advertise-interval '1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 preempt 'false'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 priority '253'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<1101/管理にバインドされる 1 次プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<1101/管理 VM にバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 advertise-interval '1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 preempt 'false'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 priority '253'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<1102/ストレージにバインドされる 1 次プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<1102/ストレージ・パス A にバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<1102/ストレージ・パス B にバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 advertise-interval '1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 preempt 'false'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 priority '253'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<1103/仮想マシンにバインドされる 1 次プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<1103/仮想マシンにバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    commit
    save

#### Brocade vRouter (Vyatta) 2
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (VLAN 1101/管理にバインドされる 1 次プライベート・サブネットからの IP アドレスを入力。Brocade vRouter (Vyatta 1) に割り当てられているものとは異なるものでなければならない
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (VLAN 1101/管理 VM にバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力。Brocade vRouter (Vyatta 1) に割り当てられているものとは異なるものでなければならない
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (VLAN 1102/ストレージ・パス A にバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力。Brocade vRouter (Vyatta 1) に割り当てられているものとは異なるものでなければならない
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (VLAN 1102/ストレージ・パス B にバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力。Brocade vRouter (Vyatta 1) に割り当てられているものとは異なるものでなければならない
    set interfaces bonding bond0 vif 1103 address ‘##.###.###.###/##’ (VLAN 1103/仮想マシンにバインドされるポータブル・プライベート・サブネットからの IP アドレスを入力。Brocade vRouter (Vyatta 1) に割り当てられているものとは異なるものでなければならない
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 advertise-interval '1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 preempt 'false'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 priority '253'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<1101/管理にバインドされる 1 次プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<1101/管理 VM にバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 advertise-interval '1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 preempt 'false'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 priority '253'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<1102/ストレージにバインドされる 1 次プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<1102/ストレージ・パス A にバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<1102/ストレージ・パス B にバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 advertise-interval '1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 preempt 'false'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 priority '253'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<1103/仮想マシンにバインドされる 1 次プライベート VLAN のゲートウェイ・アドレス/マスク>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<1103/仮想マシンにバインドされるポータブル・プライベート VLAN のゲートウェイ・アドレス/マスク>’
    commit
    save

### 外部アクセス用の SNAT の構成

管理 VM および容量クラスター上の VM がインターネットにアクセスできるように SNAT を構成します。後からセットアップの同期が行われるため、このステップ以降では、一方の Brocade vRouter (Vyatta) でのみ構成を行う必要があります。

`構成`モードで以下のコマンドを使用します。

    set nat source rule 10
    set nat source rule 10 source address ##.###.###.###/## (ポータブル・プライベート・サブネット VLAN1101/管理 VM)
    set nat source rule 10 translation address ##.###.###.### (Brocade vRouter (Vyatta) bond1 IP)
    set nat source rule 10 outbound-interface bond1
    set nat source rule 20
    set nat source rule 20 source address ##.###.###.###/## (ポータブル・プライベート・サブネット VLAN1103/仮想マシン)
    set nat source rule 20 translation address ##.###.###.### (Brocade vRouter (Vyatta) bond1 IP)
    set nat source rule 20 outbound-interface bond1
    commit
    save

### ファイアウォール・グループの構成

次に、特定の IP 範囲に関連付けられたファイアウォール・グループを構成します。

`構成`モードで以下のコマンドを使用します。

    set firewall group network-group SLSERVICES
    set firewall group network-group SLSERVICES network 10.1.128.0/19
    set firewall group network-group SLSERVICES network 10.0.86.0/24
    set firewall group network-group SLSERVICES network 10.1.176.0/24
    set firewall group network-group SLSERVICES network 10.1.64.0/19
    set firewall group network-group SLSERVICES network 10.1.96.0/19
    set firewall group network-group SLSERVICES network 10.1.192.0/20
    set firewall group network-group SLSERVICES network 10.1.160.0/20
    set firewall group network-group SLSERVICES network 10.2.32.0/20
    set firewall group network-group SLSERVICES network 10.2.64.0/20
    set firewall group network-group SLSERVICES network 10.0.64.0/19
    set firewall group network-group SLSERVICES network 10.2.128.0/20
    set firewall group network-group SLSERVICES network 10.2.200.0/24
    set firewall group network-group SLSERVICES network 10.1.0.0/24
    set firewall group network-group SLSERVICES network 10.1.24.0/24
    set firewall group network-group SLSERVICES network 10.2.208.0/24
    set firewall group network-group SLSERVICES network 10.1.236.0/24
    set firewall group network-group SLSERVICES network 10.1.56.0/24
    set firewall group network-group SLSERVICES network 10.1.8.0/24
    set firewall group network-group SLSERVICES network 10.1.224.0/24
    set firewall group network-group SLSERVICES network 10.2.192.0/24
    set firewall group network-group SLSERVICES network 10.1.16.0/24
    set firewall group network-group SLSERVICES network 10.0.0.0/14
    set firewall group network-group 1101PRIMARY network ###.###.###.### (1 次プライベート・サブネット 1101/管理)
    set firewall group network-group 1101MGMT network ###.###.###.### (ポータブル・プライベート・サブネット 1101/管理 VM)
    set firewall group network-group 1102PRIMARY network ###.###.###.### (1 次プライベート・サブネット 1102/ストレージ)
    set firewall group network-group 1102STORAGEA network ###.###.###.### (ポータブル・プライベート・サブネット 1102/ストレージ・パス A)
    set firewall group network-group 1102STORAGEB network ###.###.###.### (ポータブル・プライベート・サブネット 1102/ストレージ・パス B)
    set firewall group network-group 1103VMACCESS network ###.###.###.### (ポータブル・プライベート・サブネット 1103/仮想マシン)
    commit
    save

### ファイアウォール名ルールの構成

次に、各トラフィック方向用のファイアウォール・ルールを定義します。

`構成`モードで以下のコマンドを使用します。

    set firewall name INSIDE2OUTSIDE
    set firewall name INSIDE2OUTSIDE default-action drop
    set firewall name INSIDE2OUTSIDE rule 10 action accept
    set firewall name INSIDE2OUTSIDE rule 10 protocol all
    set firewall name INSIDE2OUTSIDE rule 10 source group network-group 1101MGMT
    set firewall name INSIDE2OUTSIDE rule 20 action accept
    set firewall name INSIDE2OUTSIDE rule 20 protocol all
    set firewall name INSIDE2OUTSIDE rule 20 source group network-group 1103VMACCESS
    set firewall name OUTSIDE2INSIDE
    set firewall name OUTSIDE2INSIDE default-action drop
    set firewall name OUTSIDE2INSIDE rule 10 action accept
    set firewall name OUTSIDE2INSIDE rule 10 protocol udp
    set firewall name OUTSIDE2INSIDE rule 20 action accept
    set firewall name OUTSIDE2INSIDE rule 20 protocol udp
    set firewall name OUTSIDE2INSIDE rule 20 destination port 4500
    set firewall name OUTSIDE2INSIDE rule 30 action accept
    set firewall name OUTSIDE2INSIDE rule 30 protocol udp
    set firewall name OUTSIDE2INSIDE rule 30 destination port 500
    set firewall name OUTSIDE2INSIDE rule 40 action accept
    set firewall name OUTSIDE2INSIDE rule 40 ipsec match-ipsec
    set firewall name OUTSIDE2INSIDE rule 50 action accept
    set firewall name OUTSIDE2INSIDE rule 50 protocol gre
    set firewall name OUTSIDE2INSIDE rule 60 action accept
    set firewall name OUTSIDE2INSIDE rule 60 protocol tcp
    set firewall name OUTSIDE2INSIDE rule 60 destination port 1723
    set firewall name OUTSIDE2INSIDE rule 70 action accept
    set firewall name OUTSIDE2INSIDE rule 70 protocol tcp
    set firewall name OUTSIDE2INSIDE rule 70 destination port 80
    set firewall name OUTSIDE2INSIDE rule 80 action accept
    set firewall name OUTSIDE2INSIDE rule 80 protocol tcp
    set firewall name OUTSIDE2INSIDE rule 80 destination port 443
    set firewall name OUTSIDE2INSIDE rule 90 action accept
    set firewall name OUTSIDE2INSIDE rule 90 state established enable
    set firewall name SLSERVICE2INSIDE
    set firewall name SLSERVICE2INSIDE default-action drop
    set firewall name SLSERVICE2INSIDE rule 10 action accept
    set firewall name SLSERVICE2INSIDE rule 10 protocol all
    set firewall name SLSERVICE2INSIDE rule 10 source group network-group SLSERVICES
    set firewall name INSIDE2SLSERVICE
    set firewall name INSIDE2SLSERVICE default-action drop
    set firewall name INSIDE2SLSERVICE rule 10 action accept
    set firewall name INSIDE2SLSERVICE rule 10 protocol all
    set firewall name INSIDE2SLSERVICE rule 10 destination group network-group SLSERVICES
    set firewall name VMACCESS2MGMT
    set firewall name VMACCESS2MGMT default-action drop
    set firewall name VMACCESS2MGMT rule 10 action drop
    set firewall name VMACCESS2MGMT rule 10 protocol all
    set firewall name VMACCESS2MGMT rule 10 source group network-group 1103VMACCESS
    set firewall name STORAGE2MGMT
    set firewall name STORAGE2MGMT default-action drop
    set firewall name STORAGE2MGMT rule 10 action accept
    set firewall name STORAGE2MGMT rule 10 protocol all
    set firewall name STORAGE2MGMT rule 10 source group network-group 1102PRIMARY
    set firewall name STORAGE2MGMT rule 20 action accept
    set firewall name STORAGE2MGMT rule 20 protocol all
    set firewall name STORAGE2MGMT rule 20 source group network-group 1102STORAGEA
    set firewall name STORAGE2MGMT rule 30 action accept
    set firewall name STORAGE2MGMT rule 30 protocol all
    set firewall name STORAGE2MGMT rule 30 source group network-group 1102STORAGEB
    set firewall name MGMT2STORAGE
    set firewall name MGMT2STORAGE default-action drop
    set firewall name MGMT2STORAGE rule 10 action accept
    set firewall name MGMT2STORAGE rule 10 protocol all
    set firewall name MGMT2STORAGE rule 10 source group network-group 1101PRIMARY
    set firewall name MGMT2STORAGE rule 10 source group network-group 1101MGMT
    commit
    save

### ゾーン・バインディングの構成

このステップでは、Brocade vRouter (Vyatta) でインターフェースに特定のゾーンをバインドします。

`構成`モードで以下のコマンドを使用します。

    set zone-policy zone OUTSIDE description “インターネット・ゾーン”
    set zone-policy zone OUTSIDE default-action drop
    set zone-policy zone OUTSIDE interface bond1
    set zone-policy zone SLSERVICE description “ソフトウェア・サービス”
    set zone-policy zone SLSERVICE default-action drop
    set zone-policy zone SLSERVICE interface bond0
    set zone-policy zone MGMT description “管理 VM & ESX ホスト・アクセス”
    set zone-policy zone MGMT default-action drop
    set zone-policy zone MGMT interface bond0.1101
    set zone-policy zone STORAGE description “ストレージ”
    set zone-policy zone STORAGE default-action drop
    set zone-policy zone STORAGE interface bond0.1102
    set zone-policy zone VMACCESS description “VM アクセス”
    set zone-policy zone VMACCESS default-action drop
    set zone-policy zone VMACCESS interface bond0.1103
    commit
    save

### ゾーンへのファイアウォール・ルールの適用

次に、ゾーン間の通信にファイアウォール・ルールを適用します。

`構成`モードで以下のコマンドを使用します。

    set zone-policy zone OUTSIDE from MGMT firewall name INSIDE2OUTSIDE
    set zone-policy zone OUTSIDE from VMACCESS firewall name INSIDE2OUTSIDE
    set zone-policy zone VMACCESS from OUTSIDE firewall name OUTSIDE2INSIDE
    set zone-policy zone VMACCESS from SLSERVICE firewall name SLSERVICE2INSIDE
    set zone-policy zone MGMT from OUTSIDE firewall name OUTSIDE2INSIDE
    set zone-policy zone MGMT from SLSERVICE firewall name SLSERVICE2INSIDE
    set zone-policy zone SLSERVICE from MGMT firewall name INSIDE2SLSERVICE
    set zone-policy zone SLSERVICE from VMACCESS firewall name INSIDE2SLSERVICE
    set zone-policy zone SLSERVICE from STORAGE firewall name INSIDE2SLSERVICE
    set zone-policy zone STORAGE from SLSERVICE firewall name SLSERVICE2INSIDE
    set zone-policy zone STORAGE from MGMT firewall name MGMT2STORAGE
    commit
    save

## HA ペアの他方の Brocade vRouter (Vyatta) との同期

HA ペアの Brocade vRouter (Vyatta) の一方をセットアップしたため、他方のゲートウェイ・デバイスに変更を同期する必要があります。

`構成`モードで以下のコマンドを使用します。

    set system config-sync remote-router <OTHER BROCADE VROUTER (VYATTA) IP> password <他方の BROCADE VROUTER (VYATTA) のパスワード>
    set system config-sync remote-router <他方の BROCADE VROUTER (VYATTA) の IP> sync-map 'SYNC'
    set system config-sync remote-router <他方の BROCADE VROUTER (VYATTA) の IP> username <他方の BROCADE VROUTER (VYATTA) のユーザー名>
    set system config-sync sync-map SYNC rule 1 action 'include'
    set system config-sync sync-map SYNC rule 1 location 'nat'
    set system config-sync sync-map SYNC rule 2 action 'include'
    set system config-sync sync-map SYNC rule 2 location 'firewall'
    set system config-sync sync-map SYNC rule 3 action 'include'
    set system config-sync sync-map SYNC rule 3 location 'vpn'
    set system config-sync sync-map SYNC rule 4 action 'include'
    set system config-sync sync-map SYNC rule 4 location 'interfaces tunnel'
    set system config-sync sync-map SYNC rule 5 action 'include'
    set system config-sync sync-map SYNC rule 5 location 'firewall'
    set system config-sync sync-map SYNC rule 6 action 'include'
    set system config-sync sync-map SYNC rule 6 location 'zone-policy'
    set system config-sync sync-map SYNC rule 7 action 'include'
    set system config-sync sync-map SYNC rule 7 location 'vpn'
    set system config-sync sync-map SYNC rule 8 action 'include'
    set system config-sync sync-map SYNC rule 8 location 'protocols static route'
    set system config-sync sync-map SYNC rule 9 action 'include'
    set system config-sync sync-map SYNC rule 9 location 'protocols static table'
    set system config-sync sync-map SYNC rule 10 action 'include'
    set system config-sync sync-map SYNC rule 10 location 'policy route'
    set system config-sync sync-map SYNC rule 11 action 'include'
    set system config-sync sync-map SYNC rule 11 location 'nat'
    commit
    save

## VLAN の関連付けおよびルーティング

ゾーンおよびファイアウォール・ルールが Brocade vRouter (Vyatta) でセットアップされた後に、VLAN をそれに関連付け、Brocade vRouter (Vyatta) を介した VLAN のルーティングを有効にする必要があります。

1. IBM Cloud カスタマー・ポータルにログインし、**「ネットワーク」、「ゲートウェイ・アプライアンス (Gateway Appliance)」**をクリックし、Brocade vRouter (Vyatta) をクリックします。
2. VLAN を選択し、**「関連付ける」**をクリックします。
3. ご使用の環境で作成した各 VLAN について、ステップ 2 を繰り返します。VLAN を Brocade vRouter (Vyatta) に関連付けるには、VLAN のルーティング・オプションが有効になっている必要があります。
4. 「関連付けられた VLAN」の下にある VLAN を見つけ、それぞれの横にあるボックスにチェック・マークを付けます。
5. **「一括アクション」**ドロップダウン・メニューをクリックし、**「経路指定」**を選択します。
6. ポップアップ画面で**「OK」**をクリックします。

これで、VLAN が Brocade vRouter (Vyatta) を介してルーティングされました。2 つのゾーン間の通信が阻害されていることに気付いた場合は、問題となっている特定の VLAN の 1 つ以上をバイパスし、Brocade vRouter (Vyatta) の設定を確認してください。

これで、IBM Cloud 内で Brocade vRouter (Vyatta) によって保護された有効なシングル・サイト VMware 環境が用意されました。
