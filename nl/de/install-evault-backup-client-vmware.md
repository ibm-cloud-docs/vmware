---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# EVault Backup-Client für VMware installieren

Der EVault Backup-Client kann auf einem VMware-Server mit einer Reihe von Befehlen in der Shell oder über das Terminal auf dem ESX-Zielserver installiert werden. In der vorliegenden Prozedur werden die erforderlichen Schritte zum Installieren des EVault Backup-Clients auf Ihrem VMware-Server erläutert:
{:shortdesc}

Um den Agenten zu installieren, laden Sie die das Paket ` Agent-VMware-ESX-Server-6.71<version-info>.tar.gz` mit dem folgenden Befehl auf den ESX-Zielserver herunter und kopieren Sie es:

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**Hinweis:** Die folgenden Schritte müssen lokal auf dem ESX-Zielserver ausgeführt werden.

1. Extrahieren Sie die Dateien aus dem Paket. Verwenden Sie dazu den folgenden Befehl (dabei ist “PACKAGENAME” möglicherweise “Agent-VMware-ESX-Server-6.71”):<br/>`tar xvfz PACKAGENAME.tar.gz`
2. Wechseln Sie in das Verzeichnis, in das Sie das Paket extrahiert haben.
3. Führen Sie das Installationsscript aus:<br />`# ./install.sh`<br/><br/>
**Hinweis:** Das Installationsscript fragt im Dialogbetrieb Konfigurationsdaten wie die Webregistrierung (Adresse, Portnummer und Authentifizierung) und den Protokolldateinamen ab.

Geben Sie den WebCC-Benutzernamen für diesen Server ein.

4. Geben Sie den **EVault Backup-Benutzernamen** in die Eingabeaufforderung für den WebCC-Benutzernamen ein. Anweisungen zum Anzeigen des EVault Backup-Benutzernamens finden Sie in der Prozedur [View EVault Backup Storage Details](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal).
5. Geben Sie das EVault Backup-Kennwort in die Eingabeaufforderung für das WebCC-Kennwort ein.
6. Nach Beendigung der Installation wird eine Abschlussnachricht angezeigt und der Agentendämon wird ausgeführt.


Weitere Installationshinweise:<br/>
Die Datei Install.log befindet sich im Installationsverzeichnis, wenn die Installation erfolgreich durchgeführt wurde.<br/>
Beispiel: `/opt/BUAgent/Install.log`.

Wenn die Installation fehlschlägt und rückgängig gemacht wird, befindet sich das Installationsprotokoll im `<Installation Failure directory>.`<br/>
Falls die Installation fehlschlägt und nicht rückgängig gemacht wird, befindet sich das Installationsprotokoll im `<Installation Kit directory>`.<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
Stellen Sie sicher, dass Sie mit dem {{site.data.keyword.BluSoftlayer_full}}-VPN verbunden sind, um den obigen Link anzuzeigen. Weitere Informationen zum Herstellen einer Verbindung zum IBM Cloud-VPN finden Sie in [Zugriff auf das private Netz der IBM Cloud-Infrastruktur aktivieren](/docs/customer-portal/getting-started.html#enable-private-network).
