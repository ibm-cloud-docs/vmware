---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# QuantaStor를 사용하는 VMware 환경에 대한 Brocade vRouter(Vyatta) 설정

QuantaStor를 사용 중인 VMware 환경에서 Brocade vRouter(Vyatta) 어플라이언스 [고가용성(HA) 구성]을 구성할 수 있습니다. [고급 단일 사이트 VMware 참조 아키텍처](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html)의 다음 정보를 사용하여 VMware 환경에 이러한 스토리지 옵션 중 하나를 설정하십시오.
{:shortdesc}

Brocade vRouter(Vyatta) 게이트웨이는 사용자 환경에 대한 게이트웨이 및 라우터로 제공되며 서브넷으로 구성된 구역을 포함합니다. 방화벽 규칙은 서로 통신할 수 있도록 구역 간에 설정됩니다. 다른 구역과 통신할 필요가 없는 구역에 대해서는 모든 패킷이 삭제되므로 방화벽 규칙이 필요하지 않습니다. 

예제 구성의 경우 Brocade vRouter(Vyatta)에서 작성되는 다섯 개의 구역이 있습니다.

* SLSERVICE – {{site.data.keyword.BluSoftlayer_full}} 서비스
* VMACCESS – 용량 클러스터의 가상 머신(VM)
* MGMT – 관리 VM 뿐만 아니라 관리 및 용량 클러스터
* STORAGE – 스토리지 서버
* OUTSIDE – 공용 인터넷 액세스

그림 1에서는 각 구역 간의 통신을 표시합니다. **참조:** 환경은 서로 다를 수 있으며 다른 구역과 방화벽 규칙이 필요할 수 있습니다.

![그림 1: Brocade vRouter(Vyatta) 구역 구성](images/brocade_figure1.png "Brocade vRouter(Vyatta) 구역 구성") 그림 1. Brocade vRouter(Vyatta) 구역 구성

## Brocade vRouter(Vyatta) 구성

Brocade vRouter(Vyatta)를 구성하려면 다음 단계를 수행하십시오.

1. 디바이스 세부사항 화면에서 확인한 루트 비밀번호를 사용하여 어플라이언스에 SSH를 추가하십시오.
2. 구성 모드로 변경하려면 'Configure'를 입력하고 이후 섹션에 있는 단계를 따르십시오. 

### 인터페이스 설정

환경의 서브넷으로 링크될 두 Brocade vRouters(Vyatta)에서 본드 인터페이스를 구성합니다. VLAN(1101, 1102 및 1103)을 사용자 환경의 해당 VLAN으로 바꿔야 합니다. 또한 '<>'로 작성된 지시사항은 사용자 환경의 세부사항으로 대체해야 합니다('<>' 제거).

다음 명령을 사용하여 Brocade vRouters(Vyatta)에서 본드 인터페이스를 구성하십시오. `configure` 모드여야 합니다. 

#### Brocade vRouter(Vyatta) 1
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Enter an IP address from Primary Private Subnet Bound to VLAN 1101/Management)
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1101/Management VMs)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1102/Storage Path A)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1102/Storage Path B)
    set interfaces bonding bond0 vif 1103 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1103/Virtual Machines)
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 advertise-interval '1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 preempt 'false'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 priority '253'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY ADDRESS/MASK of Primary Private VLAN Bound to 1101/Management>’
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY ADDRESS/MASK of Portable Private VLAN Bound to 1101/Management VMs>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 advertise-interval '1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 preempt 'false'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 priority '253'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY ADDRESS/MASK of Primary Private VLAN Bound to 1102/Storage>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY
    ADDRESS/MASK of Portable Private VLAN Bound to 1102/Storage Path A>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY ADDRESS/MASK of Portable Private VLAN Bound to 1102/Storage Path B>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 advertise-interval '1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 preempt 'false'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 priority '253'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY ADDRESS/MASK of Primary Private VLAN Bound to 1103/Virtual Machines>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY ADDRESS/MASK of Portable Private VLAN Bound to 1103/Virtual Machines>’
    commit
    save

#### Brocade vRouter(Vyatta) 2
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Enter an IP address from Primary Private Subnet Bound to VLAN 1101/Management. Must be different than the one assigned to Brocade vRouter (Vyatta 1)
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1101/Management VMs. Must be different than the one assigned to Brocade vRouter (Vyatta 1)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1102/Storage Path A. Must be different than the one assigned to Brocade vRouter (Vyatta 1)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1102/Storage Path B. Must be different than the one assigned to Brocade vRouter (Vyatta 1)
    set interfaces bonding bond0 vif 1103 address ‘##.###.###.###/##’ (Enter an IP address from Portable Private Subnet Bound to VLAN 1103/Virtual Machines. Must be different than the one assigned to Brocade vRouter (Vyatta 1)
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 advertise-interval '1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 preempt 'false'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 priority '253'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY ADDRESS/MASK of Primary Private VLAN Bound to 1101/Management>’
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY ADDRESS/MASK of Portable Private VLAN Bound to 1101/Management VMs>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 advertise-interval '1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 preempt 'false'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 priority '253'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY ADDRESS/MASK of Primary Private VLAN Bound to 1102/Storage>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY ADDRESS/MASK of Portable Private VLAN Bound to 1102/Storage Path A>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY ADDRESS/MASK of Portable Private VLAN Bound to 1102/Storage Path B>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 advertise-interval '1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 preempt 'false'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 priority '253'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY ADDRESS/MASK of Primary Private VLAN Bound to 1103/Virtual Machines>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY ADDRESS/MASK of Portable Private VLAN Bound to 1103/Virtual Machines>’
    commit
    save

### 외부 액세스에 대한 SNAT 구성

