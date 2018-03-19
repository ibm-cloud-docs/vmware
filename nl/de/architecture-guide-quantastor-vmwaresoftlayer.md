---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Architekturleitfaden für QuantaStor

Sie können die gemeinsam genutzte OSNexus QuantaStor-Speicherlösung für eine VMware ESXi 5-Umgebung bestellen und konfigurieren. Verwenden Sie die folgenden Informationen zusammen mit dem Cookbook [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html), um eine dieser Speicheroptionen in Ihrer VMware-Umgebung einzurichten.

## Schritt 1: Gemeinsam genutzten QuantaStor-Speicher bestellen

Bevor Sie eine Bestellung für den Speicher einreichen, müssen Sie die Spezifikationen ermitteln, die Ihre Anforderungen an die Kapazität und die Ein-/Ausgabe erfüllen. Zu diesen Spezifikationen gehören unter anderem Server-RAM, Typ und Anzahl der Plattenlaufwerke, SSDs für Caching, RAID-Konfiguration und Netzkonfiguration. Weitere Informationen zum Auswählen der geeigneten QuantaStor-Konfiguration in Ihrer Umgebung finden Sie in [QuantaStor Solution Design Guide for Virtualization ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide#Server_Virtualization){: new_window}.

Für die Beispielumgebung wird eine kleinere Konfiguration verwendet, die genügend Kapazität und Ein-/Ausgabe für die virtuellen Maschinen (VMs) bereitstellen kann. Sie sollten die Anforderungen an die Kapazität und die Ein-/Ausgabe Ihrer VMs kennen, bevor Sie eine Bestellung einreichen. Obwohl der QuantaStor-Server erweiterbar ist, sollten Sie die Anfangsgröße Ihrer Hardware so wählen, dass Verzögerungen bei der Konfiguration und Implementierung vermieden werden. 

### QuantaStor bestellen

Führen Sie die folgenden Schritte aus, um einen QuantaStor-Server zu bestellen.

1. Melden Sie sich bei [{{site.data.keyword.slportal_full}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} an und klicken Sie auf **Konto > Bestellung einreichen**.
2. Wählen Sie im Dialogfenster '{{site.data.keyword.baremetal_short}}, Monatlich' aus.
3. Wählen Sie den geeigneten Server mit der Speicherkapazität für die Anzahl der Datenträger, die für Ihre Umgebung benötigt werden, auf der Seite 'Serverliste' aus. [Für die Beispielumgebung wird ein System mit 12 Kernen (zweimal sechs Kerne) und 12 Laufwerkpositionen ausgewählt.]
4. Geben Sie die folgenden Konfigurationsoptionen ein:
  * **Rechenzentrum:** Die Position der zuvor erstellten VLANs und ESXi-Hosts.
  * **Server:** Xeon Dualprozessor mit sechs Kernen
  * **Arbeitsspeicher:** 64 GB
  * **Betriebssystem:** OSNexus QuantaStor 3.x (4 TB)
  * **Festplattenlaufwerke:**
    * Platte 1 & 2: 500 GB SATA in RAID 1
    * Partitionsvorlage: Linux Basic
    * Platte 3 - 10: 600 GB SAS 15K in RAID 10
  * **Öffentliche Bandbreite:** Nur privates Netz
  * **Uplink-Port-Geschwindigkeiten:** Redundante Uplinks mit 10 Gb/s für privates Netz
5. Klicken Sie auf **Bestellung fortsetzen**.

**Hinweis:** Der Speicherserver ist mit zwei nicht gebundenen Netzschnittstellen konfiguriert, d. h. der Datenverkehr für den Speicherarray kann auf zwei verschiedene Teilnetze verteilt werden.

### Konfiguration abschließen

Ihr Warenkorb enthält jetzt eine QuantaStor-Appliance. Als nächstes müssen Sie das private VLAN, den Hostnamen und die Domäne für das Gerät zuordnen, damit es ordnungsgemäß bereitgestellt werden kann.

1. Ordnen Sie die folgenden VLANs zu und erstellen Sie Hostnamen für die Geräte: QuantaStor-Host - Back-End-VLAN: (1102 in der Umgebung)
2. Wählen Sie die Zahlungsmethode aus, stimmen Sie den Geschäftsbedingungen zu und klicken Sie auf 'Bestellung abschließen'.

**Hinweis:** Fahren Sie erst mit Schritt 3 fort, nachdem der Server bereitgestellt und über VPN oder den virtuellen Server erreichbar ist.

## Schritt 2: iSCSI Software Adapter für Management- und Kapazitätshosts aktivieren

Vor dem Anhängen von iSCSI-Datenträgern muss iSCSI Software Adapter auf jedem Management- und Kapazitätshost aktiviert und der zugehörige qualifizierte iSCSI-Name (IQN) erfasst werden. Führen Sie die folgenden Schritte aus, um iSCSI Software Adapter zu aktivieren:

1. Wechseln Sie zu einem ESXi-Management- oder -Kapazitätshost und wählen Sie 'Verwalten > Speicher > Speicheradapter' aus.
2. Klicken Sie auf das grüne Pluszeichen (+) und fügen Sie die iSCSI Software Adapter-Instanz hinzu.
3. Klicken Sie auf die vmhba-Instanz, die der iSCSI Software Adapter-Instanz entspricht, und zeichnen Sie nach dem Aktivieren den zugehörigen iSCSI-Namen (Abbildung 1) im Abschnitt für Adapterdetails auf.
4. Führen Sie die Schritte 1 bis 3 für jede iSCSI Software Adapter-Instanz auf jedem ESXi-Management- und -Kapazitätshost aus.

## Schritt 3: QuantaStor konfigurieren

Nachdem der Server bereitgestellt wurde, können Sie die gemeinsam genutzte Speichereinheit einrichten. Dabei richten Sie insbesondere den Netzbetrieb ein, konfigurieren iSCSI-Datenträger und ordnen Datenträger den Hosts zu. 

Beispiel: Der Datenträger 'vmk3' verfügt über 'vmnic0', die eine Verbindung zum portierbaren privaten Teilnetz A im Speicher-VLAN herstellt. Der Datenträger 'vmk4' verfügt über 'vmnic2', die eine Verbindung zum portierbaren privaten Teilnetz B im Speicher-VLAN herstellt. Der QuantaStor-Server verfügt außerdem über die beiden privaten Netzadapter eth4 und eth6, die Verbindungen zum Speicher-VLAN herstellen.

### Networking konfigurieren

1. Öffnen Sie einen Web-Browser und rufen Sie die QuantaStor-IP-Adresse auf, die auf der Seite **Geräte** in [{{site.data.keyword.slportal_short}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} aufgelistet ist.
2. Geben Sie **Administratorbenutzername** und **Kennwort** (aus dem Abschnitt 'Kennwörter' auf der Seite **Gerätedetails**) ein. Notieren Sie vor dem Fortfahren die vom QuantaStor-Server verwendeten privaten Netzeinheiten (z. B. eth4).
3. Navigieren Sie zu **Speichersystem > Netzports**.
4. Wählen Sie in der Liste der Netzadapter den aktiven privaten Adapter aus (z. B. eth4). Klicken Sie mit der rechten Maustaste und wählen Sie im Popup-Menü die Option **Netzport ändern** aus.
5. Wählen Sie das Kontrollkästchen **iSCSI aktiviert ** ab, um iSCSI-Verbindungen zu diesem Adapter zu inaktivieren, und klicken Sie auf **OK**.
6. Wählen Sie den nicht aktiven privaten Adapter aus, der dem privaten Netz zugeordnet ist (z. B. eth6).
7. Klicken Sie mit der rechten Maustaste auf den Adapter 'eth6' und wählen Sie im Popup-Menü die Option **Netzport ändern** aus.
8. Wählen Sie in der Anzeige **Netzport ändern** unter **Konfigurationstyp** die Option **Statisch** aus.
9. Geben Sie eine primäre private IP-Adresse, ein Teilnetz und ein Gateway für den Adapter ein. Verwenden Sie eine Adresse aus der Zeile 'Speicher', wenn Sie das VLAN-Arbeitsblatt aus dem Cookbook [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) verwenden.
10. Wählen Sie das Kontrollkästchen **iSCSI aktiviert** ab, um iSCSI-Verbindungen zu diesem Adapter zu inaktivieren.
11. Klicken Sie mit der rechten Maustaste auf den privaten Adapter, und wählen Sie **Netzport aktivieren** aus, um den Adapter online zu schalten, nachdem er mit einer IP-Adresse konfiguriert wurde.
12. Klicken Sie auf **OK**, um den Port nach dem Überprüfen der IP-Adresse zu aktivieren.

### Suppor-Ticket öffnen

Sie müssen ein Support-Ticket öffnen, nachdem Sie einen zweiten Adapter mit einer primären privaten IP-Adresse konfiguriert haben. Durch das Öffnen des Tickets wird sichergestellt, dass die von Ihnen verwendete IP-Adresse nicht zum Bereitstellen einer anderen Maschine im VLAN verwendet wird.

1. Klicken Sie auf **Support** > **Ticket hinzufügen** und geben Sie die folgenden Informationen ein:
  * Betreff: Frage zu privatem Netz
  * Titel: Private IP-Adresse reservieren und zuordnen
  * Geräte zuordnen: 'QuantaStor-Server auswählen'
  * Details: Im VLAN reservieren und zuordnen. Diese IP-Adresse wird für den zweiten Adapter auf dem QuantaStor-Server verwendet.

### QuantaStor konfigurieren

Da der Array nun Verbindungen von beiden Adaptern akzeptieren kann, müssen die virtuellen Schnittstellen des Adapters in den Teilnetzen 'Speicherpfad A' und 'Speicherpfad B' zugeordnet werden.

  1. Klicken Sie mit der rechten Maustaste auf die anfängliche private Adapterschnittstelle (eth4) und wählen Sie im Popup-Menü die Option **Virtuelle Schnittstelle erstellen** aus.
  2. Geben Sie eine portierbare private IP-Adresse und ein Teilnetz für den Adapter in dem angezeigten Dialogfenster ein und stellen Sie sicher, dass **iSCSI aktiviert** ausgewählt ist.
  3. Verwenden Sie eine Adresse aus der Zeile 'Speicherpfad A', wenn Sie das VLAN-Arbeitsblatt verwenden.
  4. Notieren Sie die IP-Adresse, die im Abschnitt 'Hinweise' auf der Seite für die portierbare IP-Adresse verwendet wird.
  5. Wählen Sie die anfängliche private Adapterschnittstelle (eth4) aus, um die virtuelle Schnittstelle zu binden, und klicken Sie auf **OK**.
  6. Klicken Sie mit der rechten Maustaste auf die andere private Adapterschnittstelle (eth6) und wählen Sie im Popup-Menü **Virtuelle Schnittstelle erstellen** aus.
  7. Geben Sie eine portierbare private IP-Adresse und ein Teilnetz für den Adapter ein und stellen Sie sicher, dass in dem angezeigten Dialogfenster die Option **iSCSI aktiviert** aktiviert ist.
  8. Verwenden Sie eine Adresse aus der Zeile 'Speicherpfad B', wenn Sie das VLAN-Arbeitsblatt verwenden.
  9. Notieren Sie die IP-Adresse, die im Abschnitt 'Hinweise' auf der Seite für die portierbare IP-Adresse verwendet wird.
  10. Wählen Sie die andere private Adapterschnittstelle (eth6) aus, um die virtuelle Schnittstelle zu binden, und klicken Sie auf **OK**.

Nach dem Konfigurieren des QuantaStor-Servers mit IP-Adressen und virtuellen Schnittstellen müssen Sie das Routing konfigurieren, um sicherzustellen, dass der ausgehende Datenverkehr die richtige Schnittstelle verwendet (da zwei NICs in verschiedenen Teilnetzen vorhanden sind).

1. Melden Sie sich über SSH mit Ihren Rootberechtigungsnachweisen bei Ihrem QuantaStor-Server an und fügen Sie die folgenden Zeilen an /etc/network/interfaces an. Dabei wird vorausgesetzt, dass 'eth4' und 'eth6' die NICs im privaten Netz sind:
  * post-up ip route add 10.0.0.0/8 via dev eth4
  * post-up ip route add 10.0.0.0/8 via dev eth6 table eth6
  * post-up ip rule add from table eth6

### Speicherpool erstellen

Als Nächstes müssen Sie einen Speicherpool erstellen, der verwendet wird, um Datenträger zuzuordnen, bevor Sie Datenträger oder Freigaben erstellen können.

1. Klicken Sie mit der rechten Maustaste auf **Speicherpools** und wählen Sie **Speicherpool erstellen** aus.
2. Geben Sie in der Anzeige **Speicherpool erstellen** die folgenden Informationen ein:
  * Name: Geben Sie den entsprechenden Namen für den Speicherpool ein. Beispiel: Speicherpool-01
  * Pooltyp: Standard (zfs)
  * E/A-Profil: Virtualisierung
  * Für Speicherpool verwendete Platte(n): sdb
3. Klicken Sie auf **OK**.

Wenn die Platte 'sdb' nicht zu einem Pool hinzugefügt werden kann, ist eine Partition vorhanden, die als bootfähig gekennzeichnet ist. In diesem Fall müssen Sie 'gdisk' in der QuantaStor-Konsole verwenden, um die Partition und alle Einträge '/etc/fstab' zu entfernen. Als Nächstes müssen Sie Datenträger erstellen, die von ESXi verarbeitet werden können.

### iSCSI-Speicherdatenträger erstellen

Sie müssen zwei Speicherdatenträger erstellen. Ein Datenträger wird für Management-VMs im Management-Cluster verwendet und der andere für VMs im Kapazitätscluster. Führen Sie die folgenden Schritte aus, um die iSCSI-Speicherdatenträger zu erstellen:

1. Klicken Sie mit der rechten Maustaste auf **Speicherdatenträger** und wählen Sie im Popup-Menü **Speicherdatenträger erstellen** aus.
2. Geben Sie die Informationen für die Speicherdatenträger ein. **Hinweis:** Das Beispiel zeigt in Tabelle 1 und Tabelle 2 die Werte für jeden Speicherdatenträger an. Ihre Konfiguration kann je nach Auslastung und Speicherkapazität von den Beispielwerten abweichen.

|Feld|Wert|
|---|---|
|Name|Mgmt-LUN0|
|Speicherpool|[Im vorherigen Schritt konfigurierter Speicherpoolname]|
|Größe|500 GB|
|% reserviert|50|
|Komprimierung|Aktiviert|
{: caption="Tabelle 1. Datenträger für iSCSI-Management" caption-side="top"}

|Feld|Wert|
|---|---|
|Name|Capacity-LUN0|
|Speicherpool|[Im vorherigen Schritt konfigurierter Speicherpoolname]|
|Größe|3 TB|
|% reserviert|50|
|Komprimierung|Aktiviert|
{: caption="Tabelle 2. Datenträger für iSCSI-Kapazität" caption-side="top"}

### Hostzugriff auf Datenträger zuordnen

Sie müssen QuantaStor so konfigurieren, dass der Zugriff von den ESXi-Hosts über die einzelnen Host-IQN möglich ist, nachdem die Datenträger eingerichtet wurden.

1. Navigieren Sie zur QuantaStor-Verwaltungsseite, klicken Sie mit der rechten Maustaste auf das Menü **Hosts** und wählen Sie **Host hinzufügen** aus.
2. Geben Sie in der Anzeige **Host hinzufügen** die folgenden Informationen ein:
  * Hostname: Geben Sie einen geeigneten Hostnamen ein. Der Hostname enthält nicht den vollständig qualifizierten Domänennamen (FQDN), aber er sollte den Host beschreiben. Beispiel: MeinESXiHostName.
  * Betriebssystemtyp: VMware
  * Initiator: Optionsfeld 'Qualifizierter iSCSI-Name (IQN)'
  * Qualifizierter iSCSI-Name: Der IQN für den jeweiligen Host.
3. Klicken Sie auf **OK**.

Führen Sie die folgenden Schritte für jeden Management- und Kapazitätshost in der ESXi-Umgebung aus.

Gehen Sie nach dem Hinzufügen der einzelnen Hosts in den Management- und Kapazitätsclustern wie folgt vor:

1. Klicken Sie mit der rechten Maustaste auf das Menü **Hostgruppen** und wählen Sie **Hostgruppe erstellen ...** aus.
2. Geben Sie 'ManagementCluster' in das Feld **Name** ein und wählen Sie alle Hosts im Managementcluster aus.
3. Klicken Sie auf **OK**. Es wird eine Hostgruppe erstellt, die einem bestimmten Datenträger zugeordnet werden kann.

Wiederholen Sie diesen Prozess für den Kapazitätscluster.

1. Klicken Sie auf das Menü **Speicherdatenträger**.
2. Klicken Sie mit der rechten Maustaste auf den Datenträger **Mgmt-Lun0** und wählen Sie **Hostzugriff zuordnen/aufheben** aus.
3. Stellen Sie sicher, dass **Mgmt-Lun0** als Option im Dropdown-Menü angezeigt wird, und wählen Sie die Hostgruppe aus, die Sie im vorherigen Schritt erstellt haben. Über diese Option kann jeder ESXi-Host im Managementcluster auf den Datenträger 'Mgmt-Lun0' zugreifen. Führen Sie diesen Vorgang auch für **Capacity-LUN0** aus.

## Schritt 4: Datenträger in Management-/Kapazitätsclustern anhängen

Melden Sie sich bei vSphere Web Client an und navigieren Sie in den vCenter-Bestandslisten zu **Hosts******.

Führen Sie die folgenden Schritte aus, um den Datenträger auf den ESXi-Hosts anzuhängen:

1. Wählen Sie einen Host aus, und klicken Sie auf **Verwalten > Speicher** > **Speicheradapter**.
2. Wählen Sie **Ziele** > **Dynamische Erkennung** > **Hinzufügen...** aus.
3. Geben Sie die IP-Adresse, die der Speichereinheit 'QuantaStor' in 'Speicherpfad A' zugeordnet ist, in der Anzeige **Sendezielserver hinzufügen** ein.
4. Behalten Sie **3260** als Port bei und klicken Sie auf **OK**.
5. Klicken Sie auf **Dynamische Erkennung** > **Hinzufügen...**. Wiederholen Sie die Schritte 4 und 5 für den Speicherpfad B.

Der ESXI-Host kann nun iSCSI Software Adapter erneut scannen, um den Datenträger Mgmt-Lun0 zu erkennen.

1. Wählen Sie das Symbol **Speicheradapter erneut scannen** (Abbildung 9) in der Anzeige **Speicheradapter** aus.
2. Behalten Sie die Standardoption in dem angezeigten Dialogfenster bei und klicken Sie auf **OK**.
3. Klicken Sie nach dem Erkennen des Datenträgers auf **Aktionen > Neuer Datenspeicher** und formatieren Sie den Datenträger mit dem Format **VMFS-5**.
4. Stellen Sie sicher, dass das Formatieren abgeschlossen ist, und klicken Sie auf **Speichereinheiten > Einheitendetails > Multipathing bearbeiten...**.
5. Wählen Sie **Umlauf** als **Pfadauswahlrichtlinie** aus und klicken Sie auf **OK**.

Nachdem der Datenträger Mgmt-Lun0 nun einem einzelnen Host zugeordnet ist, müssen Sie den Prozess auf den anderen Managementhosts im Cluster wiederholen, um den Datenträger hinzuzufügen. Sie können jedoch auf das Formatieren des Datenträgers verzichten, da er bereits das Format VMFS-5 aufweist und nach der Erkennung entsprechend angezeigt wird.

## Schritt 5: Verzögerte Bestätigung (ACK) für vSphere ESXi-Hosts inaktivieren

Die verzögerte Bestätigung muss inaktiviert werden, nachdem die Speicher-LUNs an die Management- und Kapazitätshosts angehängt wurden.

1. Navigieren Sie zur vSphere-Umgebung und wählen Sie **Speicheradapter** > **iSCSI Software Adapter** > **Erweiterte Optionen** aus.
2. Klicken Sie auf **Bearbeiten** und blättern Sie zum Ende der Anzeige 'Erweiterte Optionen'.
3. Wählen Sie das Kontrollkästchen für verzögerte Bestätigung (DelayedACK)**** ab und klicken Sie auf **OK**.

Weitere Informationen zur verzögerten Bestätigung in VMware finden Sie in [VMware Knowledge Base](https://kb.vmware.com/s/article/1002598).

Sie können nun zum Cookbook [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) zurückkehren und das Einrichten der Umgebung abschließen.
