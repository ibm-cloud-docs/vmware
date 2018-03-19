---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-10"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Virtuelle Maschine mit VMware vSphere 6 erstellen 

1. Klicken Sie im Teilfenster 'Bestand' des vSphere-Clients mit der rechten Maustaste auf die IP-Adresse Ihres Hostknotens.
2. Wählen Sie im Konfigurationsfenster **Angepasst** aus.
3. Weisen Sie der virtuellen Maschine einen geeigneten Namen zu und klicken Sie auf **Weiter**.
4. Wählen Sie die Speicherposition für Dateien der virtuellen Maschine aus und klicken Sie auf **Weiter**.
* Über das Menü 'Version der virtuellen Maschine' können Sie verschiedene Clustertypen verwenden. Da es sich um einen neuen Cluster handelt und Sie keine Unterstützung für ältere Versionen benötigen, wählen Sie **Virtuelle Maschine Version 8** aus. **Hinweis:** Wenn Sie den Web-Client zum Erstellen eines Clusters verwenden, verwenden Sie Version 11.
5. Wählen Sie den Typ für das **Betriebssystem** aus.
6. Legen Sie die Anzahl der virtuellen Prozessoren (auf der Seite 'CPUs') fest und klicken Sie auf **Weiter**.
  1. **Hinweis:** Sie können die Anzahl der CPUs später ändern, wenn die entsprechenden Ressourcen zur Verfügung stehen.
7. Legen Sie die gewünschte Speicherkapazität für die virtuelle Maschine fest. Klicken Sie auf **Weiter**.
  1. **Hinweis:** Sie können die Speicherkapazität später ändern, wenn die entsprechenden Ressourcen zur Verfügung stehen.
8. Im Netzabschnitt müssen Sie zwei NICs anschließen. Dabei ist NIC 1 für das private Netz bestimmt und NIC 2 für das öffentliche Netz. Der Adaptertyp lautet 'Flexibel'. Stellen Sie sicher, dass das Kontrollkästchen 'Beim Einschalten verbinden' ausgewählt ist.
9. Behalten Sie in der Anzeige 'SCSI-Controller' die Standardeinstellung für parallele LSI-Logik bei. Wählen Sie in der Anzeige 'Platte auswählen' die Option **Neue virtuelle Platte erstellen** aus. Behalten Sie in den Anzeigen **Erweiterte Optionen** und **Bereit zum Abschließen** die Standardeinstellungen bei. Ihre neue virtuelle Maschine wird nun erstellt. Klicken Sie in der Bestandsliste auf den Servernamen, um mit dem Laden der Installationsmedien zu beginnen, und klicken Sie unter 'Basistasks' auf **Einstellungen für virtuelle Maschine bearbeiten**.
<!--* false-->
10. Während 'CD/DVD Drive 1' ausgewählt ist, wählen Sie **Beim Einschalten verbinden** unter 'Gerätestatus' aus. Klicken Sie auf **Durchsuchen**, um eine ISO-Datei anzugeben, die sich auf Ihrem Datenspeicher befindet.
* Hier können die in den Standarddatenspeicher 'Storeage1' hochgeladenen ISO-Dateien ausgewählt werden. Außerdem werden die Ordner mit Konfigurations- bzw. Protokolldateien angezeigt, die in Schritt 3 im Abschnitt 'Datenspeicher' des Prozesses 'Neue virtuelle Maschine erstellen' für alle virtuellen Servermaschinen eingerichtet wurden.
11. Nachdem Sie das gewünschte ISO-Image ausgewählt haben, können Sie mit dem Installationsprozess des entsprechenden Betriebssystems beginnen.
* Wenn Ihre virtuelle Gastmaschine erfolgreich gestartet ist, installieren Sie [VMware Tools![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://kb.vmware.com/s/article/1014294){: new_window}, falls dies unterstützt wird.
* Weitere Informationen zu Anleitungen für den Netzbetrieb finden Sie in [Netz mit virtuellen Maschinen einrichten](/docs/infrastructure/virtualization/virtual-machine-network-setup.html).