관리 VM 및 용량 클러스터의 VM이 인터넷에 액세스할 수 있도록 SNAT를 구성합니다. 이 단계부터 설정 동기화가 나중에 발생하므로 하나의 Brocade vRouter(Vyatta)에서만 구성을 수행해야 합니다. 

`configure` 모드에서 다음 명령을 사용하십시오.

    set nat source rule 10
    set nat source rule 10 source address ##.###.###.###/## (Portable Private Subnet VLAN1101/Management VMs)
    set nat source rule 10 translation address ##.###.###.### (Brocade vRouter (Vyatta) bond1 IP)
    set nat source rule 10 outbound-interface bond1
    set nat source rule 20
    set nat source rule 20 source address ##.###.###.###/## (Portable Private Subnet VLAN1103/Virtual Machines)
    set nat source rule 20 translation address ##.###.###.### (Brocade vRouter (Vyatta) bond1 IP)
    set nat source rule 20 outbound-interface bond1
    commit
    save

### 방화벽 그룹 구성

다음으로 특정 IP 범위와 연관된 방화벽 그룹을 구성합니다. 

`configure` 모드에서 다음 명령을 사용하십시오.

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
    set firewall group network-group 1101PRIMARY network ###.###.###.### (Primary Private Subnet 1101/Management)
    set firewall group network-group 1101MGMT network ###.###.###.### (Portable Private Subnet 1101/Management VMs)
    set firewall group network-group 1102PRIMARY network ###.###.###.### (Primary Private Subnet 1102/Storage)
    set firewall group network-group 1102STORAGEA network ###.###.###.### (Portable Private Subnet 1102/Storage Path A)
    set firewall group network-group 1102STORAGEB network ###.###.###.### (Portable Private Subnet 1102/Storage Path B)
    set firewall group network-group 1103VMACCESS network ###.###.###.### (Portable Private Subnet 1103/Virtual Machines)
    commit
    save

### 방화벽 이름 규칙 구성

이제 트래픽의 각 방향에 대해 방화벽 규칙을 정의합니다. 

`configure` 모드에서 다음 명령을 사용하십시오.

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

### 구역 바인딩 구성

이 단계에서 특정 구역을 Brocade vRouter(Vyatta)의 인터페이스로 바인딩합니다.

`configure` 모드에서 다음 명령을 사용하십시오.

    set zone-policy zone OUTSIDE description “Internet Zone”
    set zone-policy zone OUTSIDE default-action drop
    set zone-policy zone OUTSIDE interface bond1
    set zone-policy zone SLSERVICE description “SoftLayer Services”
    set zone-policy zone SLSERVICE default-action drop
    set zone-policy zone SLSERVICE interface bond0
    set zone-policy zone MGMT description “Management VMs & ESX Host Access”
    set zone-policy zone MGMT default-action drop
    set zone-policy zone MGMT interface bond0.1101
    set zone-policy zone STORAGE description “Storage”
    set zone-policy zone STORAGE default-action drop
    set zone-policy zone STORAGE interface bond0.1102
    set zone-policy zone VMACCESS description “VM Access”
    set zone-policy zone VMACCESS default-action drop
    set zone-policy zone VMACCESS interface bond0.1103
    commit
    save

### 구역에 방화벽 규칙 적용

이제 방화벽 규칙을 구역 간의 통신에 적용합니다. 

`configure` 모드에서 다음 명령을 사용하십시오.

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

## HA 쌍에서 다른 Brocade vRouter(Vyatta)와 동기화

HA 쌍에서 Brocade vRouter(Vyatta) 중 하나를 설정했으므로 다른 게이트웨이 디바이스에 변경사항을 동기화해야 합니다. 

`configure` 모드에서 다음 명령을 사용하십시오.

    set system config-sync remote-router <OTHER BROCADE VROUTER (VYATTA) IP> password <OTHER BROCADE VROUTER (VYATTA) PASSWORD>
    set system config-sync remote-router <OTHER BROCADE VROUTER (VYATTA) IP> sync-map 'SYNC'
    set system config-sync remote-router <OTHER BROCADE VROUTER (VYATTA) IP> username <OTHER BROCADE VROUTER (VYATTA) USERNAME>
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

## VLAN 연관 및 라우팅

구역과 방화벽 규칙이 Brocade vRouter(Vyatta)에 설정되고 나면, VLAN을 연관시키고 Brocade vRouter(Vyatta)를 통해 VLAN의 라우팅을 사용 가능하도록 설정해야 합니다.

1. IBM Cloud 고객 포털에 로그인하고 **네트워크, 게이트웨이 어플라이언스**를 클릭한 후 Brocade vRouter(Vyatta)를 클릭하십시오.
2. VLAN을 선택하고 **연관**을 클릭하십시오.
3. 환경에 대해 작성한 각 VLAN에 대해 2단계를 반복하십시오. VLAN에는 Brocade vRouter(Vyatta)와 연관시킬 라우팅 옵션이 사용으로 설정되어 있어야 합니다.
4. 연관된 VLAN 아래에서 해당 VLAN을 찾고 각 항목 옆에 있는 상자를 선택하십시오.
5. **벌크 조치** 드롭 다운 메뉴를 클릭하고 **라우트**를 선택하십시오.
6. 팝업 화면에서 **확인**을 클릭하십시오.

이제 VLAN이 Brocade vRouter(Vyatta)를 통해 라우팅됩니다. 두 구역 간에 통신이 방해받는 경우 문제가 되는 하나 이상의 특정 VLAN을 무시하고 Brocade vRouter(Vyatta) 설정을 확인하십시오. 

이제 IBM Cloud 내에서 Brocade vRouter(Vyatta)에 의해 보안이 설정된 단일 사이트 VMware 환경이 작동합니다. 
