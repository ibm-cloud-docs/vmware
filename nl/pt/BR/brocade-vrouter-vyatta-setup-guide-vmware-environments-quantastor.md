---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configurando o Brocade vRouter (Vyatta) para ambientes VMware com QuantaStor

É possível configurar um dispositivo Brocade vRouter (Vyatta) [configuração de alta disponibilidade (HA)] dentro de um ambiente VMware que está usando QuantaStor. Use as informações a seguir com o [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) para configurar uma dessas opções de armazenamento em seu ambiente VMware.
{:shortdesc}

O gateway Brocade vRouter (Vyatta) serve como um gateway e roteador para seu ambiente e contém zonas que consistem em sub-redes. As regras de firewall são configuradas entre zonas para que elas possam se comunicar entre si. Para aquelas zonas que não precisam se comunicar com outras zonas, nenhuma regra de firewall é necessária pois todos os pacotes são eliminados.

Na configuração de exemplo, há cinco zonas que são criadas no Brocade vRouter (Vyatta):

* SLSERVICE – Serviços do {{site.data.keyword.BluSoftlayer_full}}
* VMACCESS – Máquinas virtuais (VMs) no cluster de capacidade
* MGMT – Clusters de gerenciamento e de capacidade, bem como VMs de gerenciamento
* STORAGE – Servidores de armazenamento
* OUTSIDE – Acesso de Internet pública

A Figura 1 descreve a comunicação entre cada zona. **Nota:** seu ambiente pode ser diferente e pode requerer diferentes zonas e regras de firewall.

![Figure 1: configuração de zona do Brocade vRouter (Vyatta)](images/brocade_figure1.png "Configuração de zona do Brocade vRouter (Vyatta)") Figura 1. Configuração de zona do Brocade vRouter (Vyatta)

## Configurando o Brocade vRouter (Vyatta)

Para configurar o Brocade vRouter (Vyatta), siga estas etapas:

1. Efetue SSH no dispositivo usando a senha raiz que está localizada na tela Detalhes do dispositivo.
2. Digite 'Configurar' para entrar no modo de configuração e siga as etapas nas seções subsequentes.

### Configurando interfaces

É possível configurar as interfaces de ligação em ambos os Brocade vRouters (Vyatta) para serem vinculadas à sub-rede no ambiente. É necessário substituir as VLANs (1101, 1102 e 1103) pelas VLANs correspondentes em seu ambiente. Além disso, observe que instruções que são feitas com '<>' devem ser substituídas por detalhes de seu ambiente (com o '<>' removido).

Use os comandos a seguir para configurar as interfaces de ligação no Brocade vRouters (Vyatta). Deve-se estar no modo de `configuração`.

#### Brocade vRouter (Vyatta) 1
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

#### Brocade vRouter (Vyatta) 2
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

### Configurando o SNAT para acesso externo

É possível configurar o SNAT de forma que as VMs de gerenciamento e as VMs no cluster de capacidade possam acessar a Internet. Nessa etapa, a configuração precisa ser feita em apenas um Brocade vRouter (Vyatta) pois a sincronização da configuração ocorre posteriormente.

Use os comandos a seguir no modo `configure`:

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

### Configurando grupos de firewalls

Em seguida, você configurará os grupos de firewalls que estão associados a determinados intervalos de IP.

Use os comandos a seguir no modo `configure`:

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

### Configurando regras de nome de firewall

Agora você definirá as regras de firewall para cada direção de tráfego.

Use os comandos a seguir no modo `configure`:

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

### Configurando ligações de zona

Nesta etapa, você ligará zonas específicas a interfaces no Brocade vRouter (Vyatta).

Use os comandos a seguir no modo `configure`:

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

### Aplicando regras de firewall em zonas

Agora você aplicará as regras de firewall à comunicação entre zonas.

Use os comandos a seguir no modo `configure`:

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

## Sincronizando com outro Brocade vRouter (Vyatta) no par de HA

Como você configurou um dos Brocade vRouters (Vyatta) no par de HA, sincronize as mudanças no outro dispositivo de gateway.

Use os comandos a seguir no modo `configure`:

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

## Associando e roteando VLANs

Após as zonas e regras de firewall serem configuradas no Brocade vRouter (Vyatta), deve-se associar as VLANs a ele e ativar o roteamento das VLANs por meio do Brocade vRouter (Vyatta).

1. Efetue login no portal do cliente do IBM Cloud e clique em **Rede, Dispositivo de gateway** e clique no Brocade vRouter (Vyatta).
2. Selecione uma VLAN e clique em **Associar**.
3. Repita a etapa 2 para cada VLAN que você criou para seu ambiente. As VLANs devem ter a opção de roteamento ativada para serem associadas ao Brocade vRouter (Vyatta).
4. Localize as VLANs em VLANs associadas e marque a caixa próxima a cada uma.
5. Clique no menu suspenso **Ações em massa** e selecione **Rotear**.
6. Clique em **OK** na tela pop-up.

Suas VLANs agora são roteadas por meio do Brocade vRouter (Vyatta). Se você observar que a comunicação foi prejudicada entre duas zonas, ignore uma ou mais VLANs específicas em questão e verifique as configurações de seu Brocade vRouter (Vyatta).

Agora você tem um ambiente VMware de site único ativo protegido por um Brocade vRouter (Vyatta) dentro do IBM Cloud.
