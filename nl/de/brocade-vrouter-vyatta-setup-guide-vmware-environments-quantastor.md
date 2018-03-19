---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Brocade vRouter (Vyatta) für VMware-Umgebungen mit QuantaStor einrichten

Sie können eine Brocade vRouter-Appliance (Vyatta-Appliance) [mit Konfiguration für Hochverfügbarkeit (High Availability, HA)] in einer VMware-Umgebung konfigurieren, in der QuantaStor verwendet wird. Verwenden Sie die folgenden Informationen mit dem Cookbook [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html), um eine dieser Speicheroptionen in Ihrer VMware-Umgebung einzurichten.
{:shortdesc}

Das Brocade vRouter-Gateway (Vyatta-Gateway) dient als Gateway und Router für Ihre Umgebung und enthält Zonen, die aus Teilnetzen bestehen. Zwischen den Zonen werden entsprechende Firewallregeln definiert, damit die Zonen miteinander kommunizieren können. Für Zonen, die nicht mit anderen Zonen kommunizieren müssen, werden keine Firewallregeln benötigt, da alle übertragenen Pakete gelöscht werden.

Die Beispielkonfiguration enthält fünf Zonen, die in Brocade vRouter (Vyatta) erstellt werden:

* SLSERVICE – {{site.data.keyword.BluSoftlayer_full}}-Services
* VMACCESS – Virtuelle Maschinen (VMs) im Kapazitätscluster
* MGMT – Management- und Kapazitätscluster sowie Management-VMs
* STORAGE – Speicherserver
* OUTSIDE – Öffentlicher Internetzugang

Abbildung 1 beschreibt die Kommunikation zwischen den einzelnen Zonen. **Hinweis:** Ihre Umgebung kann von diesem Beispiel abweichen und andere Zonen und Firewallregeln erfordern.

![Abbildung 1: Zonenkonfiguration für Brocade vRouter (Vyatta)](images/brocade_figure1.png "Zonenkonfiguration für Brocade vRouter (Vyatta)") Abbildung 1. Zonenkonfiguration für Brocade vRouter (Vyatta)

##  Brocade vRouter (Vyatta) konfigurieren

Führen Sie die folgenden Schritte aus, um Brocade vRouter (Vyatta) zu konfigurieren:

1. Greifen Sie über SSH mit dem in der Anzeige 'Einheitendetails' angegebenen Rootkennwort auf die Appliance zu.
2. Geben Sie 'Konfigurieren' ein, um den Konfigurationsmodus zu aktivieren und führen Sie die in den nachfolgenden Abschnitten angegebenen Schritte aus.

### Schnittstellen einrichten

Sie konfigurieren die bond-Schnittstellen in beiden Instanzen von Brocade vRouter (Vyatta), die mit den Teilnetzen in der Umgebung verknüpft werden sollen. Dabei müssen Sie die VLANs (1101, 1102 und 1103) durch die entsprechenden VLANs in Ihrer Umgebung ersetzen. Außerdem müssen die Anweisungen mit der Markierung '<>' durch die Details für Ihre Umgebung ohne die Markierung '<>' ersetzt werden.

Verwenden Sie die folgenden Befehle, um die bond-Schnittstellen in den Instanzen von Brocade vRouter (Vyatta) zu konfigurieren. Dabei muss der Konfigurationsmodus (`configure`) aktiviert sein.

#### Brocade vRouter (Vyatta) 1
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des primären privaten Teilnetzes an, das an VLAN 1101/Management gebunden ist)
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1101/Management-VMs gebunden ist)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1102/Speicherpfad A gebunden ist)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1102/Speicherpfad B gebunden ist)
    set interfaces bonding bond0 vif 1103 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1103/Virtuelle Maschinen gebunden ist)
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 advertise-interval '1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 preempt 'false'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 priority '253'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des primären privaten VLANs, das an 1101/Management gebunden ist>’
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANS, das an 1101/Management-VMs gebunden ist>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 advertise-interval '1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 preempt 'false'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 priority '253'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des primären privaten VLANs, das an 1102/Speicher gebunden ist>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANs, das an 1102/Speicherpfad A gebunden ist>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANs, das an 1102/Speicherpfad B gebunden ist>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 advertise-interval '1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 preempt 'false'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 priority '253'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des primären privaten VLANs, das an 1103/Virtual Machines gebunden ist>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANs, das an 1103/Virtuelle Maschinen gebunden ist>’
    commit
    save

