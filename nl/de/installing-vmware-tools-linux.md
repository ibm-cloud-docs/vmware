---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# VMware Tools unter Linux installieren

VMware Tools ist eine Suite mit Dienstprogrammen, die das Leistungsverhalten des Betriebssystems der virtuellen Gastmaschine und die Verwaltung der virtuellen Maschine verbessert. Die Installation von VMware Tools im Gastbetriebssystem ist von entscheidender Bedeutung. Wenn das Gastbetriebssystem ohne VMware Tools ausgeführt wird, verzichten Sie auf wichtige Funktionen und auf Bedienungskomfort.

Der Service trägt unter Linux, FreeBSD und Solaris den Namen `vmware-guestd`. Der Service `vmware-guestd` führt innerhalb des Gastbetriebssystems die folgenden Aufgaben aus:

* Nachrichten vom Hostbetriebssystem an das Gastbetriebssystem übermitteln
* Im Betriebssystem Befehle zum ordnungsgemäßen Herunterfahren oder Neustart eines Linux-, FreeBSD- oder Solaris-Systems ausführen, wenn Sie Stromversorgungsfunktionen in der Workstation auswählen
* Die Systemzeit des Gastbetriebssystems und des Hostbetriebssystems synchronisieren
* Scripts zum Automatisieren der Operationen des Gastbetriebssystems ausführen (die Scripts werden ausgeführt, wenn sich der Stromversorgungsstatus der virtuellen Maschine ändert)

Der Service wird beim Starten des Gastbetriebssystems gestartet.

Um VMware Tools auf einem Linux-Server zu starten, klicken Sie mit der rechten Maustaste auf den entsprechenden Server in Ihrem vSphere-Client, bewegen Sie den Mauszeiger auf **Gast** und klicken Sie auf **VMware Tools installieren/aktualisieren**.

Über diesen Link wird ein virtuelles CD-ROM-Laufwerk mit den Produktmedien von VMware Tools angehängt. Führen Sie die folgenden Schritte aus, um die Tools zu installieren, nachdem Sie das virtuelle CD-ROM-Laufwerk angehängt haben:
1. Hängen Sie das CD-ROM-Laufwerk mit dem folgenden Befehl an: `mount /dev/cdrom /mnt`.
2. Stellen Sie sicher, dass die Datei vorhanden und ordnungsgemäß angehängt ist, indem Sie den Befehl `ls /mnt` für das angehängte Verzeichnis ausführen. Die Datei `VMWareTools-4.0.0-208167.i386.rpm` wird angezeigt. 
3. Führen Sie den Befehl `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm` aus.
4. Führen Sie den folgenden Befehl aus, um VMware Tools für den aktiven Kernel zu konfigurieren: `/usr/bin/vmware-config-tools.pl`. **Hinweis:** Während der Ausführung der Konfigurationsänderungen werden Sie aufgefordert, die **EINGABETASTE** zu drücken.
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**Hinweis:** Ein Neustart der VM nach dem Installieren von VMware Tools ist nicht erforderlich. Es wird jedoch empfohlen, einen Neustart auszuführen.

Wenn VMware Tools ordnungsgemäß installiert wurde, wird in der Schnittstelle Ihres vSphere-Clients 'OK' angezeigt.
