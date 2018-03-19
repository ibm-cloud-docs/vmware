---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Lizenzierungsoptionen für VMware 

VMware-Administratoren können durch die Implementierung in einer auf Unternehmen abgestimmten globalen {{site.data.keyword.BluSoftlayer_full}}-Cloud innerhalb kurzer Zeit kosteneffiziente Hybrid-Cloud-Merkmale realisieren. Ein wichtiges Alleinstellungsmerkmal von {{site.data.keyword.BluSoftlayer_notm}} besteht darin, dass vSphere-Workloads und -Kataloge in VMware vSphere-Umgebungen in {{site.data.keyword.BluSoftlayer_notm}}-Rechenzentren bereitgestellt werden können, ohne VMware-VMs oder -Gastmaschinen zu ändern. Diese Implementierungen werden durch eine einheitliche vSphere-Hypervisor- und Management-/Orchestrierungsplattform ermöglicht.

Zusätzlich zur vSphere 6 Enterprise Plus-Lizenz bietet {{site.data.keyword.BluSoftlayer_notm}} die monatliche Lizenzierung für vCenter, NSX, vRealize, vSAN und Site Recovery Manager (SRM) an.

## VMware vSphere

**Vorgesehener Verwendungszweck:** Betriebssystemplattform für die Bare-Metal-Server-Virtualisierung, die durch Abstrahieren von Prozessor-, Hauptspeicher-, Speicher- und Netzressourcen mehrere virtuelle Server auf einem einzigen physischen Server erstellt. Mehrere physische Server können zu einem Cluster zusammengefasst werden, um eine private Cloud zu erstellen.

**Benutzerschnittstelle:** vCenter-Clients, VMware-API, VMware-CLI

**Features:**
* vMotion-Livemigration
* Hochverfügbarkeit
* Fehlertoleranz
* Replikation
* Nvidia GRID vGPU-Virtualisierung
* Kapazitätsoptimierung für Workloads
* Scheduler für verteilte Ressourcen (Distributed Resources Scheduler, DRS)
* Thin Provisioning
* Netz-E/A-Steuerung

## VMware vCenter

**Vorgesehene Verwendung:** Zentralisierte Verwaltung der Rechenressourcen in jedem vSphere-Host. Im Unterschied zur Einzelverwaltung der vSphere-Hosts ermöglicht die zentralisierte Verwaltung mit vCenter die folgenden Funktionen:

**Benutzerschnittstelle:** Web Client, Thick Client, VMware-API, VMware-CLI

**Features:**
* Zentrale Steuerung und Sichtbarkeit für alle Aspekte verwalteter vSphere-Hosts und virtueller Gastmaschinen.
* Zentrale grafische Schnittstellenansicht für das Computingnetz- und Speichermanagement über den vCenter-Web-Client.
* Proaktive Optimierung. Ermöglicht das Zuordnen und Optimieren von Ressourcen für die maximale Effizienz der vSphere-Hosts.
* Erweiterte Managementfunktion für weitere integrierte Add-ons und Services wie NSX, vRealize, vSAN und Site Recovery Manager (SRM).
* Monitoring, Alerting und Planung. Cloudadministratoren können Ereignisse und Alerts im vCenter-Web-Client anzeigen und geplante Aktionen konfigurieren.
* Automatisierungsengine. vCenter ist die Steuerkomponente (Engine) zum Ausführen der Tasks die von der Webschnittstelle der vSphere-API übermittelt werden. VMware vRealize Automation und vRealize Orchestration sind Beispiele für Anwendungen, die vCenter-Aktionen über die VMware-API steuern.

## VMware NSX

**Vorgesehene Verwendung:** NSX bietet zentrale SDN-Funktionen (SDN = Software-Defined Network) zur Unterstützung von Operationen in der Cloudplattform.

**Benutzerschnittstelle:** vCenter-Clients, VMware-API, VMware-CLI

**Features:**
* Lastausgleich
* Firewalls
* Routing
* Logische Switches
* VPN
* VxLAN-Segmentierung / Tunnelendpunkte

## VMware vRealize

**Vorgesehene Verwendung:** VMware vRealize Suite ist eine auf Unternehmen abgestimmte Cloud-Management-Plattform, mit der Sie eine heterogene Hybrid-Cloud verwalten können.

**Benutzerschnittstelle:** vCenter-Clients, VMware-API, VMware-CLI

**Lizenzierungsmodell:** Pro Prozessor pro Monat

**Features:**
* vRealize Automation: Automatisierte Bereitstellung von personalisierter Infrastruktur, Anwendungen und angepassten IT-Services.
* vRealize Operations: Intelligente Orchestrierung von Status-, Leistungs-, Kapazitäts- und Konfigurationsmanagement.
* vRealize Log Insight: Protokollmanagement und Protokollanalyse in Echtzeit.

## VMware vSAN

**Vorgesehene Verwendung:** VMware vSAN ist eine Lösung für verteilten Speicher und bietet die Möglichkeit, lokale Speicherlaufwerke auf jedem vSphere-Host zu bündeln und in einer Speichereinheit mit exklusiver Nutzung zusammenzufassen, die für alle Hosts in einem vSAN-Cluster zugänglich ist.

**Benutzerschnittstelle:** vCenter-Clients, VMware-API, VMware-CLI

**Features:**
* Verteilter hostbasierter Speicher
* Architektur mit exklusiv genutzten Systemen
* Skaliert bis zu 64 Knoten
* Niedrige Latenzzeiten
* Konfigurierbare Fehlertoleranz

## VMware Site Recovery Manager (SRM)

**Vorgesehene Verwendung:** VMware Site Recovery Manager (SRM) ermöglicht die siteübergreifende Verfügbarkeit und Mobilität von Anwendungen in privaten Cloudumgebungen. Durch die effiziente Nutzung der Kapselung und Isolierung von virtuellen Maschinen vereinfacht Site Recovery Manager die Automatisierung der Disaster-Recovery, um Zielsetzungen für die Wiederherstellungszeit einzuhalten. Darüber hinaus unterstützt SRM die Kostenreduzierung für Business-Continuity-Pläne sowie vorhersagbare Ergebnisse und Risikominimierung bei der Wiederherstellung einer virtuellen Umgebung.

**Benutzerschnittstelle:** vCenter-Clients, VMware-API, VMware-CLI

**Features:**
* Unterbrechungsfreie Wiederherstellungstests
* Automatisierte Orchestrierungsworkflows
* Automatisierte Wiederherstellung von Netz- und Sicherheitseinstellungen
* Erweiterbarkeit für angepasste Automatisierung
* vCenter-übergreifende Orchestrierung für vMotion
* Zentralisierte Wiederherstellungspläne
* Richtlinienbasiertes Management
