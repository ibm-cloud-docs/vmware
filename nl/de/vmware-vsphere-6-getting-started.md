---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Einführung in VMware vSphere 6 

Die folgenden Informationen bieten eine Einführung in vSphere 6.

## Informationen zur Umgebung und zur Konfiguration

Zur Optimierung Ihrer VMware-Lösung wird die Verwendung eines privaten VLAN-Netzes und eines öffentlichen Netzes für Ihre VMware vSphere-Umgebung empfohlen (der öffentliche Port kann inaktiviert werden, falls er nicht benötigt wird). Dieses Bereitstellungsprofil ermöglicht die folgenden Datenverkehrsbegrenzungen für Segmente der Ebene 2:

|Beispiel-VLAN-ID|Beschreibung|Typ|Zusätzliche Informationen|
|---|---|---|---|
|VLAN1 - **1101**|Management, VxLAN|Privat, BCR|Natives VLAN ohne Kennzeichnung; ursprüngliches natives VLAN, in dem die VMWare-Hosts zum Zeitpunkt der Bestellung implementiert werden|
|VLAN4 - **2200**|DMZ mit öffentlichem Internetzugang|Öffentlicher FCR|Natives VLAN ohne Kennzeichnung; ursprüngliches natives VLAN, in dem die VMWare-Hosts zum Zeitpunkt der Bestellung implementiert werden|
{: caption="Tabelle 1. Beispiele für privates und öffentliches VLAN" caption-side="top"}

