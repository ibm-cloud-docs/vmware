---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# vCenter Server Appliance (vCSA) mit VMware vSphere 6 implementieren und konfigurieren  

Führen Sie die folgenden Schritte aus, um eine VMware vCenter-Server-Appliance zu implementieren.
{:shortdesc}

**Voraussetzungen**
* Windows-System mit installiertem kompatiblem Browser
  * Internet Explorer / Firefox / Chrome
* vSphere-Hosts mit ausreichenden Ressourcen für die Unterstützung einer VMware vCenter-Server-Appliance
  * Weitere Informationen zu erforderlichen Systemressourcen finden Sie in [Minimum requirements for the VMware vCenter Server 6.0 Appliance ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://kb.vmware.com/s/article/2106572){: new_window}.
* ISO-Image für vCSA
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* Möglichkeit zum Anhängen eines ISO-Image
* VPN-Sitzung mit Zugang zu IBM Cloud Private Network

**vCenter-Server-Appliance implementieren und konfigurieren**

1. Hängen Sie das ISO-Image für vCenter Server Appliance (vCSA) an.
2. Öffnen Sie die Datei vcsa-setup.html in einem kompatiblen Browser.
3. Prüfen und akzeptieren Sie die Installation des Plug-ins für VMware Client Integration.
4. Klicken Sie auf **Zulassen**.
5. Klicken Sie auf **Installieren**.
6. Prüfen und akzeptieren Sie die Bedingungen der Lizenzvereinbarung und klicken Sie anschließend auf **Weiter**.
7. Geben Sie den FQDN oder die private IP-Adresse sowie den Benutzernamen und das Kennwort des VMware-Hosts ein, auf dem Sie die vCSA installieren möchten. Klicken Sie auf **Weiter**.
8. Klicken Sie auf **Ja**, um die Zertifikatswarnung zu akzeptieren.
9. Geben Sie einen geeigneten Appliance-Namen und ein zugehöriges Betriebssystemkennwort ein und klicken Sie auf **Weiter**.
10. Wählen Sie als Implementierungstyp 'vCenter-Server mit Embedded Platform Services Controller installieren' aus und klicken Sie anschließend auf **Weiter**.
11. Klicken Sie auf 'SSO-Domäne erstellen' und dann auf **Weiter**. <!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. Wählen Sie eine Größe für die Appliance aus und klicken Sie auf **Weiter**.
13. Wählen Sie einen Datenspeicher aus und klicken Sie auf **Weiter**.
14. Wählen Sie 'Integrierte Datenbank (PostgreSQL) verwenden' aus und klicken Sie auf 'Weiter'.
15. Richten Sie Ihre Netzkonfigurationen ein, indem Sie die folgenden Informationen eingeben:
  1. Netz
  * IP-Adressfamilie
  * Netztyp
  * Netzadresse
  * Systemname
  * Teilnetzmaske
  * Netzgateway
  * Netz-DNS-Server
      * Weitere Informationen finden Sie in [Was sind lokale DNS-Auflöser?](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-).
  * Konfigurieren Sie die Zeitsynchronisation.
  * Klicken Sie auf **Weiter**.
16. Prüfen Sie die Einstellungen und klicken Sie anschließend auf **Fertigstellen**. Ihre vCSA-Instanz wird bereitgestellt.

