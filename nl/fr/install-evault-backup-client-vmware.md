---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Installation du client EVault Backup pour VMware

L'installation du client de sauvegarde EVault Backup sur un serveur VMware peut être effectuée via une série de commandes dans le shell ou le terminal du serveur ESX cible. Cette procédure expose les étapes requises pour installer le client EVault Backup sur votre serveur VMware :
{:shortdesc}

Pour installer l'agent, téléchargez et copiez le package `Agent-VMware-ESX-Server-6.71.<version-info>.tar.gz` sur le serveur ESX cible à l'aide de la commande suivante :

`wget -N http://downloads.service.softlayer.com/evault/archive/Agent-VMware-ESX-Server-6.71.2105.tar.gz`

**Remarque :** Vous devez effectuer la procédure suivante en local, sur le serveur ESX cible.

1. Extrayez les fichiers du package. Pour ce faire, utilisez la commande suivante (où “PACKAGENAME” pourrait être “Agent-VMware-ESX-Server-6.71”) :<br/>`tar xvfz PACKAGENAME.tar.gz`
2. Accédez au répertoire dans lequel vous avez extrait le package.
3. Exécutez le script d'installation :<br />`# ./install.sh`<br/><br/>
**Remarque :**  Le script d'installation vous invite à fournir des informations de configuration telles que l'enregistrement Web (adresse, numéro de port et authentification) et le nom de fichier journal.

Entrez le nom d'utilisateur WebCC pour ce serveur.

4. Entrez le nom d'utilisateur **EVault Backup Username** à l'invite demandant le nom d'utilisateur WebCC. Reportez-vous à la procédure [Afficher les détails du stockage de sauvegarde EVault](/docs/infrastructure/Backup/index.html#viewing-evault-backup-storage-details-in-ibm-cloud-infrastructure-customer-portal) pour les instructions d'affichage du nom d'utilisateur EVault Backup.
5. Entrez le mot de passe EVault Backup à l'invite demandant le mot de passe WebCC.
6. Une fois l'installation terminée, un message d'achèvement s'affiche et le démon d'agent s'exécute.


Autres remarques relatives à l'installation :<br/>
Le journal d'installation se trouve dans le répertoire d'installation si l'installation aboutit.<br/>
Par exemple  : `/opt/BUAgent/Install.log`

En cas d'échec et d'annulation de l'installation, le journal d'installation se trouve dans le répertoire `<Installation Failure directory>.`<br/>
Si l'installation échoue mais n'est pas annulée, le journal d'installation se trouve dans le répertoire `<Installation Kit directory>`.<br/>
<!-- For more information, you are able to download the User Guide at: http://downloads.service.softlayer.com/evault/Documentation/VMware_Agent_User_Guide.pdf<br/>-->
Assurez-vous d'être connecté au VPN {{site.data.keyword.BluSoftlayer_full}} pour afficher le lien ci-dessus. Pour plus d'informations sur la connexion au VPN IBM Cloud, voir [Activer l'accès au réseau privé de l'infrastructure IBM Cloud](/docs/customer-portal/getting-started.html#enable-private-network).
