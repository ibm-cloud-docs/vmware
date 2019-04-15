---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# VMware vSphere ESXi mit der fernen Konsole und virtuellen Datenträgern installieren
{: #installing-vsphere-esxi}

Die Vorgehensweise beim Implementieren von ESX mithilfe von Installationsmedien ist bei allen Versionen ähnlich und kann in Szenarios mit selbst bereitgestellten Lizenzen (Bring Your Own License, BYOL) verwendet werden.

## Voraussetzungen
* Eine Instanz einer virtuellen Maschine (VM) mit Zugriff auf das private Netz [z. B. eine Cloud-Computing-Instanz (VSI), installiert unter Windows oder Linux mit einem Java-fähigen Browser, erreichbar über vpn.softlayer.com oder öffentliche IP]. Die VSI muss sich im selben privaten Netz wie die IPMI-Adressen des Servers (IPMI = Intelligent Platform Management Interface) befinden.
* Eine Kopie des ISO-Image von VMware ESXi VIM Installer.

<!--## Steps -->

## Verbindung zu IPMI herstellen
1. Laden Sie das ISO-Image für VMware in die VSI hoch, die in den Voraussetzungen angegeben ist (die VSIs sollten über öffentlichen Webzugriff verfügen).
2. Stellen Sie die Adresse und die Anmeldeinformationen für IPMI aus dem Kundenportal zusammen.
3. Wählen Sie **Einheiten** > **Einheitenliste** > **[Server]** > **Fernverwaltung** aus.
4. Stellen Sie mit Remote Desktop (RDP) oder Remote X die Verbindung zu der VSI her, auf der das ESXi-Image gespeichert ist.
5. Öffnen Sie in der RDP-Sitzung einen Web-Browser und geben Sie die IPMI-Adresse ein, die Sie in Schritt 2 erfasst haben.
6. Melden Sie sich bei der IPMI-Konsole mit den Berechtigungsnachweisen (in der Regel Rootberechtigungen) an, die ebenfalls in Schritt 2 erfasst wurden.
* Notieren Sie sich Ihre IPMI-Benutzerzugriffsebene. Möglicherweise die Administratorebene. Beim Anhängen kann ein Problem auftreten, wenn für den fernen Speicher die Zugriffsebene **Operator** (Bediener) festgelegt ist. Öffnen Sie ein Support-Ticket, damit Ihre IPMI-Berechtigungsnachweise hochgestuft werden, wenn Sie keine Datenträger anhängen können.
7. Vergewissern Sie sich, dass die Anmeldestartseite geöffnet ist, und klicken Sie auf **Fernsteuerung** > **Konsolenumleitung** > **Konsole starten**.

## ISO anhängen
1. Wählen Sie in der Anzeigefunktion der kernelbasierten virtuellen Maschine (KVM) die Optionen **Virtuelle Datenträger** > **Virtueller Speicher** aus. Gegebenenfalls müssen Sie im Betriebssystem und in der Java-Version den Zugriff gewähren, damit die Java-basierte Anzeigefunktion gestartet werden kann.
2. Klicken Sie auf die Registerkarte **CD-ROM & ISO** im Fenster 'Virtueller Speicher'. Wählen Sie für den Typ des logischen Laufwerks die Option **ISO-Datei** aus und klicken Sie auf **Image öffnen**.
3. Navigieren Sie zum ESXi-ISO-Image und klicken Sie auf **OK**. Klicken Sie anschließend auf **Anhängen**.
4. Klicken Sie nach dem Anhängen des ISO-Image auf **OK**.
* Navigieren Sie wieder zur IPMI-Webseite und klicken Sie auf **Remote** > **Steuerung** > **Server zurücksetzen** > **Aktion ausführen**, um den Server erneut zu starten.

### Netzkonfiguration installieren und abschließen
1. Installieren Sie ESXi.
* Nachdem die Installation abgeschlossen ist, stellen Sie sicher, dass das ISO-Image **abgehängt** ist, damit Sie den Server erneut starten können.
2. Starten Sie den Server erneut.
3. Konfigurieren Sie die IP-Adresse des Servers, nachdem er erneut gestartet wurde.
4. Notieren Sie die zugehörigen Details von der Registerkarte 'Konfiguration' der Einheit.

Sie können nun den ESXi-Host verwalten.

Weitere Informationen zum Einrichten des Endurance- oder Performance-Blockspeichers finden Sie in [Blockspeicher bereitstellen und verwalten](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Weitere Informationen zum Einrichten von QuantaStor finden Sie in [Architekturleitfaden für QuantaStor](architecture-guide-quantastor-vmwaresoftlayer.html).
