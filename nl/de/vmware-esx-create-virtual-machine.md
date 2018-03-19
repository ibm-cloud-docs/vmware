---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Virtuelle VMware-ESX-Maschine erstellen

Führen Sie die folgenden Schritte aus, um eine neue virtuelle Maschine zu erstellen.{:shortdesc}

1. Klicken Sie im Teilfenster 'Bestand' des vSphere-Clients mit der rechten Maustaste auf die IP-Adresse Ihres Hostknotens.
2. Wählen Sie im Konfigurationsfenster **Angepasst** aus.
3. Weisen Sie der virtuellen Maschine einen geeigneten Namen zu und klicken Sie auf **Weiter**.
4. Wählen Sie die Speicherposition für Dateien der virtuellen Maschine aus und klicken Sie auf **Weiter**.
5. Wählen Sie unter **Version der virtuellen Maschine** den Eintrag **Virtual Machine Version 8** aus. <!-- since we are using vSphere instead of the Web Client to create it (in which case we would use version 11 instead).-->
6. Wählen Sie das **Betriebssystem** aus.
7. Wählen Sie die Anzahl der virtuellen Prozessoren (**Seite 'CPU'**) und die Kapazität für den **Hauptspeicher** der zu erstellenden virtuellen Maschine aus. **Hinweis:** Sie können die Prozessoranzahl und die Größe des Arbeitsspeichers später ändern, wenn die entsprechenden Ressourcen zur Verfügung stehen.
Im Netzabschnitt müssen Sie zwei NIC-Instanzen anbinden (dabei stellt NIC das private Netz dar und NIC 2 das öffentliche Netz). Der Adaptertyp lautet 'Flexibel'. Stellen Sie sicher, dass **Beim Einschalten verbinden** ausgewählt ist.
8. Behalten Sie in der Anzeige **SCSI-Controller** die Standardeinstellung für parallele LSI-Logik bei. Wählen Sie in der Anzeige **Platte auswählen** die Option **Neue virtuelle Platte erstellen** aus. Behalten Sie in den Anzeigen **Erweiterte Optionen** und **Bereit zum Abschließen** ebenfalls die Standardeinstellungen bei. Die Erstellung der neuen virtuellen Maschine ist nun abgeschlossen. 

Klicken Sie in der Bestandsliste auf den Servernamen, um mit dem Laden der Installationsmedien zu beginnen. Klicken Sie anschließend auf **Einstellungen für die virtuelle Maschine bearbeiten** unter **Grundlegende Tasks**.

9. Während **CD/DVD Drive 1** ausgewählt ist, aktivieren Sie das Kontrollkästchen **Beim Einschalten verbinden** unter 'Gerätestatus'. Klicken Sie auf **Durchsuchen**, um eine ISO-Datei anzugeben, die sich auf Ihrem Datenspeicher befindet.
10. Hier können die in den Standarddatenspeicher 'Storeage1' hochgeladenen ISO-Dateien ausgewählt werden. Außerdem werden die Ordner für Konfigurations- bzw. Protokolldateien angezeigt, die in Schritt 3 im Abschnitt **Datenspeicher** des Prozesses 'Neue virtuelle Maschine erstellen' für alle virtuellen Servermaschinen eingerichtet wurden.

Nachdem Sie das gewünschte ISO-Image ausgewählt haben, können Sie mit dem Installationsprozess des entsprechenden Betriebssystems beginnen.

Weitere Informationen zum Konfigurieren eines Netzes mit virtuellen Maschinen finden Sie in [Netz mit virtuellen Maschinen einrichten](/docs/infrastructure/virtualization/virtual-machine-network-setup.html){:new_window}.