#### Brocade vRouter (Vyatta) 2
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des primären privaten Teilnetzes an, das an VLAN 1101/Management gebunden ist. Muss sich von der Adresse unterscheiden, die der Brocade vRouter-Instanz (Vyatta 1) zugeordnet ist.)
    set interfaces bonding bond0 vif 1101 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1101/Management-VMs gebunden ist. Muss sich von der Adresse unterscheiden, die der Brocade vRouter-Instanz (Vyatta 1) zugeordnet ist.)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1102/Speicherpfad A gebunden ist. Muss sich von der Adresse unterscheiden, die der Brocade vRouter-Instanz (Vyatta 1) zugeordnet ist.)
    set interfaces bonding bond0 vif 1102 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1102/Speicherpfad B gebunden ist. Muss sich von der Adresse unterscheiden, die der Brocade vRouter-Instanz (Vyatta 1) zugeordnet ist.)
    set interfaces bonding bond0 vif 1103 address ‘##.###.###.###/##’ (Geben Sie eine IP-Adresse des portierbaren privaten Teilnetzes an, das an VLAN 1103/Virtuelle Maschinen gebunden ist. Muss sich von der Adresse unterscheiden, die der Brocade vRouter-Instanz (Vyatta 1) zugeordnet ist.)
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 advertise-interval '1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 preempt 'false'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 priority '253'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des primären privaten VLANs, das an 1101/Management gebunden ist>’
    set interfaces bonding bond0 vif 1101 vrrp vrrp-group 2 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANS, das an 1101/Management-VMs gebunden ist>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 advertise-interval '1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 preempt 'false'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 priority '253'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des primären privaten VLANs, das an 1102/Speicher gebunden ist>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANs, das an 1102/Speicherpfad A gebunden ist>’
    set interfaces bonding bond0 vif 1102 vrrp vrrp-group 3 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANs, das an 1102/Speicherpfad B gebunden ist>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 advertise-interval '1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 preempt 'false'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 priority '253'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 'rfc3768-compatibility'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 sync-group 'vgroup1'
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des primären privaten VLANs, das an 1103/Virtual Machines gebunden ist>’
    set interfaces bonding bond0 vif 1103 vrrp vrrp-group 4 virtual-address ‘<GATEWAY-ADRESSE/-MASKE des portierbaren privaten VLANs, das an 1103/Virtuelle Maschinen gebunden ist>’
    commit
    save

### SNAT für externen Zugriff konfigurieren

Sie konfigurieren SNAT so, dass Management-VMs und VMs im Kapazitätscluster auf das Internet zugreifen können. Ab diesem Schritt muss die Konfiguration nur auf einem Brocade vRouter (Vyatta) durchgeführt werden, da die Konfigurationen später synchronisiert werden.

Verwenden Sie die folgenden Befehle im Konfigurationsmodus (`configure`):

    set nat source rule 10
    set nat source rule 10 source address ##.###.###.###/## (portierbares privates Teilnetz VLAN1101/Management-VMs)
    set nat source rule 10 translation address ##.###.###.### (Brocade vRouter (Vyatta) bond1 IP)
    set nat source rule 10 outbound-interface bond1
    set nat source rule 20
    set nat source rule 20 source address ##.###.###.###/## (portierbares privates Teilnetz VLAN1103/virtuelle Maschinen)
    set nat source rule 20 translation address ##.###.###.### (Brocade vRouter (Vyatta) bond1 IP)
    set nat source rule 20 outbound-interface bond1
    commit
    save

### Firewallgruppen konfigurieren

Als Nächstes konfigurieren Sie die Firewallgruppen, die bestimmten IP-Bereichen zugeordnet sind.

