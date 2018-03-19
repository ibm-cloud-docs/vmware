---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  Migration und Upgrade auf VMware vSphere 6

Mit der VMware-Verwaltungskonsole können Sie Ihre VMware-Cloudumgebungen schnell und einfach in ein {{site.data.keyword.BluSoftlayer_full}}-Rechenzentrum erweitern oder verschieben. Die folgenden Schritte bieten einen Leitfaden für die Migration und die Aktualisierung von vSphere-Workloads.
{:shortdesc}

1. Daten zusammenstellen
2. Überprüfen Sie die vorhandene Architektur:
  1. Ressourcennutzung (CPU/Hauptspeicher/Datenträger)
  2. Wachstumsraten verfolgen und prognostizieren
  3. Zukünftig anstehende Projekte identifizieren
  4. Ermitteln, welche zugeordneten VLANs, Teilnetze usw. implementiert (im Steuerportal verfügbar) sind
  5. Ermitteln der selbstdefinierten (privaten) RFC1918-Teilnetze, die für die Lösung verwendet werden
3. Lesen Sie die VMWare 6-Dokumentation und treten Sie VMWare-Communitys bei:
  1. [VMware vSphere-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [VMware Technology Network  ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://communities.vmware.com/welcome){: new_window}
4. Schulen Sie Ihr Administratorteam für die Verwendung und den Support von VMWare 6.
5. Planen und entwerfen Sie eine neue Architektur.
6. Wählen Sie ein auf Konformität ausgerichtetes [Rechenzentrum ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window} aus. Legen Sie in Zusammenarbeit mit dem IBM Cloud-Vertrieb einen besonders geeigneten Standort im Hinblick auf die Verfügbarkeit von Produkten und/oder Services fest.
7. Definieren Sie die erforderlichen VLANs und Teilnetze (portierbare öffentliche und private IP-Adressen).
8. Planen Sie die vSphere-Server:
  1. Prüfen Sie den aktuellen Katalog der IBM Cloud-Server. Empfohlen werden Intel Xeon v3-Server mit redundanten Uplinks, redundanter Stromversorgung und RAID-1 für lokale (Boot-)Platten.
  2. Die meisten VMware-Kunden wenden bei der Kapazität eine unveränderliche Obergrenze von N+1 an (alle VMs können problemlos Servern zugeordnet werden; ein einzelner Knoten wird für Wartung, Störungen usw. vorgehalten).
  3. Viele Kunden würden eine höhere 'weiche Obergrenze' von ca. 80 % (80 % der Kapazität der Serverkonfiguration 'n') gegenüber dem geringeren Standardwert von 60 - 75 % bevorzugen (wegen der kürzeren Rechenzeiten).
  4. Externe Betriebssystemlizenzierung (z. B. für Microsoft oder Red Hat) kann für vSphere-Gastsysteme eines externen Anbieters erforderlich sein.
  5. Lesen Sie die das Dokument [Performance Best Practices for VMware vSphere 6.0 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window}.
9. Planen Sie den vCenter-Server:
  1. In der Regel wird eine virtuelle Serverinstanz (VSI) mittlerer Größe als Einstiegspunkt für kleine Umgebungen verwendet (8 vCPUs + 16 GB RAM). Bare-Metal-Systeme werden für größere Umgebungen verwendet.
  2. vCenter kann auf einer eigenständigen VSI unter Windows als Betriebssystem-Add-on oder als Appliance implementiert werden.
    1. Links zu Referenzinformationen:
        * [vCenter Server 6.0 requirements for installation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://kb.vmware.com/s/article/2107948){: new_window}
        * [VMware vCenter Server Performance and Best Practices ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}
        * [vCenter Server Appliance (vCSA) mit VMware vSphere 6 implementieren und konfigurieren](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. Nicht-VMWare-Server: Ermitteln und entwerfen Sie alle möglicherweise benötigten Nicht-VMWare-Server (virtuelle Server oder Bare-Metal-Server) und schließen Sie diese in die Planung ein.
11. Speicher:
  1. Erstellen Sie einen Plan für den Speicher in der Umgebung. Endurance mit 2 IOPS pro GB und Snapshot-Speicherbereich für die Virtualisierung ist ein guter Ausgangspunkt für die Speicherplanung. Wenn jedoch virtuelle Datenbanken oder andere Anwendungen mit hoher Leistung zum Einsatz kommen, ist die Stufe mit 4 IOPS pro GB besser geeignet. NFS-Speicher wird normalerweise empfohlen.  
  2. Eine Auswahlmatrix finden Sie in [Speicher für die Verwendung mit VMware Systems](select-storage-option-use-vmware.html).
  3. Als sekundäre Maßnahme für zeitpunktgesteuerte Wiederherstellungen wird meist der Snapshot-Speicherbereich verwendet. 10 % sind ein guter Anfangswert, da der Prozess sehr effizient arbeitet und ohne großen Aufwand erweitert werden kann.
12. Sicherungen:
  1. Stellen Sie sicher, dass die vorhandene Sicherungsstrategie funktioniert. Falls keine Sicherungsstrategie vorhanden ist, sollte eine erstellt werden.
  2. Sie können Ihre eigene Sicherungslösung verwenden. Sie können auch die integrierten Sicherungsfunktionen der vSphere Enterprise Plus-Lizenzierung sowie optimierte Lösungen anderer Anbieter (z. B. VEEAM) oder konventionelle IBM Cloud-Backups wie R1Soft verwenden.
13. Entwickeln Sie eine Migrationsstrategie:
  1. Lesen Sie das Dokument [Best practices to install or upgrade to ESXi 6.0 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://kb.vmware.com/s/article/2109712){: new_window}.
  2. Prüfen Sie die vorhandenen DNS- und/oder IP-Konfigurationen und kürzen Sie den TTL-Wert nach Bedarf. 
  3. Entwickeln Sie einen Plan für VMs, der den Quellenhost, den Zielhost, Quellen-IPs, Ziel-IPs und zugehörige DNS-Einträge beinhaltet.
  4. In den meisten Szenarios hat es sich bewährt, die VMs einzeln nacheinander zu migrieren und anschließend die öffentlichen und privaten Netzkonfigurationen zu aktualisieren. Beim Umstellen von alten Versionen auf neue Versionen ist es in der Regel am besten, die VM zu beenden und durch Abhängen/Anhängen (_detach/attach_) zwischen den Umgebungen zu verschieben. Wenn Sie mit verschiedenen Standorten arbeiten, ist vMotion für größere Entfernungen einsetzbar.
  5. Entwickeln Sie Testpläne zum Überprüfen der Umgebung.
  6. Vereinbaren Sie mit den Benutzern ein Zeitfenster für Änderungs- und Wartungsvorgänge. Einzelne VM-Wartungszeiten können für die Datenübertragung, zum Konfigurieren der VM, zum Ändern und Weitergeben von DNS sowie für die Fehlerbehebung genutzt werden.
14. Implementieren Sie die neue Umgebung:
  1. [Einführung in VMware vSphere 6](vmware-vsphere-6-getting-started.html).
  2. Bestellen Sie neue vSphere- und vCenter-Server (sowie alle weiteren Server, die Sie benötigen).
      **Hinweis:** Stellen Sie sicher, dass die richtigen 'nicht gebundenen' Netz-Uplinks ausgewählt sind.
  3. Bestellen und konfigurieren Sie den entsprechenden Speicher: [Architecture Guide for IBM File Storage for IBM Cloud with VMware](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html).
  4. Bestellen Sie neue VLANs und portierbare Teilnetze (möglicherweise sind ausführliche Architekturdiagramme und Begründungen erforderlich).
  5. Konfigurieren Sie vCenter für die Kommunikation mit vSphere-Servern und konfigurieren Sie die Umgebung.
  6. Erstellen Sie Sicherungen in der Liveumgebung.
  7. Führen Sie den Migrationsplan und die zugehörigen Testpläne durch.
  8. Implementieren Sie Sicherungen in der neuen Umgebung.
  9. Nehmen Sie die neue Umgebung in Betrieb.
  10. Setzen Sie die vorherige Umgebung außer Betrieb.
