---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Speicher für die Verwendung mit VMware-Systemen
Für die Speicherung stehen Ihnen verschiedene Optionen zur Verfügung. Sie haben die Wahl zwischen privaten, gemeinsam genutzten und eigenen Speicherlösungen. Die folgenden Informationen erleichtern Ihnen die Entscheidung, welche Speicherlösung für Ihre Workload am besten geeignet ist.

Tabelle 1 enthält die Speichertiers und erleichtert die Zuordnung zu Ihrer Workload.
<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabelle 1. Speichertiers</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Tier 1</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Tier 2</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Tier 3</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Geschäftliche Nutzung</strong></p>
			</td>
			<td style="width:160px;">
				<p>Produktionsanwendungen, -datenbanken und -daten für hohe Leistung und/oder hohe Verfügbarkeit</p>
			</td>
			<td style="width:160px;">
				<p>Nicht geschäftskritische Anwendungen, Datenbanken und Daten für Test und Entwicklung</p>
			</td>
			<td style="width:160px;">
				<p>Nicht geschäftskritische Datenspeicherung, Sicherung und Archivierung</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Leistung</strong></p>
			</td>
			<td style="width:160px;">
				<p>Hoch (SSD, SAS)</p>
			</td>
			<td style="width:160px;">
				<p>Mittel (SAS, SATA)</p>
			</td>
			<td style="width:160px;">
				<p>Niedrig (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Garantierte E/A-Operationen pro Sekunde (IOPS)</strong></p>
			</td>
			<td style="width:160px;">
				<p>Ja</p>
			</td>
			<td style="width:160px;">
				<p>Nein</p>
			</td>
			<td style="width:160px;">
				<p>Nein</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Hochverfügbarkeit (High Availability, HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>Ja</p>
			</td>
			<td style="width:160px;">
				<p>Nein</p>
			</td>
			<td style="width:160px;">
				<p>Nein</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Replikation</strong></p>
			</td>
			<td style="width:160px;">
				<p>Ja</p>
			</td>
			<td style="width:160px;">
				<p>Ja</p>
			</td>
			<td style="width:160px;">
				<p>Nein</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Snapshots</strong></p>
			</td>
			<td style="width:160px;">
				<p>Ja</p>
			</td>
			<td style="width:160px;">
				<p>Nein</p>
			</td>
			<td style="width:160px;">
				<p>Nein</p>
			</td>
		</tr>
	</tbody>
</table>


## Optionen für privaten und gemeinsam genutzten VMware-Speicher

Sie können aus mehreren Speicheroptionen auswählen. Für den privaten Speicher können Sie lokale Plattenoptionen, VSAN oder QuantaStor auswählen. Für den gemeinsam genutzten Speicher können Sie Endurance- oder Performance-Speicher auswählen. Wenn Sie eigenen Speicher einbinden möchten, stehen mehrere 'private' Speicheroptionen zur Verfügung, darunter NetApp OnTap Edge, NetApp Private Storage (NPS), {{site.data.keyword.IBM}} Spectrum Accelerate und softwarebasierter Speicher. In Tabelle 2 und Tabelle 3 finden Sie einen übersichtlichen Parallelvergleich der Optionen.

## Optionen für privaten Speicher

In einer Single-Tenant-Umgebung sind mehrere Speicheroptionen zum Verbinden mit VMware verfügbar: 

* Lokaler Speicher
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## Lokaler Speicher

Bestellen Sie {{site.data.keyword.baremetal_short}} im IBM Cloud-Kundenportal mit ESX und wählen Sie die gewünschten Festplatten aus [SATA, seriell angeschlossene SCSI (SA SCSI) oder SSD].
 
Falls Sie eine eigene ESX-Lizenz bereitstellen möchten, müssen Sie ein Support-Ticket öffnen, um den Support über die Änderung zu informieren.

* Empfohlene Workloads: Tier 3
* Leistung: Begrenzt, abhängig von RAID und Plattentyp. SSDs kosten mehr und bieten eine bessere Leistung.
* Skalierbarkeit: Begrenzt durch die Anzahl der Laufwerkschächte im Gehäuse.
* Protokolle: Nicht zutreffend
* Kosten: Geringe Investitionskosten (CAPEX) und Betriebskosten (OPEX)
* Hochverfügbarkeit: Nicht verfügbar
* Replikation: [vSphere Replication Virtual Appliance ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Zuverlässigkeit: Mehrere einzelne Fehlerpunkte (Single Points of Failure)



## vSAN [1]

* Empfohlene Workloads: Tier 1
* Leistung: ab 90.000 E/A-Operationen pro Sekunde, je nach Hostkonfiguration
* Skalierbarkeit: VMDK (Virtual Machine Disk) v5.5 bis 2 TB, VMDK v6.0 bis 62 TB. Scale-out durch weitere Knoten.
* Protokolle: Proprietär
* Kosten: Mittlere Kosten für CAPEX und OPEX
* Hochverfügbarkeit: Unterstützt für Host- und Datenträgerfehler. Fehlerdomänen werden ab VMware v6 unterstützt.
* Replikation: [vSphere Replication Virtual Appliance ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Replikation und Disaster-Recovery:<!--
    1. VM-Backup über VMware vCenter Server terminieren
    2. VM-Snapshot erstellen
    3. Daten-DE für VM wird erstellt
    4. VM wiederherstellen-->
 * Zuverlässigkeit: Bis zu drei Hostfehler für sieben oder mehr Hosts werden unterstützt. Fehlerdomänen wurden in VMware v6 eingeführt.   

[1] vSan 6.2 - Die neue Funktion für standortübergreifende Cluster ermöglicht Hosts in verschiedenen Pods im selben Rechenzentrum (Validierungstests werden durchgeführt). <!-- Should this in progress mention be removed? -->

vSAN 5.5 - Nur verfügbar bei Bereitstellung einer eigenen Lizenz (Bring Your Own License, BYOL). Wird von VMware nur unterstützt, wenn Sie einen Plattencontroller 'Avago LSI MegaRAID SAS 9361-8i' verwenden.

vSAN 6.0 - Direkt verfügbar im IBM Cloud-Portal mit Abrechnung auf CPU-Lizenzbasis.

## QuantaStor

In der Veröffentlichung [OSNexus Solution Design Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} finden Sie hilfreiche Informationen zum Verbinden von VMware mit QuantaStor.

* Empfohlene Workloads: Tier 2 und 3 
* Leistung: Variabel je nach Laufwerkanzahl, RAID und Plattennutzung (iSCSI oder NFS)  
* Skalierbarkeit: v3-Einzelrahmen unterstützt 128 TB; kein Scale-up oder Scale-out. 
* Protokolle: iSCSI, NFS und SMB 
* Kosten: Hohe Kosten für CAPEX und OPEX 
* Hochverfügbarkeit: Nicht verfügbar  
* Replikation: Integrierte Replikationsfunktionen; SRA nicht verfügbar. vSphere Replication Appliance kann ebenfalls verwendet werden. 
* Zuverlässigkeit: Single Point of Failure für Gehäuse und RAID-Controller.


<a name="NetApp"></a>
## NetApp Data OnTap Edge

Sie müssen eine NetApp-Einheit von NetApp oder IBM erwerben. Diese Einheit muss auf einem {{site.data.keyword.baremetal_short}} in Ihrem {{site.data.keyword.BluSoftlayer}}-Rechenzentrum installiert werden.

Weitere Informationen zum Verbinden von VMware mit NetApp finden Sie über die folgenden Links:
* [NetApp ONTAP Select ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: Build a data center on a server with NetApp fundamentals ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* Empfohlene Workloads: Tier 2 und 3
* Leistung: Variabel je nach Laufwerkanzahl und RAID
* Skalierbarkeit: Unterstützt 110 TB; kein Scale-out.
* Protokolle: iSCSI, NFS und SMB
* Kosten: Mittlere Kosten für CAPEX und OPEX
* Hochverfügbarkeit: Nicht verfügbar
* Replikation: Unterstützt SnapMirror; wird auch mit [vRealize Automation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link") ](https://www.vmware.com/products/vrealize-automation){: new_window}(vRA) erreicht.
* Zuverlässigkeit: Single Point of Failure für Gehäuse und RAID-Controller.

<a name="NPS"></a>
## Privater NetApp-Speicher

Sie müssen eine NetApp-Einheit von NetApp oder IBM erwerben. Diese Einheit muss auf einer der Kollokations-Sites in der Nähe Ihres IBM Cloud-Rechenzentrums installiert und über Direct Link Colocation oder Direct Link Cloud verbunden werden.

Weitere Informationen zum Verbinden von VMware mit NetApp finden Sie über die folgenden Links: 
* [NetApp Private Storage for IBM Cloud ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Solution brief: NetApp Private Storage for IBM Cloud ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* Empfohlene Workloads: Tier 1
* Leistung: Vom NetApp-Modell abhängig
* Skalierbarkeit: Unterstützt das Hinzufügen von Laufwerken und Rahmen für erhöhte Kapazität und mehr E/A-Operationen pro Sekunde (IOPS)
* Protokolle: iSCSI, NFS und SMB
* Kosten: Hohe Kosten für CAPEX und OPEX
* Hochverfügbarkeit: Zwei Kopfsätze und Controller
* Replikation: Unterstützt SnapVault und SnapMirror; wird auch mit [vRealize Automation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.vmware.com/products/vrealize-automation) erreicht.
* Zuverlässigkeit: Hohe Redundanz und MPIO-Unterstützung

<a name="IBM"></a>
## IBM Spectrum Accelerate

Die Option 'IBM Spectrum Accelerate' für privaten Speicher ist im IBM Cloud-Kundenportal nicht verfügbar. <!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* Empfohlene Workloads: Tier 1
* Leistung: Abhängig von der Anzahl der Platten, vom Solid-State-Laufwerk (optional) und von der Speicherkapazität, die für jede Knoten-VM angegeben ist.
* Skalierbarkeit: Skalierung von 8 bis 325 TB (verwendbar)
  * Mindestkapazität: 3 VMs x 6 Laufwerke
  * Höchstkapazität: 15 VMs x 12 Laufwerke
  * Skalierung bis 144 virtuelle Arrays und über 40 PB (verwendbar) durch IBM Hyper-Scale Manager
  * Unterbrechungsfreie Kapazitätserweiterung durch Hinzufügen weiterer Knoten
  * 1 x 500 oder 800 GB SSD je Knoten wird unterstützt
* Protokolle: nur iSCSI
* Kosten: Abhängig vom Preismodell und von den physischen Maschinen, die für Knoten implementiert sind. Hohe Kosten für CAPEX; mittlere bis niedrige Kosten für OPEX je nach Lizenzierung.
  * Abrechnung pro Binärdatei (TiB) der verwendbaren Kapazität
  * Nicht an eine bestimmte Hardwarekonfiguration gebunden. Beispiel: Eine Lizenz für 200 TiB kann als eine Instanz mit 200 TiB, als zwei Instanzen mit jeweils 100 TiB oder als vier Instanzen mit jeweils 50 TiB implementiert werden.
  * Zwei Varianten werden angeboten: zeitlich unbegrenzte Lizenz [einschließlich ein Jahr Subskription und Service (S&S)] und monatliche Lizenz (einschließlich S&S)
* Hochverfügbarkeit: Clusterlösung
* Replikation: Wird mithilfe von [vRealize Automation![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link") ](https://www.vmware.com/products/vrealize-automation){: new_window} (SRA) erreicht, das zum Replizieren der physischen IBM XIV-Instanz mit VMware Site Recovery Manager (SRM) verwendet werden kann.
  * [vSphere Replication ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [VMware vCenter Site Recovery Manager version 5.x guidelines for IBM XIV Gen3 Storage System ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* Zuverlässigkeit: Hohe Redundanz und MPIO-Unterstützung. Jeder verfügbare Knoten kann den Cluster verwalten. Die folgenden Funktionen werden von IBM Spectrum Accelerate gegenwärtig nicht über hardwarebasierte IBM XIV-Systeme unterstützt:
  * Spiegelung auf drei Standorte
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG v6
  * Plattenlaufwerke mit 6 TB
  * Storage Management Initiative Specifications (SMI-S) 1.6
  * Verschlüsselung ruhender Daten
  * Die Lizenzierung von vStorage for API Array Integration (VAAI) ist jetzt in Verbindung mit virtuellen Datenträgern (Virtual Volumes, VVol) verfügbar
  * vCenter Operations Manager (VCop)
  * Weitere Informationen zu IBM XIV Storage System finden Sie in [Platform and application integration for IBM XIV Storage System ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}

## Optionen für gemeinsam genutzten Speicher

Zwei Speicheroptionen können zum Verbinden mit VMware in einer Multi-Tenant-Umgebung verwendet werden: Blockspeicher und Dateispeicher.

### Blockspeicher und Dateispeicher

Bestellen Sie {{site.data.keyword.baremetal_short}} im IBM Cloud-Kundenportal mit ESX.

In VMware werden drei vordefinierte <!--**Authorize** (**Block** or **File**) **Storage SoftLayer** -->-Werte auf der Registerkarte **Speicher für Hostgerätedetails** bereitgestellt: Benutzername, Kennwort (für CHAP-Authentifizierung) und Host-IQN.

Weitere Informationen zum Bereitstellen von Blockspeicher finden Sie in [Blockspeicher bereitstellen und verwalten](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Weitere Informationen zum Bereitstellen von Dateispeicher finden Sie in [IBM File Storage für IBM Cloud bereitstellen und verwalten](/docs/infrastructure/FileStorage/provisioning-file-storage.html).

* Empfohlene Workloads: Tier 1, 2 und 3
* Zwei Methoden für die Leistungsbereitstellung:
    1. IOPS für Endurance-Tiers: 0,25, 2, 4 oder 104 IOPS pro GB verfügbar
    2. Leistung für zugeordnete IOPS: IOPS unabhängig von Kapazität angeben. Empfohlen für Workloads mit klar definierten Leistungsanforderungen.
    * Parameter für prognostizierbare Speicherleistung
    * Mehrere Datenträger können einheitenübergreifend zusammengefasst werden, um mehr IOPS und einen höheren Durchsatz zu erzielen
* Latenz < 10 ms UP bis 48.000 IOPS
* Skalierbarkeit: 20 GB bis 12 TB bestellbar. Das Volumen kann nach der Bestellung nicht mehr geändert werden.
* Protokolle: iSCSI und NFS
* Kosten: Hohe Kosten für CAPEX (zehnmal soviel wie für ein SAN gleicher Größe) und OPEX
* Hochverfügbarkeit: Zwei Kopfsätze und Controller
* Replikation: Snapshot und Replikation werden über das IBM Cloud Private Network bereitgestellt; wird auch mit [vRealize Automation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link") ](https://www.vmware.com/products/vrealize-automation){: new_window} erreicht, jedoch ohne SRA.
* Zuverlässigkeit: Hohe Redundanz; iSCSI verwendet eine MPIO-Verbindung; NFS-basierter Speicher wird über TCP/IP-Verbindungen weitergeleitet. Snapshot und Replikation aktiviert.

Tabelle 2 listet die Vor-und Nachteile für privaten Speicher in einer Single-Tenant-Umgebung auf.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabelle 2. Vor- und Nachteile der Optionen für privaten VMware-Speicher</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; Privater Speicher (Single Tenant)</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>Schlüsselfaktoren/Speicheroption</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>Lokal</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>Virtuelles SAN</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:99px;">
				<p>QuantaStor</p>
			</td>
			<td bgcolor="#C6D9F1" colspan="2" style="width:159px;">
				<p align="center">NetApp</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p>IBM Spectrum Accelerate</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>OnTap Edge</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>NPS</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p align="center">&nbsp;</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Typ</strong></p>
			</td>
			<td style="width:87px;">
				<p>Lokal</p>
			</td>
			<td style="width:95px;">
				<p>SDS</p>
			</td>
			<td style="width:99px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>Monolithisch</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Leistung</strong></p>
			</td>
			<td style="width:87px;">
				<p>Basiert auf SSD/SA-SCSI-Spezifikationen; zusätzlicher RAID 5/10 kann für mehr Lese-/Schreibleistung verwendet werden.</p>
			</td>
			<td style="width:95px;">
				<p>Ab 90.000 IOPS pro Host, je nach Hostkonfiguration. 100 VMs pro Host, 32 Hosts pro Cluster, 3.200 VMs pro Cluster, nur 2.048 geschützt (v5.5).</p>
				<p>Bis 20.000 IOPS, 200 VMs pro Host, 64 Hosts pro Cluster und 6.000 geschützte VMs pro Cluster (v6.0).</p>
			</td>
			<td style="width:99px;">
				<p>Basiert auf Typ und Anzahl der ausgewählten Platten sowie auf den RAID-Konfigurationen und auf der Verwendung von iSCSI oder NFS.</p>
			</td>
			<td style="width:80px;">
				<p>Basiert auf Typ und Anzahl der ausgewählten Platten sowie auf den RAID-Konfigurationsaktionen.</p>
			</td>
			<td style="width:80px;">
				<p>Hängt vom Modell ab.</p>
			</td>
			<td style="width:96px;">
				<p>Basiert auf Typ und Anzahl der ausgewählten Platten sowie auf den RAID-Konfigurationen und auf der optionalen SSD-Plattennutzung pro Hypervisorknoten.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Skalierbarkeit</strong></p>
			</td>
			<td style="width:87px;">
				<p>Begrenzte Zunahme der Größe und des Platten-E/A-Durchsatzes.</p>
			</td>
			<td style="width:95px;">
				<p>Platte der virtuellen Maschine (Virtual Nachine Disk, VMDK) bis zu 2 TB unter v5.5 und bis zu 62 TB unter v6.0.</p>
				<p>Scale-out durch weitere Knoten.</p>
			</td>
			<td style="width:99px;">
				<p>Single QS bis zu 128 TB (3,x). Kein Scale-up oder Scale-out.</p>
			</td>
			<td style="width:80px;">
				<p>Bis zu 10 TB; kein Scale-out.</p>
			</td>
			<td style="width:80px;">
				<p>Ja, durch zusätzliche Baugruppenrahmen für Kapazität und IOPS.</p>
			</td>
			<td style="width:96px;">
				<p>Skalierung von 8 bis 325 TB Speicherplatz (nutzbar).</p>
				<p>Mindestkapazität: 3 VMs x 6 Laufwerke.</p>
				<p>Höchstkapazität: 15 VMs x 12 Laufwerke.</p>
				<p>Skalierung bis 144 virtuelle Arrays und über 40 PB (verwendbar) durch IBM Hyper-Scale Manager.</p>
				<p>Erweiterung der unterbrechungsfreien Kapazität durch Hinzufügen weiterer Knoten.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protokolle</strong></p>
			</td>
			<td style="width:87px;">
				<p>Nicht zutreffend</p>
			</td>
			<td style="width:95px;">
				<p>Proprietär</p>
			</td>
			<td style="width:99px;">
				<p>iSCSI/NFS/SMB</p>
			</td>
			<td colspan="2" style="width:159px;">
				<p align="center">iSCSI/NFS/SMB</p>
			</td>
			<td style="width:96px;">
				<p>iSCSI</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Anwendungsfälle</strong></p>
			</td>
			<td style="width:87px;">
				<p>Workloads in Tier 2 und 3</p>
			</td>
			<td style="width:95px;">
				<p>Workloads in Tier 1</p>
			</td>
			<td style="width:99px;">
				<p>Workloads in Tier 2 und 3</p>
			</td>
			<td style="width:80px;">
				<p>Workloads in Tier 2 und 3</p>
			</td>
			<td style="width:80px;">
				<p>Workloads in Tier 1</p>
			</td>
			<td style="width:96px;">
				<p>Workloads in Tier 1</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Hochverfügbarkeit (High Availability, HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>Verfügbar mit RAID</p>
			</td>
			<td style="width:95px;">
				<p>Ja; Host- und Datenträgerfehler; Fehlerdomänen (v6.0)</p>
			</td>
			<td style="width:99px;">
				<p>In IBM Cloud nicht verfügbar.</p>
			</td>
			<td style="width:80px;">
				<p>Nicht zutreffend</p>
			</td>
			<td style="width:80px;">
				<p>Ja; zwei Kopfsätze und Controller.</p>
			</td>
			<td style="width:96px;">
				<p>Ja; Clusterlösung.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Konfigurierbarkeit</strong></p>
			</td>
			<td style="width:87px;">
				<p>Anzahl und Typ der Platten; RAID-Stufen</p>
			</td>
			<td style="width:95px;">
				<p>Bestimmte Controller erforderlich.</p>
			</td>
			<td style="width:99px;">
				<p>CPU, Hauptspeicher, Cache, Anzahl und Typ der Platten sowie RAID-Stufen.</p>
			</td>
			<td style="width:80px;">
				<p>CPU, Hauptspeicher, Cache, Anzahl und Typ der Platten sowie RAID-Stufen.</p>
			</td>
			<td style="width:80px;">
				<p>Wird noch festgelegt</p>
			</td>
			<td style="width:96px;">
				<p>CPU, Hauptspeicher, Cache, Anzahl und Typ der Platten, SSD, Caching, iSCSI-Portkonfiguration. Multi-Tanant-Servicequalitätsstufe.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Disaster-Recovery und Replikation</strong></p>
			</td>
			<td style="width:87px;">
				<p>Verwenden Sie vRA zum Replizieren; keine SRAs.</p>
			</td>
			<td style="width:95px;">
				<p>Verwenden Sie vRA zum Replizieren.</p>
			</td>
			<td style="width:99px;">
				<p>Integrierte Replikation; keine SRAs verfügbar.</p>
			</td>
			<td style="width:80px;">
				<p>Kann vRA zum Replizieren verwenden; SnapMirror.</p>
			</td>
			<td style="width:80px;">
				<p>Kann vRA zum Replizieren verwenden; SnapMirror, SnapVault.</p>
			</td>
			<td style="width:96px;">
				<p>vRA oder SRA wird unterstützt; Replikation zwischen SDS und/oder physischen XIV-Geräten.</p>
				<p>Snapshots werden unterstützt; Anwendungswiederherstellung durch IBM FlashCopy Manager.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Zuverlässigkeit</strong></p>
			</td>
			<td style="width:87px;">
				<p>Single Point of Failure ohne Hochverfügbarkeit (High Availabilität, HA).</p>
			</td>
			<td style="width:95px;">
				<p>Bis zu drei Hostfehler für sieben oder mehr Hosts werden toleriert.</p>
				<p>Fehlerdomänen wurden in v6.0 eingeführt.</p>
			</td>
			<td style="width:99px;">
				<p>Single Point of Failure (Gehäuse und RAID-Controller) und keine HA.</p>
			</td>
			<td style="width:80px;">
				<p>Single Point of Failure (Gehäuse und RAID-Controller) und keine HA.</p>
			</td>
			<td style="width:80px;">
				<p>Multipath I/O-Verbindung (MPIO-Verbindung) mit hoher Redundanz.</p>
			</td>
			<td style="width:96px;">
				<p>iSCSI-MPIO-Verbindungen mit hoher Redundanz: Jeder Knoten kann den Cluster verwalten.</p>
			</td>
		</tr>
	</tbody>
</table>

Tabelle 2 - Dokumentationslinks:
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge: Im Kundenportal nicht verfügbar – eigene Lösung bereitstellen.
  * [Data ONTAP Installation and Administration Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP Express Setup Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate: Im Kundenportal nicht verfügbar – eigene Lösung bereitstellen.
  * [Working with an IBM Spectrum Accelerate system ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

Tabelle 3 listet die Vor- und Nachteile für gemeinsam genutzten Speicher in einer Multi-Tenant-Umgebung auf.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tabelle 3. Vor- und Nachteile der Optionen für gemeinsam genutzten VMware-Speicher</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>Gemeinsam genutzter VMware-Speicher (Multi-Tenant)</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Schlüsselfaktoren/Speicheroptionen</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">Endurance - Block- und Dateispeicher</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">Leistung - Block- und Dateispeicher</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Typ</strong></p>
			</td>
			<td style="width:266px;">
				<p>SDS</p>
			</td>
			<td style="width:271px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Leistung</strong></p>
			</td>
			<td style="width:266px;">
				<p>0,25, 2, 4 oder 104 IOPS pro GB verfügbar</p>
				<p>Parameter für prognostizierbare Speicherleistung.</p>
				<p>Mehrere Datenträger können einheitenübergreifend zusammengefasst werden, um mehr IOPS und einen höheren Durchsatz zu erzielen.</p>
			</td>
			<td style="width:271px;">
				<p>Der Client stellt je nach Workloadbedarf oder Preispunkt die gewünschte Leistungsstufe bereit.</p>
				<p>&nbsp;</p>
				<p>Parameter für prognostizierbare Speicherleistung.</p>
				<p>Mehrere Datenträger können einheitenübergreifend zusammengefasst werden, um mehr IOPS und einen höheren Durchsatz zu erzielen.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Skalierbarkeit</strong></p>
			</td>
			<td style="width:266px;">
				<p>Datenträgergrößen von 20 GB bis 12 TB. Die Größe kann nach der Bestellung nicht mehr geändert werden.</p>
			</td>
			<td style="width:271px;">
				<p>Datenträgergrößen von 20 GB bis 12 TB. Die Größe kann nach der Bestellung nicht mehr geändert werden.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protokolle</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI und NFS</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI und NFS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Hostverbindungen</strong></p>
			</td>
			<td style="width:266px;">
				<p>Maximal 8 für iSCSI und 64 für NFS.</p>
			</td>
			<td style="width:271px;">
				<p>Maximal 8 für iSCSI und 64 für NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Anwendungsfälle</strong></p>
			</td>
			<td style="width:266px;">
				<p>Workloads in Tier 1, 2 und 3:</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 0,25 IOPS pro GB: Geringes Ein-/Ausgabevolumen. Anwendungsbeispiele: Mailboxspeicherung und Dateifreigaben für Unternehmensbereiche.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 2 IOPS pro GB: Allgemeine Zwecke. Anwendungsbeispiele: Hosting kleiner Datenbanken als Datenbasis für Webanwendungen oder Plattenimages von virtuellen Maschinen für einen Hypervisor.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 4 IOPS pro GB: Hohes Ein-/Ausgabevolumen. Anwendungsbeispiele: Transaktionsorientierte oder andere leistungskritische Datenbanken.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 10 IOPS pro GB: Hohes Ein-/Ausgabevolumen. Anwendungsbeispiele: Analyseanwendungen.</p>
			</td>
			<td style="width:271px;">
				<p>Workloads in Tier 1, 2 und 3:</p>
				<p>iSCSI-basierte MPIO-Speicherung; besonders geeignet für Anwendungen mit hohem Ein-/Ausgabevolumen (z. B. relationale Datenbanken, die ein vorhersehbares Leistungsverhalten erfordern). Die Größe der Speicherdatenträger reicht von 20 GB bis 12 TB mit benutzerdefiniertem IOPS-Volumen von 100 bis 48.000 IOPS (E/A-Operationen pro Sekunde).</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Hochverfügbarkeit</strong></p>
			</td>
			<td style="width:266px;">
				<p>Ja, zwei Kopfsätze und Controller.</p>
			</td>
			<td style="width:271px;">
				<p>Ja, zwei Kopfsätze und Controller.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Konfigurierbarkeit</strong></p>
			</td>
			<td style="width:266px;">
				<p>Nur Größe und IOPS.</p>
			</td>
			<td style="width:271px;">
				<p>Nur Größe und IOPS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Disaster-Recovery und Replikation</strong></p>
			</td>
			<td style="width:266px;">
				<p>Snapshot und Replikation werden über das IBM Cloud Private Network bereitgestellt. vRA kann zum Replizieren auf VM-Ebene verwendet werden; kein SRA.</p>
			</td>
			<td style="width:271px;">
				<p>Snapshot und Replikation werden über das IBM Cloud Private Network bereitgestellt. vRA kann zum Replizieren auf VM-Ebene verwendet werden; kein SRA.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Zuverlässigkeit</strong></p>
			</td>
			<td style="width:266px;">
				<p>Hohe Redundanz, MPIO-Verbindung, NFS-basierte Dateispeicherung und Weiterleitung über Dateispeicher für TCP/IP-Verbindungen. Snapshots und Replikation aktiviert.</p>
			</td>
			<td style="width:271px;">
				<p>Hohe Redundanz, MPIO-Verbindung, NFS-basierte Dateispeicherung und Weiterleitung über Dateispeicher für TCP/IP-Verbindungen. </p>
			</td>
		</tr>
	</tbody>
</table>

Tabelle 3 - Dokumentationslinks:
* [Blockspeicher](/docs/infrastructure/BlockStorage/index.html)
* [Dateispeicher](/docs/infrastructure/FileStorage/index.html)
