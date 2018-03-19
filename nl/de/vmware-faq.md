---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Häufig gestellte Fragen (FAQs) zu VMware 

## Welche Lizenzierungsstufe wird aktiviert, wenn Sie vSphere über das IBM Cloud-Portal implementieren?

Enterprise Plus, die höchste vSphere-Lizenzierungsstufe.

## Wie wird VMware vSphere 6 lizenziert?

Das Lizenzierungsverfahren ist an Ihren Implementierungsmechanismus gebunden. Sie haben zwei Möglichkeiten zum Implementieren von VMware 6:

1. Wenn Sie vSphere über das Steuerportal implementieren, wird automatisch die VSPP-Lizenzierung (VSPP = VMware Service Provider Program) aktiviert. Beim Implementieren wird ein Standardbenutzer (slvmadmin) in der Steuerkonsole auf dem Host für vSphere-Administrations- und -Integrationsservices hinzugefügt.

2. Beim manuellen Implementieren von vSphere können Sie eigene Lizenzen (Bring Your Own Licence, BYOL) oder eigene Medien (Bring Your Own Media, BYOM) bereitstellen, d. h. Sie können Ihre Standardlizenzen auf diese Hosts anwenden.**Hinweis:** Wenn Sie beabsichtigen, eigene VMWare-Lizenzen zu verwenden, sollten Sie den Server mit einem freien Betriebssystem wie CentOS oder ohne Betriebssystem (NO OS) bestellen. Installieren Sie anschließend das VMware-Betriebssystem mit dem [Virtuellen ISO-Image](../bare_metal/mount-iso-bare-metal-server.html) und IPMI.

## Kann ich eine isolierte private VMware-Cloud erstellen?

Ja, Sie können Bare-Metal-Systeme implementieren und alle unterstützten Hypervisor (einschließlich VMware ESX) auf diesen Hosts installieren. Sie können virtuelle Maschinen auch mit den nativen Management-Tools implementieren. Standardmäßig werden Systeme zur Abgrenzung in VLANs implementiert und mithilfe von Netzkomponenten (z. B. Gateways, Router und Firewalls) kann nahezu jede Topologie erstellt werden.

## Wie wird VMware lizenziert?

Das Lizenzierungsverfahren ist an Ihren Implementierungsmechanismus gebunden. Sie haben zwei Möglichkeiten zum Implementieren von VMware:

1. Wenn Sie ESX über das Portal implementieren, wird automatisch die VSPP-Lizenzierung (VSPP = VMware Service Provider Program) aktiviert. Bei der Implementierung wird der Standardbenutzer 'vmadmin' zum ESX-Server für die Datenerfassung hinzugefügt. Löschen Sie diesen Standardbenutzer nicht. VSPP stellt Gebühren für RAM in Rechnung, der für alle 'eingeschalteten' virtuellen Maschinen reserviert und genutzt wird (und nicht 'pro Socket', wie bei einer Standardhostlizenz).

2. Beim manuellen Implementieren von ESX können Sie eigene Lizenzen bereitstellen (Bring Your Own Licence, BYOL), d. h. Sie können Standardlizenzen auf diese Hosts anwenden. **Hinweis:** BYOL kann nicht für Hosts verwendet werden, die über das Portal implementiert werden. Es wird erwartet, dass VSPP aktiviert ist.

    * Außerdem ist keine vCenter-Serverinstanz erforderlich, damit VSPP funktionsfähig ist.

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## Kann ich VMware-Komponenten direkt über das IBM Cloud-Portal implementieren?

Ja, Sie haben dabei zwei Möglichkeiten:

1. Automatisches Auswählen und Implementieren des ESX-Hypervisor mit einem monatlich abgerechneten Bare-Metal-System<!-- (Figure 2)-->. Alternativ können Sie die vCenter-Verwaltung zusammen mit einer virtuellen Maschine oder einem Bare-Metal-System automatisch implementieren (nur unter Windows).

2. Implementieren Sie einen Bare-Metal-Host mit einem freien Betriebssystem (z. B. CentOS) und installieren Sie ESX danach manuell über die ferne Konsole und den virtuellen Medienzugriff des Hosts. Anschließend können Sie vCenter-Server manuell installieren oder die unter Linux ausgeführte VMware vCenter-Server-Appliance implementieren.

