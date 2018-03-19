---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-27"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Foire aux questions : VMware 

## Quel niveau de licence est activé lorsque vous déployez vSphere depuis le portail IBM Cloud ?

Enterprise Plus, le niveau le plus élevé de licence vSphere.

## Comment la licence VMware vSphere 6 est-elle octroyée ?

L'approche d'octroi de licence est liée à votre mécanisme de déploiement. Vous pouvez déployer VMware 6 de deux façons différentes :

1. Lorsque vous déployez vSphere depuis le portail de contrôle, la licence VMware Service Provider Program (VSPP) est automatiquement activée. Lors du déploiement, un utilisateur par défaut, "slvmadmin", est ajouté à l'hôte pour les services d'administration et d'intégration de vSphere sur le portail de contrôle.

2. Lorsque vous déployez vSphere manuellement, vous pouvez utiliser vos propres licence et support (BYOL/BYOM), ce qui vous permet d'appliquer vos licences standard à ces hôtes. **Remarque :** Si vous souhaitez utiliser votre propre licence VMWare, il est recommandé de commander le serveur avec un système d'exploitation gratuit, tel que CentOS ou en tant que NO OS. Installez ensuite le système d'exploitation VMWare via l'interface IPMI ([Virtual ISO](../bare_metal/mount-iso-bare-metal-server.html)).

## Puis-je créer un cloud VMware privé et isolé ?

Oui, vous pouvez déployer des systèmes bare metal et installer tout hyperviseur pris en charge (y compris VMware ESX) sur ces hôtes. Vous pouvez également déployer des machines virtuelles en utilisant les outils de gestion natifs. Par défaut, les systèmes sont déployés sur les réseaux locaux virtuels pour les composants d'agrégation et de mise en réseau (passerelle, routeurs et pare-feux) et sont utilisés pour créer presque tout type de topologie.

## Comment la licence VMware est-elle octroyée ?

L'approche d'octroi de licence est liée à votre mécanisme de déploiement. Vous pouvez déployer VMware de deux façons différentes :

1. Lorsque vous déployez ESX depuis le portail, le programme VSPP (VMware Service Provider Program) est automatiquement activé. Lors du déploiement, un utilisateur par défaut, 'vmadmin', est ajouté au serveur ESX pour la collecte de données. Ne supprimez pas cet utilisateur par défaut. VSPP facture la mémoire RAM réservée et utilisée pour toutes les machines virtuelles “sous tension” (et non “par socket” comme une licence d'hôte standard).

2. Lorsque vous déployez ESX manuellement, vous pouvez choisir d'utiliser le type BYOL (Bring Your Own License, licence à fournir) afin d'appliquer des licences standard à ces hôtes. **Remarque :** Le type BYOL ne peut pas être utilisé pour des hôtes déployés via le portail. La licence VSPP doit être activée.

    * En outre, aucune instance vCenter Server n'est requise pour que le programme VSPP fonctionne.

<!--## How do I download VMware add-ons?-->
<!--To download VMware software add-ons, you need to connect to the VPN (SSL or PPTP). The VMware add-ons can then be downloaded from either of the following locations:
http://downloads.service.softlayer.com
or http://downloads.service.usgov.softlayer.com if you're on the Federal network.
All add-ons must be installed and managed through vCenter on your device that is using these license keys. Canceling a device that this software is installed on does not cancel the software license. The license must be canceled from the customer portal on the VMware Licenses page to avoid recurring fees. For more information, see the terms of service. -->

## Puis-je déployer des composants VMware directement depuis le portail IBM Cloud ?

Oui, vous disposez pour cela de deux options :

1. Sélectionner et déployer l'hyperviseur ESX automatiquement avec un système bare metal mensuel<!-- (Figure 2)-->. Vous pouvez également déployer la gestion vCenter automatiquement avec un système de machine virtuelle ou bare metal (Windows uniquement).

2. Déployer un hôte bare metal avec un système d'exploitation gratuit, tel que CentOS, puis installer ESX manuellement via l'accès à la console distante et au support virtuel de l'hôte. Vous pouvez ensuite installer vCenter Server manuellement ou déployer le dispositif VMware vCenter Server qui fonctionne sous Linux.