## vSphere-Server bestellen
1. Melden Sie sich bei [{{site.data.keyword.slportal_full}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://control.softlayer.com/){: new_window} an.
2. Klicken Sie auf **Konto > Bestellung einreichen**.
3. Klicken Sie im Abschnitt **Bare-Metal-Server** auf **Monatlich**.
4. Wählen Sie die Server aus. Angaben zu den Mindestvoraussetzungen finden Sie in den VMware Support-Veröffentlichungen:
  * Für das Beispiel wurden die folgenden Server ausgewählt. **Hinweis:** Doppelte, nicht gebundene öffentliche und private Uplinks sind für die Redundanz erforderlich. Stellen Sie sicher, dass die Rechenzentren, in denen Ihre VLANs erstellt wurden, über nicht gebundene Uplinks verfügen.
  * Kapazitätscluster (Anzahl: 2)
    * Serverkonfiguration: Wählen Sie einen Intel Xeon v3-Server im Abschnitt für Mehrkern-Server mit Dualprozessor aus
    * Software: Betriebssystem = vSphere Enterprise Plus 6
    * Betriebssystemspeicher: 2 x 1 TB SATA (als RAID 1 konfiguriert)
    * Datenspeicher: Empfehlen Sie die Bestellung von SATA mit 2 TB oder SSD mit 1,2 TB oder Endurance- bzw. Performance-NFS-SAN-Speicher
      * Wenn Sie an anderen Speichertypen interessiert sind, finden Sie weitere Informationen in [Speicher für die Verwendung mit VMware-Systemen](select-storage-option-use-vmware.html)
      * Uplink-Port-Geschwindigkeiten: duale öffentliche und private Netze (nicht gebunden) mit 1 Gb/s
        * Für VMware vSAN-Lösungen werden Uplinks mit 10 Gb/s empfohlen
5. Wenn Sie eine neue Implementierung in einem neuen IBM Cloud-Rechenzentrum erstellen, fahren Sie mit Schritt 6 fort. Wenn es um eine Erweiterung oder eine Implementierung in einem bestehenden Rechenzentrum geht, wählen Sie das bevorzugte Back-End-BCR-VLAN und Front-End-FCR-VLAN aus. Beispiel: Das Back-End-BCR-VLAN ist 1101 und das Front-End-FCR-VLAN ist 2200. **Hinweis:** Wenn es sich um eine neue Implementierung oder eine neue Implementierung in einer neuen DC handelt, werden Back-End-BCR-VLAN und Front-End-FCR-VLAN bei Ihrer Serverbestellung erstellt.
6. Geben Sie Werte für **Hostname** und **Domäne** ein.
7. Überprüfen Sie die Bestellung und klicken Sie auf **Bestellung abschließen**, um den Bereitstellungsprozess zu starten.

## vCenter-Server bestellen

vCenter ist ein Add-on für Windows Server. In dieser Konfiguration können bis zu 20 vSphere-Hosts vertikal skaliert werden. Für größere Implementierungen wird empfohlen, die vCenter-Server-Appliance (VCSA), wie in [vCenter-Server-Appliance (vCSA) implementieren und konfigurieren](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html) erläutert, direkt in einem vSphere-Cluster zu implementieren.

Gehen Sie wie folgt vor, um einen virtuellen Server mit installiertem vCenter zu bestellen:

1. Melden Sie sich beim {{site.data.keyword.slportal_short}} an.
2. Klicken Sie auf **Konto > Bestellung einreichen**.
3. Bestellen Sie eine **monatliche** Bare-Metal-Serverinstanz oder eine Instanz eines virtuellen Servers (VSI) für öffentliche/private Knoten unter 'Virtuelle Server'.
  1. Damit eine SoftLayer-VSI (virtuelle Serverinstanz) für vCenter 6.0 qualifiziert ist, muss sie auf mindestens **4 Kernen mit je 2,0 GHz** und mit **4 GB RAM** implementiert werden.
  2. Eine Liste der Empfehlungen für vCenter-Implementierungen finden Sie in der Veröffentlichung [VMware vCenter Server&trade; 6.0 Deployment Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}.
4. Geben Sie die folgenden Informationen ein:
  * Basierend auf der empfohlenen Mindestkonfiguration für Server
    * vCPU-Basiskonfiguration: 4 Kerne mit je 2,0 GHz
    * RAM-Konfiguration: 12 GB RAM
    * Software: Betriebssystem = Windows Server 2012 R2 Standard Edition (64 Bit)
    * Betriebssystemspezifisches Add-on: vCenter 6
    * Erste Platte: 1 x 100 GB (SAN)
    * Zweite Platte: 1 x 50 GB (SAN)
    * Uplink-Port-Geschwindigkeiten: 1 Gb/s für öffentliche und private Netz-Uplinks

5. Wenn dies eine neue Implementierung in einem neuen IBM Cloud-Rechenzentrum ist, fahren Sie mit dem Schritt 6 unten fort. Wenn diese Implementierung eine Erweiterung oder eine Implementierung in einem vorhandenen Rechenzentrum ist, wählen Sie das bevorzugte Back-End-BCR-VLAN und Front-End-FCR-VLAN aus. Im vorliegenden Beispiel wird 1101 als Back-End-BCR-VLAN verwendet und 2200 als Front-End-FCR-VLAN. (Wenn es sich um eine komplett neue Implementierung oder eine neue Implementierung in einer neuen DC handelt, werden Back-End-BCR-VLAN und Front-End-FCR-VLAN bei Ihrer Serverbestellung erstellt.)
6. Geben Sie Werte für **Hostname** und **Domäne** ein.
7. Überprüfen Sie die Bestellung und klicken Sie auf **Bestellung abschließen**, um den Bereitstellungsprozess zu starten.

## Portierbare öffentliche und private Teilnetze bzw. IP-Adressen bestellen

**Hinweis:** Setzen Sie diesen Vorgang erst fort, nachdem die Bereitstellung der VLANs vollständig abgeschlossen ist.

Die Teilnetze werden zum Adressieren des kernelbasierten Datenverkehrs für die virtuelle VMware-Gastmaschine (VM) und den VMware-Host verwendet.

1. Klicken Sie im Steuerportal auf **Netz > IP-Verwaltung > Teilnetze**.
2. Klicken Sie rechts oben in der Anzeige auf **IP-Adressen bestellen**.
3. Wählen Sie **Portierbare private** aus.
4. Wählen Sie das entsprechende VLAN aus (z. B. bcr01.wdc04: 1101).
5. Klicken Sie auf **Weiter**.
6. Füllen Sie das Formular **IP-Adressen bestellen** aus.
7. Klicken Sie oben rechts in der Anzeige auf **IP-Adressen bestellen**.
8. Klicken Sie auf **Bestellung aufgeben**.
9. Führen Sie diesen Vorgang für jedes zugehörige VLAN aus (z. B. 1101, 2200).
  1. Weitere Informationen zu VLANs finden Sie in [Einführung in VLANs](/docs/infrastructure/vlans/getting-started.html).

|Teilnetztyp|Teilnetzgröße|Gebundenes VLAN|vSphere-Host-Nutzung|
|---|---|---|---|
|Portierbar - Privat|/27 32 Adressen|**1101**|Management-VMs|
|Portierbar - Privat|/27 32 Adressen|**1101**|VM-Kernelports für iSCSI und vMotion|
|Portierbar - Privat|/27 32 Adressen|**1101**|Private IPs für Gast-VM|
|Portierbar - Öffentlich|/27 32 Adressen|**2200**|Öffentliche IPs für Gast-VMs (optional)|
{: caption="Tabelle 2. Teilnetze" caption-side="top"}

### Optional: Allgemein zugängliche Schnittstelle auf dem vSphere-Host inaktivieren

Sie können die allgemein zugänglichen vSphere-Schnittstellen zu Sicherheitszwecken inaktivieren, wenn sie nicht verwendet werden sollen.

1. Klicken Sie im Steuerportal auf **Einheiten > Einheitenliste**.
2. Klicken Sie auf den Namen Ihres vSphere-Hosts.
3. Klicken Sie auf die Tabelle 'Konfiguration' und blättern Sie zum Abschnitt 'Netz'.
4. Wählen Sie **Trennen** für jedes zugehörige Paar mit vSphere-Host und 'eth1' bzw. 'eth3' aus.

Dies kann auch über [{{site.data.keyword.slapi_full}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window} erfolgen.

## vSphere Data Center Cluster erstellen und konfigurieren<!-- create and configure should be separate tasks-->

Sie können sich nun beim vCenter-Server anmelden und den vSphere-Cluster konfigurieren.

1. Klicken Sie im Steuerportal auf**Einheiten > Einheitenliste**
2. Suchen Sie Ihre vCenter-Einheit und klicken Sie auf den Einheitennamen.
3. Blättern Sie in der Anzeige **Einheitendetails** zum Abschnitt **Netz** für den Server und notieren Sie die **Private IP-Adresse**.
4. Blättern Sie in der Anzeige **Einheitendetails** nach unten und notieren Sie das **Kennwort** für das Windows-Betriebssystem und für die vCenter-Software.
5. Öffnen Sie eine Microsoft Remote Desktop-Sitzung (RDP-Sitzung) und stellen Sie über die öffentliche IP-Adresse eine Verbindung zu Ihrem vCenter-Server her.
6. Melden Sie sich mit den Kennwörtern an, die Sie in Schritt 4 notiert haben. **Hinweis:** Eine aktive VPN-Verbindung zu IBM Cloud ist erforderlich, um mit der privaten IP-Adresse auf vCenter zuzugreifen. Weitere Informationen zum VPN-Zugriff finden Sie in [Zugriff auf das private Netz der IBM Cloud-Infrastruktur aktivieren](/docs/customer-portal/getting-started.html#enable-private-network).
7. Laden Sie den konventionellen [vSphere-Client ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window} herunter oder verwenden Sie vSphere Web Client über den Link `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/`.
8. Melden Sie sich bei vCenter mit der IP-Adresse und den Kennwörtern an, die Sie in den Schritten 3 und 4 notiert haben.
9. Klicken Sie im linken Teilfenster mit der rechten Maustaste auf den Namen des vCenter-Servers und wählen Sie **Neues Rechenzentrum** aus.
10. Geben Sie einen geeigneten Namen für das Rechenzentrum ein.
11. Klicken Sie mit der rechten Maustaste auf das Rechenzentrum und wählen Sie **Neuer Cluster** aus.
12. Geben Sie einen Clusternamen ein. VERZICHTEN Sie zu diesem Zeitpunkt auf das Aktivieren von Cluster-Features, vSphere HA und vSphere DRS.
13. Klicken Sie auf **Weiter**.
14. Lassen Sie **EVC** inaktiviert und klicken Sie auf **Weiter**.
15. Akzeptieren Sie die Standardeinstellung (_Auslagerungsdatei im gleichen Verzeichnis wie die virtuelle Maschine speichern_) und klicken Sie auf **Weiter**.
16. Klicken Sie auf **Fertigstellen**, um den Cluster abzuschließen.
17. Klicken Sie mit der rechten Maustaste auf den neuen Cluster, den Sie soeben erstellt haben, und wählen Sie **Host hinzufügen** aus.
18. Geben Sie die IP-Adresse oder den Hostnamen eines vSphere-Hosts ein und geben Sie **Root** in das Feld **Benutzername** sowie das Kennwort für den Host in das Feld **Kennwort** ein.
19. Klicken Sie jeweils auf **Weiter** in den Anzeigen für Host-Zusammenfassung, Lizenzzuordnung und Sperrmodus und klicken Sie anschließend auf **Fertigstellen**, um das Hinzufügen Ihres Hosts zu dem Cluster abzuschließen.
20. Wiederholen Sie die Schritte 18 und 19 für jeden weiteren vSphere-Host in Ihrem Cluster. Anschließend werden alle vSphere-Hosts unter dem neuen Cluster angezeigt.

### Basisnetzkonstrukt für die vSphere-Hosts konfigurieren

Führen Sie die folgenden Schritte aus, um das Basiskonstrukt für die vSphere-Hosts in Ihrem Cluster zu konfigurieren.

1. Wählen Sie den ersten vSphere-Host aus und klicken Sie auf die Registerkarte **Konfiguration**.
2. Wählen Sie unter **Hardware** die Option **Netzbetrieb** aus. 'vSwitch0' mit 'vmnic0' müssten bereits vorhanden sein. Klicken Sie auf **Eigenschaften** neben 'vSwitch0'.
3. Wählen Sie **Netzadapter** im Fenster für die vSwitch-Eigenschaften**** aus und klicken Sie auf die Schaltfläche **Hinzufügen**.
4. Wählen Sie 'vmnic2' zum Hinzufügen zu 'vSwitch0' aus und klicken Sie auf **Weiter**.
5. Stellen Sie sicher, dass beide vmnic-Instanzen **Aktive Adapter** sind und klicken Sie auf **Weiter**.
6. Klicken Sie auf **Fertigstellen**.
7. Klicken Sie auf die Registerkarte **Ports** und stellen Sie sicher, dass 'vSwitch' hervorgehoben ist. Klicken Sie auf **Bearbeiten**.
8. Klicken Sie auf die Registerkarte **Allgemein** und ändern Sie den Wert für **MTU** in '9000' (Jumbo-Frame).
9. Klicken Sie auf die Registerkarte **NIC-Teaming**, ändern Sie den Hashwert für den Lastausgleich in **Route auf IP-Basis** und klicken Sie auf **OK**.
10. Führen Sie die Schritte 1 bis 8 aus, um die vmnic-Instanzen für die übrigen vSphere-Hosts in Ihrem Cluster zu konfigurieren.

Eine Portgruppe für vMotion muss hinzugefügt werden. Die Gruppe kann als virtueller Standard-Switch (VSS) oder als virtueller verteilter Switch (Virtual Distributed Switch, VDS) erstellt werden. Für das vorliegende Beispiel wird ein VSS-Switch erstellt.

1. Wählen Sie die Registerkarte **Konfiguration** und die Option **Netzbetrieb** aus.
2. Klicken Sie auf **Eigenschaften...** für 'vSwitch0'.
3. Klicken Sie auf **Hinzufügen...** um eine Portgruppe zu erstellen.
4. Wählen Sie **VMkernel** aus und klicken Sie auf **Weiter**.
5. Geben Sie in den Eigenschaften für die Portgruppe die folgenden Informationen ein:
  * **Netzbezeichnung:** Ein geeigneter Name für die Portgruppe.
  * **VLAN-ID (optional):** Die VLAN-ID für den vMotion-Datenverkehr (im vorliegenden Beispiel 1101). Mithilfe der VLAN-ID kann VMware den Datenverkehr für das jeweilige VLAN kennzeichnen.
  * Wählen Sie **Diese Portgruppe für vMotion verwenden** aus.
6. Klicken Sie auf **Weiter**.
7. Geben Sie eine **Portierbare IP-Adresse** für das VLAN ein. (Sie können die Port-IP-Adresse im SoftLayer-Portal über **Netz > IP-Verwaltung > VLANs** abrufen. Wählen Sie das richtige VLAN aus. Unter **Teilnetze** wird ein Bereich mit portierbaren IP-Adressen angezeigt. Wenn keine portierbare IP-Adresse verfügbar oder Ihr aktueller Pool ausgeschöpft ist, führen Sie die Schritte im Abschnitt 'Private Teilnetze / IP-Adressen bestellen' aus, um eine weitere portierbare IP-Adresse zu bestellen.
8. Klicken Sie auf **Weiter** und anschließend auf **Fertigstellen**, um den Vorgang abzuschließen.

Führen Sie die folgenden Schritte aus, um eine Portgruppe für VM-Datenverkehr zu erstellen.

1. Klicken Sie auf **Eigenschaften...** für 'vSwitch0' und wählen Sie **Hinzufügen > Virtuelle Maschine** aus.
2. Geben Sie in den Eigenschaften für die Portgruppe**** die folgenden Informationen ein:
  * **Netzbezeichnung:** Geben Sie den Namen für die Portgruppe ein (z. B. VM-Daten).
  * **VLAN-ID (optional):** Geben Sie eine VLAN-ID ein (im vorliegenden Beispiel wird 1101 verwendet). Mithilfe der VLAN-ID kann VMware den Datenverkehr für das jeweilige VLAN kennzeichnen.

### Optional: Lizenzen für VMware-Add-ons (NSX, vRealize, vSAN usw.) installieren

Nachdem die VMware-Umgebung nun gestartet ist, können Sie mit dem Implementieren weiterer Konfigurationen, Gast-VMs oder VMware-Add-ons fortfahren. Lizenzen für VMware-Add-ons können auch über das IBM Cloud-Steuerportal erworben und über Ihre vCenter-Konsole hinzugefügt werden. Weitere Informationen zum Bestellen und Verwalten von Lizenzen für VMware-Add-ons finden Sie in [VMware vSphere 6-Lizenzen bestellen und verwalten](vmware-vsphere-6-ordering-and-managing-licenses.html).

## Nächste Schritte
Sie verfügen nun über eine einfache Single-Site-VMware-Umgebung, die in einem IBM Cloud-Rechenzentrum ausgeführt wird. Die Basiskonfiguration verfügt lediglich über einen lokalen Datenspeicher und ist damit eine vereinfachte Konfiguration ohne Features wie VMware-DRS, Hochverfügbarkeit, Speicher-DRS und eine Firewall.

Weitere Informationen finden Sie in [Häufig gestellte Fragen (FAQs) zu VMware](vmware-faq.html). 
