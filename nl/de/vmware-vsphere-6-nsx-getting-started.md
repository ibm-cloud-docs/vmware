---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in VMware vSphere 6 NSX 

NSX wird als Lizenzberechtigung implementiert, die Sie auf Ihre Infrastruktur anwenden können. {{site.data.keyword.BluSoftlayer_full}} stellt Lizenzen für einzelne Prozessoren bereit (der Preis ist unabhängig von der Anzahl der Kerne pro CPU). Auf jedem Server, der eine NSX-Komponente verwendet ist eine NSX-Lizent (Management, Control oder Data Plan) erforderlich. NSX fügt zusätzliche Networking-Funktionen zur Plattform hinzu. Sie können ein leistungsfähiges Overlay-Netz für Systemsicherheit, Tenant-Segmentierung und für Hybrid-Cloud-Umgebungen erstellen, die verschiedene Provider umfassen oder von lokalen privaten Clouds ausgehen.
{:shortdesc}

Sie können Firewalls, Lastausgleich, VPN, NAT-Services, VXLAN-basierte Mikrosegmentierung zu Ihrer Umgebung hinzufügen (mit Automatisierungsunterstützung durch die REST-konforme API).

## Lizenzen hinzufügen
Zum Hinzufügen von Lizenzen auf den Servern wird der folgende Prozess verwendet:
1. Melden Sie sich mit dem vSphere-Client bei vCenter Server an.
* Klicken Sie unter **Verwaltung** auf **Lizenzierung**.
* Klicken Sie auf **Lösungen**.
* Klicken Sie in der Produktliste auf **VMware NSX for vSphere**.
* Klicken Sie auf **Lizenzschlüssel** oder **Neuen Lizenzschlüssel eingeben**.
* Klicken Sie auf **OK**.

## NSX installieren

1. NSX Manager implementieren
* Registrieren Sie NSX Manager bei vCenter Server.
* vSphere Web Client implementiert die NSX Controller-Instanzen über NSX Manager.
* Bereiten Sie vSphere-Hosts mit NSX Manager für die Installation von VIBs auf den Hosts im Cluster vor.
* Nach dem Implementieren der NSX Controller-Instanzen auf allen zugehörigen Hosts, definieren und konfigurieren Sie die NSX-Komponenten wie Edge-Gateways, Lastausgleichsfunktionen und Firewalls.

## Hinweise zur Implementierung

Zum Aktivieren von NSX für eine Lösung sind neben den Standardrechenknoten zusätzliche vSphere-Knoten erforderlich.

**NSX Manager**<br />
IBM Informix Virtual Appliance on Management steht in einer 1:1-Beziehung zu vCenter. Normale vSphere-HA-Funktionen werden empfohlen. NSX Manager enthält geplante bzw. bedarfsorientierte Sicherungsfunktionen und erfordert IP-Konnektivität zu vCenter, Controller, NSX Edge-Ressourcen und ESXi-Hosts. NSX Manager wird im selben Teilnetz bzw. VLAN wie vCenter implementiert, ist jedoch nicht zwingend erforderlich. Eine typische VM-Dimensionierung sieht wie folgt aus:

|NSX-Release|vCPU|Speicher|BS-Platte|
|---|---|---|---|
|6.2 Klein|4|12 GB|60 GB|
|6.2 Standard|4|16 GB|60 GB|
|6.2 Groß|4|24 GB|60 GB|
{: caption="Tabelle 1. Typische VM-Dimensionierung für NSX Manager" caption-side="top"}

**NSX-Controllerknoten**<br />
NSX-Controllerknoten werden als virtuelle Appliances über die Benutzerschnittstelle von NSX Manager implementiert. Jede Appliance kommuniziert über eine separate IP-Adresse, die sich normalerweise im selben Teilnetz wie der NSX-Manager befindet (dies ist jedoch nicht zwingend erforderlich). Es wird empfohlen, mindestens drei Controller-VMs auf mindestens drei separaten physischen vSphere-Knoten zu implementieren. Diese werden in einer Aktiv/Aktiv/Aktiv-Konfiguration mit Jobeinteilung ausgeführt, die von NSX Manager definiert wird. Wenn ein Knoten ausfällt, wird eine Funktionsübernahme nach Mehrheitsregeln durchgeführt, um die Workload auf die übrigen Controller zu verteilen. NSX setzt dieses Designverfahren nicht zwingend durch. Sie können mithilfe der nativen Antiaffinitätsregeln von vSphere verhindern, dass mehr als ein Controllerknoten auf demselben ESXi-Server implementiert wird. Eine typische VM-Dimensionierung für die einzelne VMs sieht wie folgt aus:

|Controller-VMs|vCPU|Reservierung|Speicher|BS-Platte|
|---|---|---|---|---|
|3|4|2048 MHz|4 GB|20 GB|
{: caption="Tabelle 2. Typische VM-Dimensionierung für NSX-Controller" caption-side="top"}

**NSX-Switch**
Ein aktualisierter VDS (Virtual Distributed Switch) wird auf allen Hosts implementiert, um verteilte Funktionen bereitzustellen.

**NSX Edge-Services-Gateway**<br />
Wird in der Umgebung nach Bedarf durch Multifunktions-VM-Appliances implementiert. Für die Weiterleitung allein kann ein aktiver Cluster mit bis zu acht Gateways implementiert werden. Für beliebige viele bzw. alle weiteren Services erfolgt die Implementierung als Aktiv/Standby-Implementierung. Für die Kommunikation außerhalb der VM-Umgebung sind für IBM Cloud zugeordnete, portierbare IPs erforderlich, um NAT-Pools, VIPs und VPN-Endpunkte einzuschließen.

|Gateway-Form|vCPU|Speicher|Spezifische Verwendung|
|---|---|---|---|
|Extragroß|6|8 GB|Geeignet für LB mit hoher Leistung auf Ebene 7|
|Quad-Größe|4|1 GB|Geeignet für ECMP- und FW-Implementierung mit hoher Leistung|
|Groß|2|1 GB|Kleine DC & Single Service|
|Kompakt|1|512 MB|Kleine Implementierungen oder Single Service-Nutzung oder POC|
{: caption="Tabelle 3. NSX Edge-Services" caption-side="top"}

