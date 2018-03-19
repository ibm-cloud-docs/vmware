---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Déploiement et configuration d'un dispositif vCSA (vCenter Server Appliance) avec VMware vSphere 6  

Utilisez la procédure suivante pour déployer un dispositif VMware vCenter Server Appliance.
{:shortdesc}

**Prérequis**
* Système Windows avec un navigateur compatible installé
  * Internet Explorer/Firefox/Chrome
* Hôtes vSphere dotés de ressources adéquates pour prendre en charge un dispositif VMware vCenter Server
  * Pour plus d'informations sur les ressources système requises, voir [Minimum requirements for the VMware vCenter Server 6.0 Appliance ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://kb.vmware.com/s/article/2106572){: new_window}.
* Image ISO vCSA
  <!--* In the vmware section of IBM Cloud Download Services site or vmware.com: http://downloads.service.softlayer.com/vmware/VMware-VCSA-all-6.*.iso-->
* Possibilité de monter une image ISO
* Session VPN avec accès au réseau privé IBM Cloud

**Déploiement et configuration d'un dispositif vCenter Server**

1. Montez l'image ISO du dispositif vCenter Server Appliance (vCSA).
2. Ouvrez la page vcsa-setup.html dans un navigateur compatible.
3. Passez en revue et acceptez l'installation du plug-in VMware Client Integration.
4. Cliquez sur **Allow**.
5. Cliquez sur **Install**.
6. Passez en revue et acceptez les dispositions du contrat de licence puis cliquez sur **Next**.
7. Entrez le nom de domaine qualifié complet (FQDN) ou l'adresse IP privée et les nom d'utilisateur et mot de passe de l'hôte VMware de votre choix pour installer le dispositif vCSA. Cliquez sur **Next**.
8. Cliquez sur **Yes** pour accepter l'avertissement de certificat.
9. Entrez le nom de dispositif et le mot de passe de système d'exploitation appropriés puis cliquez sur **Next**.
10. Pour le type de déploiement, sélectionnez 'Install vCenter Server with an Embedded Platform Services Controller', puis cliquez sur **Next**.
11. Cliquez sur 'Create an SSO domain' puis sur **Next**. <!-- if "create a new" is in the UI, it needs to be changed to "Create an SSO..."-->
12. Sélectionnez une taille de dispositif puis cliquez sur **Next**.
13. Sélectionnez un magasin de données puis cliquez sur **Next**.
14. Sélectionnez 'Use an embedded database (PostgreSQL)' puis cliquez sur **Next*.
15. Définissez vos configurations réseau en entrant les informations suivantes : 
  1. Network (réseau)
  * IP address Family (famille d'adresses IP)
  * Network Type (type de réseau)
  * Network Address (adresse réseau)
  * System name (nom de système)
  * Subnet mask (masque de sous-réseau)
  * Network gateway (passerelle réseau)
  * Network DNS Servers (serveurs DNS du réseau)
      * Pour plus d'informations, voir [What are Local DNS Resolvers](/docs/infrastructure/dns/dns-faq.html#what-are-the-local-dns-resolvers-).
  * Configurez la synchronisation de l'heure.
  * Cliquez sur **Next**
16. Passez en revue les paramètres puis cliquez sur **Finish**. Votre instance vCSA est mise à disposition.

