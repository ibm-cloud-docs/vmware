---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration du routeur virtuel Brocade vRouter (Vyatta) pour des environnements VMware avec QuantaStor

Vous pouvez configurer un routeur virtuel Brocade vRouter (dispositif Brocade vRouter (Vyatta) [configuration à haute disponibilité (HA)] au sein d'un environnement VMware qui utilise QuantaStor. Servez-vous des informations suivantes avec le manuel d'instructions [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) pour configurer l'une des options de stockage dans votre environnement VMware.
{:shortdesc}

La passerelle Brocade vRouter (Vyatta) sert de passerelle et de routeur pour votre environnement ; elle contient des segments composés de sous-réseaux. Des règles de pare-feu sont mises en place entre les segments afin qu'ils puissent communiquer entre eux. Pour les segments qui n'ont pas besoin de communiquer avec d'autres, aucune règle de pare-feu n'est nécessaire car tous les paquets sont supprimés.

Dans l'exemple de configuration, cinq segments ont été créés dans le dispositif Brocade vRouter (Vyatta) :

* SLSERVICE – services {{site.data.keyword.BluSoftlayer_full}} 
* VMACCESS – machines virtuelles sur le cluster de capacité
* MGMT – clusters de gestion et de capacité, ainsi que machines virtuelles de gestion
* STORAGE – serveur(s) de stockage
* OUTSIDE – accès Internet public

La Figure 1 représente la communication entre chaque zone. **Remarque :** Il est possible que votre environnement soit différent et nécessite des zones et des règles de pare-feu différentes.

![Figure 1: Brocade vRouter (Vyatta) - Configuration de zone](images/brocade_figure1.png "Brocade vRouter (Vyatta) - Configuration de zone") Figure 1. Brocade vRouter (Vyatta) - Configuration de zone

## Configuration du routeur virtuel Brocade vRouter (Vyatta)

Pour configurer le routeur virtuel Brocade vRouter (Vyatta), procédez comme suit :

1. Accédez via Secure Shell au dispositif en utilisant le mot de passe root qui figure sur l'écran Détails de l'unité.
2. Tapez 'Configure' pour passer en mode configuration et suivez la procédure des sections suivantes.

### Configuration des interfaces

Vous configurez les interfaces de liaison sur les routeurs Brocade vRouter (Vyatta) pour que ceux-ci soient liés aux sous-réseaux de l'environnement. Vous devez remplacer les réseaux locaux virtuels (1101, 1102 et 1103) par les VLAN correspondants de votre environnement. Notez également que les instructions où figure '<>' doivent être remplacées par les détails de votre environnement (en supprimant '<>').

Utilisez les commandes suivantes pour configurer les interfaces de liaison sur les routeurs Brocade vRouter (Vyatta). Vous devez être en mode `configure`.

#### Routeur virtuel Brocade vRouter (Vyatta) 1
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

#### Routeur virtuel Brocade vRouter (Vyatta) 2
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

### Configuration de SNAT pour l'accès externe

Vous configurez SNAT pour la gestion de machines virtuelles et pour que les machines virtuelles sur le cluster de capacité puissent accéder à Internet. La configuration doit alors être effectuée uniquement sur le routeur virtuel Brocade vRouter (Vyatta) car la configuration de la synchronisation est effectuée ultérieurement.

Utilisez les commandes suivantes en mode `configure` :

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

### Configuration de groupes de pare-feux

Vous allez ensuite configurer les groupes de pare-feux qui sont associés à certaines plages d'adresses IP.

Utilisez les commandes suivantes en mode `configure` :

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

### Configuration des règles de nom de pare-feu

Vous allez à présent définir les règles de pare-feu pour chaque sens du trafic.

Utilisez les commandes suivantes en mode `configure` :

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

### Configuration de liaisons de zone

Pour cette étape, vous allez lier des zones particulières à des interfaces sur le routeur virtuel Brocade vRouter (Vyatta).

Utilisez les commandes suivantes en mode `configure` :

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

### Application des règles de pare-feu aux zones

Vous allez à présent appliquer les règles de pare-feu aux communications entre zones.

Utilisez les commandes suivantes en mode `configure` :

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

## Synchronisation avec l'autre routeur virtuel Brocade vRouter (Vyatta) dans la paire haute disponibilité

Comme vous avez configuré l'un des routeurs virtuels Brocade vRouter (Vyatta) dans la paire à haute disponibilité, vous devez synchroniser les changements sur l'autre dispositif de passerelle.

Utilisez les commandes suivantes en mode `configure` :

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

## Association et routage de réseaux locaux virtuels

Une fois les zones et les règles de pare-feu configurées sur le routeur virtuel Brocade vRouter (Vyatta), vous devez y associer les réseaux locaux virtuels (VLAN) et activer le routage des VLAN via le routeur Brocade vRouter (Vyatta).

1. Connectez-vous au portail client IBM Cloud et cliquez sur **Réseau, Dispositif de passerelle** puis cliquez sur le routeur virtuel Brocade vRouter (Vyatta).
2. Sélectionnez un réseau local virtuel et cliquez sur **Associer**.
3. Répétez l'étape 2 pour chaque VLAN créé pour votre environnement. Les réseaux locaux virtuels doivent avoir l'option de routage activée pour être associés au routeur virtuel Brocade vRouter (Vyatta).
4. Localisez les VLAN sous VLAN associés et cochez la case en regard de chacun d'eux.
5. Cliquez sur le menu déroulant **Actions groupées** et sélectionnez **Router**.
6. Cliquez sur **OK** dans le menu contextuel. 

Vos réseaux locaux virtuels sont à présent routés via le routeur virtuel Brocade vRouter (Vyatta). Si vous constatez que la communication est gênée entre deux zones, ignorez un ou plusieurs des VLAN concernés et vérifiez les paramètres de votre routeur Brocade vRouter (Vyatta).

Vous disposez désormais d'un environnement VMware mono-site fonctionnel, sécurisé par un routeur virtuel Brocade vRouter (Vyatta) au sein d'IBM Cloud.