Verwenden Sie die folgenden Befehle im Konfigurationsmodus (`configure`):

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
    set firewall group network-group 1101PRIMARY network ###.###.###.### (primäres privates Teilnetz 1101/Management)
    set firewall group network-group 1101MGMT network ###.###.###.### (portierbares privates Teilnetz 1101/Management-VMs)
    set firewall group network-group 1102PRIMARY network ###.###.###.### (primäres privates Teilnetz 1102/Speicher)
    set firewall group network-group 1102STORAGEA network ###.###.###.### (portierbares privates Teilnetz 1102/Speicherpfad A)
    set firewall group network-group 1102STORAGEB network ###.###.###.### (portierbares privates Teilnetz 1102/Speicherpfad B)
    set firewall group network-group 1103VMACCESS network ###.###.###.### (portierbares privates Teilnetz 1103/virtuelle Maschinen)
    commit
    save

### Firewallnamensregeln konfigurieren

Sie definieren nun die Firewallregeln für jede Richtung des Datenverkehrs.

Verwenden Sie die folgenden Befehle im Konfigurationsmodus (`configure`):

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

### Zonenbindungen konfigurieren

In diesem Schritt binden Sie bestimmte Zonen an Schnittstellen im Brocade vRouter (Vyatta).

Verwenden Sie die folgenden Befehle im Konfigurationsmodus (`configure`):

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

### Firewallregeln auf Zonen anwenden

Als Nächstes wenden Sie die Firewallregeln auf die Kommunikation zwischen Zonen an.

Verwenden Sie die folgenden Befehle im Konfigurationsmodus (`configure`):

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

## Synchronisation mit zweitem Brocade vRouter (Vyatta) im HA-Paar

Nachdem Sie eine Brocade vRouter-Instanz (Vyatta-Instanz) in dem HA-Paar eingerichtet haben, müssen Sie die Änderungen mit der zweiten Gateway-Einheit synchronisieren.

Verwenden Sie die folgenden Befehle im Konfigurationsmodus (`configure`):

    set system config-sync remote-router <OTHER BROCADE VROUTER (VYATTA) IP> password <KENNWORT FÜR ANDEREN BROCADE VROUTER (VYATTA)>
    set system config-sync remote-router <OTHER BROCADE VROUTER (VYATTA) IP> sync-map 'SYNC'
    set system config-sync remote-router <OTHER BROCADE VROUTER (VYATTA) IP> username <BENUTZERNAME FÜR ANDEREN BROCADE VROUTER (VYATTA)>
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

## VLANs zuordnen und weiterleiten

Nachdem die Zonen und Firewallregeln auf dem Brocade vRouter (Vyatta) eingerichtet sind, müssen Sie die VLANs zuordnen und die Weiterleitung der VLANs über den Brocade vRouter (Vyatta) aktivieren.

1. Melden Sie sich beim IBM Cloud-Kundenportal an, klicken Sie auf **Netz > Gateway-Appliance** und anschließend auf den Brocade vRouter (Vyatta).
2. Wählen Sie ein VLAN aus und klicken Sie auf **Zuordnen**.
3. Wiederholen Sie Schritt 2 für jedes VLAN, das Sie für Ihre Umgebung erstellt haben. Für die VLANs muss die Routing-Option aktiviert sein, damit sie dem Brocade vRouter (Vyatta) zugeordnet werden können.
4. Lokalisieren Sie die VLANs unter 'Zugeordnete VLANs' und aktivieren Sie die Kästchen neben den einzelnen VLANs.
5. Klicken Sie auf das Dropdown-Menü **Massenaktionen** und wählen Sie **Route** aus.
6. Klicken Sie im Dialogfenster auf **OK**.

Ihre VLANs werden jetzt über den Brocade vRouter (Vyatta) weitergeleitet. Wenn Sie feststellen, dass die Kommunikation zwischen zwei Zonen behindert wird, umgehen Sie eines oder mehrere der betreffenden VLANs und überprüfen Sie die Einstellungen für Ihren Brocade vRouter (Vyatta).

Sie verfügen nun über eine funktionsfähige Single-Site-VMware-Umgebung, die durch einen Brocade vRouter (Vyatta) in IBM Cloud geschützt wird.
