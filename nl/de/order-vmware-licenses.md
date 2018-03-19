---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware-Lizenzen bestellen

VMware-Administratoren können durch die Implementierung in {{site.data.keyword.BluSoftlayer_full}} innerhalb kurzer Zeit die kosteneffizienten Hybrid-Cloud-Merkmale realisieren. Eines dieser Merkmale besteht darin, dass vSphere-Workloads und -Kataloge für VMware vSphere-Umgebungen ohne Änderungen an VMware-VMs oder -Gastmaschinen in {{site.data.keyword.cloud_notm}}-Rechenzentren bereitgestellt werden können. Diese Implementierungen werden durch eine einheitliche vSphere-Hypervisor- und Management-/Orchestrierungsplattform ermöglicht.
{:shortdesc}

Die vSphere-Implementierung ermöglicht auch die Verwendung anderer Komponenten. Tabelle 1 enthält eine Liste der VMware-Produkte, die über das {{site.data.keyword.slportal}} bestellt werden können. Preisinformationen finden Sie unter [IBM Cloud for VMware Solutions](http://www.softlayer.com/vmware-solutions).

|Produktname|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard Tier 1 (0 - 20 TB)|
|Virtual SAN Standard Tier 2 (21 - 64 TB)|
|Virtual SAN Standard Tier 3 (65 - 124 TB)|
|VMware Site Recovery Manager (SRM)|
{: caption="Tabelle 1. Im Kundenportal verfügbare VMware-Produkte" caption-side="top"}

Führen Sie die folgenden Schritte aus, um Lizenzen für die VMware-Produkte zu bestellen, die in Tabelle 1 aufgelistet sind:
1. Melden Sie sich beim [{{site.data.keyword.slportal_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} an.
2. Klicken Sie auf **Einheiten > Verwalten > VMware-Lizenzen**.
3. Klicken Sie in der rechten oberen Ecke auf **VMware-Lizenzen bestellen**.
4. Klicken Sie auf die Dropdown-Liste unter **Lizenz hinzufügen...**, um die VMware-Produkte und die Anzahl der CPUs für die Lizenzen aufzulisten, die Sie bestellen möchten.
  * **Hinweis:** VMware vSphere Enterprise Plus (ESXi 6.0) wird nicht über diesen Prozess bestellt. Es wird als angefordertes Betriebssystem bestellt, wenn Sie einen Bare-Metal-Server bestellen.
5. Der Preis für das VMware-Produkt, das Sie ausgewählt haben, wird rechts in der Anzeige angegeben.
6. Klicken Sie auf **Weiter**, um die Lizenzen zu bestellen, oder auf **Lizenz hinzufügen**, um weitere Lizenzen hinzuzufügen.
  * Nach dem Klicken auf **Weiter** wird wieder die Seite **VMware-Lizenzen** mit Ihren VMware-Produkten und Lizenzschlüsseln angezeigt.
7. Laden Sie die **Installationsdateien** über den bereitgestellten Link herunter. Für den Zugriff auf die Downloadseite benötigen Sie eine SSL-Verbindung zum privaten IBM Cloud-Netz.
8. Laden Sie die entsprechenden VMware-Produkte herunter und installieren Sie sie manuell in Ihrer vSphere-Umgebung.
