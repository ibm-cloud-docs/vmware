---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation à VMware vSphere 6 

Utilisez les informations suivantes pour débuter avec vSphere 6.

## Maîtrise de l'environnement et de la configuration

Afin d'optimiser votre solution VMware, il est recommandé d'utiliser un VLAN de réseau privé et public (facultatif, le port public peut être désactivé si inutile) pour votre environnement VMware vSphere. Ce profil de mise à disposition autorise les limitations de trafic de segment de couche 2 suivantes :

|Exemple d'ID VLAN|Description|Type|Détails complémentaires|
|---|---|---|---|
|VLAN1 - **1101**|Gestion, VxLAN|BCR privé|VLAN natif sans balise, VLAN natif d'origine sur lequel sont déployés les hôtes VMWare au moment de la commande|
|VLAN4 - **2200**|Zone démilitarisée d'accès Internet public|FCR public|VLAN natif sans balise, VLAN natif d'origine sur lequel sont déployés les hôtes VMWare au moment de la commande|
{: caption="Tableau 1. Exemples de réseau local virtuel privé et public" caption-side="top"}

## Validation de votre commande de serveurs vSphere
1. Connectez-vous au portail [{{site.data.keyword.slportal_full}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){: new_window}.
2. Cliquez sur **Compte > Passer une commande**.
3. A la section **Serveur bare metal**, cliquez sur **Au mois**.
4. Sélectionnez les serveurs. Consultez les publications du support VMware pour connaître la configuration minimale requise.
  * Les serveurs suivants ont été sélectionnés pour l'exemple. **Remarque :** Disposer de liaisons montantes doubles publiques et privées sans liaison constitue une exigence pour la redondance. Confirmez que le centre de données dans lequel vous avez créé vos réseaux locaux virtuels possède des liaisons montantes sans liaison. 
  * Cluster de capacité (quantité : 2)
    * Configuration de serveur : Sélectionnez un serveur Intel Xeon v3 à la section 'Serveurs multicoeurs biprocesseurs'
    * Logiciel : système d'exploitation = vSphere Enterprise Plus 6
    * Stockage OS : 2 x 1 To SATA (configuré en tant que RAID 1)
    * Stockage des données : il est recommandé de commander 2 To SATA ou 1,2 To SSD ou du stockage Endurance / Performance NFS SAN
      * Si vous êtes intéressé par d'autres types de stockage, voir [Stockage à utiliser avec les systèmes VMware](select-storage-option-use-vmware.html)
      * Vitesses de port de liaison montante : 1 Gbps réseaux public et privé doubles (sans liaison)
        * Les liaisons montantes 10 Gbps sont recommandées pour les solutions VMware vSAN
5. Si vous créez un déploiement dans un nouveau centre de données IBM Cloud, passez à l'étape 6. S'il s'agit d'une extension ou d'un déploiement dans un centre de données existant, sélectionnez vos VLAN BCR de back end + VLAN FCR frontal préférés. Pour l'exemple, le VLAN BCR de back end est 1101 et celui FCR frontal  est 2200. **Remarque :** S'il s'agit d'un nouveau déploiement ou d'un nouveau déploiement dans un nouveau centre de données, les VLAN BCR de back end et FCR frontal sont créés lorsque vous commandez le serveur.
6. Entrez un **Nom d'hôte** et un **Domaine**.
7. Passez en revue la commande puis cliquez sur **Finaliser la commande** pour lancer le processus de mise à disposition.

## Validation de la commande pour vCenter Server

vCenter est un module complémentaire pour un serveur Windows. Cette configuration peut augmenter jusqu'à 20 hôtes vSphere. Pour des implémentations de plus grande taille, ou pour le déploiement du dispositif vCenter Server Appliance (VCSA), [déployer et configurer un dispositif vCenter Server Appliance (vCSA)](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html) directement sur un cluster vSphere est recommandé.

Utilisez la procédure suivante pour commander un serveur virtuel avec vCenter installé :

1. Connectez-vous au portail {{site.data.keyword.slportal_short}}.
2. Cliquez sur **Compte > Passer une commande**.
3. Commandez une instance de noeud public/privé de serveur virtuel ou bare metal **Au mois** sous Serveurs virtuels.
  1. Pour qu'une instance de serveur virtuel SoftLayer soit qualifiée pour vCenter 6.0, vous devez déployer sur au moins **4 coeurs x 2,0 GHz** et **4 Go de RAM**
  2. Pour connaître la liste des recommandations de déploiement vCenter, voir le manuel [VMware vCenter Server&trade; 6.0 Deployment Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.vmware.com/files/pdf/techpaper/vmware-vcenter-server6-deployment-guide.pdf){: new_window}.
4. Entrez les informations suivantes :
  * En fonction de la configuration de serveur minimale recommandée
    * Configuration de coeurs vCPU : 4 coeurs x 2,0 GHz
    * Configuration de mémoire RAM : 12 Go
    * Logiciel : système d'exploitation = Windows Server 2012 R2 Standard Edition (64 bits)
    * Module complémentaire spécifique au système d'exploitation : vCenter 6
    * Premier disque : 1 x 100 Go (SAN)
    * Second disque : 1 x 50 Go (SAN)
    * Vitesses de port de liaison montante : 1 Gbps, liaisons montantes de réseau privé et public

5. S'il s'agit d'un nouveau déploiement sur un nouveau centre de données IBM Cloud, passez à l'étape 6 ci-dessous. S'il s'agit d'une extension ou d'un déploiement dans un centre de données existant, sélectionnez vos VLAN BCR de back end + VLAN FCR frontal préférés. Pour notre exemple, le VLAN BCR de back end est 1101 et celui FCR frontal  est 2200. (S'il s'agit d'un déploiement entièrement nouveau ou d'un nouveau déploiement dans un nouveau centre de données, les VLAN BCR de back end et FCR frontal sont créés lorsque vous commandez le serveur)
6. Entrez un **Nom d'hôte** et un **Domaine**.
7. Passez en revue la commande puis cliquez sur **Finaliser la commande** pour lancer le processus de mise à disposition.

## Commande de sous-réseaux public et privés portables/adresses IP portables

**Remarque :** Ne continuez pas la procédure si des réseaux locaux virtuels n'ont pas été totalement mis à disposition.

Les sous-réseaux sont utilisés pour traiter le trafic des machines virtuelles invitées VMware et le trafic du noyau hôte VMware.

1. Depuis le portail de contrôle, cliquez sur **Réseau > Gestion IP > Sous-réseaux**.
2. Cliquez sur **Commander des adresses IP** dans la partie supérieure droite de l'écran.
3. Sélectionnez **Privé Portable**.
4. Sélectionnez le réseau local virtuel approprié (exemple : bcr01.wdc04: 1101)
5. Cliquez sur **Continuer**.
6. Complétez le formulaire **Commander des adresses IP**.
7. Cliquez sur **Commander des adresses IP** dans la partie supérieure droite de l'écran.
8. Cliquez sur **Valider la commande**.
9. Suivez cette procédure pour chaque VLAN applicable (par exemple, 1101, 2200)
  1. Pour plus d'informations sur les réseaux locaux virtuels (VLAN), voir la rubrique d'[initiation aux réseaux VLAN](/docs/infrastructure/vlans/getting-started.html).

|Type de sous-réseau|Taille de sous-réseau|VLAN lié|Utilisation hôte vSphere|
|---|---|---|---|
|Portable - Privé|Adresse /27 32|**1101**|Machines virtuelles de gestion|
|Portable - Privé|Adresse /27 32|**1101**|Ports noyau machine virtuelle pour iSCSI et vMotion|
|Portable - Privé|Adresse /27 32|**1101**|IP privées pour machine virtuelle invitée|
|Portable - Public|Adresse /27 32|**2200**|IP publiques pour machines virtuelles invitées (facultatif)|
{: caption="Tableau 2. Sous-réseaux" caption-side="top"}

### Facultatif – Désactivation de l'interface publique sur l'hôte vSphere

Vous pouvez désactiver les interfaces publiques de vSphere à des fins de sécurité, si vous ne prévoyez pas de les utiliser.

1. Depuis le portail de contrôle, cliquez sur **Equipements > Liste des unités**.
2. Cliquez sur le nom de votre hôte vSphere.
3. Cliquez sur le tableau Configuration et faites défiler jusqu'à la section Réseau.
4. Sélectionnez **Déconnecter** pour chaque hôte vSphere applicable, paire eth1 et eth3 pour tous les hôtes.

Cette opération peut également être effectuée via [{{site.data.keyword.slapi_full}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://sldn.softlayer.com/reference/service/SoftLayer_Hardware_Server/shutdownPublicPort){: new_window}.

## Création et configuration de cluster de centre de données vSphere <!-- create and configure should be separate tasks-->

Vous pouvez à présent vous connecter à vCenter Server et configurer le cluster vSphere.

1. Depuis le portail de contrôle, cliquez sur **Equipements > Liste des unités**.
2. Recherchez votre dispositif vCenter et cliquez sur son nom.
3. Faites défiler l'écran **Détails de l'unité** jusqu'à la section **Réseau** du serveur et notez l'**Adresse IP privée**.
4. Faites défiler l'écran **Détails de l'unité** et notez les **mots de passe** du système d'exploitation Windows et du logiciel vCenter.
5. Ouvrez une session Bureau à distance Microsoft et connectez-vous à votre serveur vCenter Server via son adresse IP publique.
6. Connectez-vous à l'aide des mots de passe que vous vous êtes procuré à l'étape 4. **Remarque :** Une connexion VPN active à IBM Cloud devra être en place si l'adresse IP privée est utilisée pour accéder à vCenter. Pour plus d'informations sur l'accès au VPN, voir [Activer l'accès au réseau privé de l'infrastructure IBM Cloud](/docs/customer-portal/getting-started.html#enable-private-network).
7. Téléchargez et installez le [client vSphere ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=2089791){: new_window} classique, ou utilisez le client Web de vSphere via le lien `https://<vCenter-Sever-Public-IP-Address>/vsphere-client/`.
8. connectez-vous à vCenter avec l'adresse IP et les mots de passe obtenus aux étapes 3 et 4. 
9. Cliquez avec le bouton droit de la souris sur ne nom de serveur vCenter dans le panneau de gauche, puis sélectionnez **New Datacenter**.
10. Entrez un nom approprié pour le centre de données.
11. Cliquez avec le bouton droit de la souris sur le centre de données et sélectionnez **New Cluster**.
12. Entrez un nom de cluster. N'activez PAS Cluster Features, vSphere HA ou vSphere DRS pour le moment.
13. Cliquez sur **Next**.
14. Laissez **EVC** désactivé et cliquez sur **Next**.
15. Acceptez les valeurs par défaut pour stocker le fichier d'échange dans le même répertoire que la machine virtuelle (_default to store the swapfile in the same directory as the virtual machine_) puis cliquez sur **Next**.
16. Cliquez sur **Finish** pour terminer la création du cluster.
17. Cliquez avec le bouton droit de la souris sur le cluster que vous venez de créer et sélectionnez **Add Host**.
18. Entrez l'adresse IP ou le nom d'hôte de l'un des hôtes vSphere puis indiquez **Root** dans la zone **Username**, ainsi que le mot de passe de l'hôte dans la zone **Password**.
19. Cliquez sur **Next** pour les écrans Host Summary, Assign License, Lockdown Mode, puis cliquez sur **Finish** pour terminer l'ajout de votre hôte au cluster.
20. Répétez les étapes 18 et 19 pour chaque hôte vSphere de votre cluster. Une fois que vous avez terminé, les différents hôtes vSphere figurent sous le nouveau cluster.

### Configuration de la construction réseau de base pour les hôtes vSphere

Utilisez la procédure suivante pour configurer la construction de base pour les hôtes vSphere de votre cluster.

1. Sélectionnez le premier hôte vSphere et cliquez sur l'onglet **Configuration**.
2. A la section **Hardware**, sélectionnez **Networking**. Vous devriez déjà avoir vSwitch0 avec vmnic0 ; cliquez sur **Properties** en regarde de vSwitch0.
3. Sélectionnez **Network Adapters** dans la fenêtre **vSwitch Properties** puis cliquez sur le bouton **Add**.
4. Sélectionnez vmnic2 pour l'ajouter à vSwitch0 puis cliquez sur **Next**.
5. Assurez-vous que les deux vmnic sont des **adaptateurs actifs** puis cliquez sur **Next**.
6. Cliquez sur **Finish**.
7. Cliquez sur l'onglet **Ports** et vérifiez que vSwitch est mis en évidence, puis cliquez sur **Edit**.
8. Cliquez sur l'onglet **General** et remplacez la valeur de **MTU** par 9000 (trame Jumbo).
9. Cliquez sur l'onglet **NIC Teaming** et remplacez l'équilibrage de charge par **Route Based on IP hash** puis cliquez sur **OK**.
10. Utilisez les étapes 1 à 8 pour configurer les vmnic pour les autres hôtes vSphere de votre cluster.

Vous devez à présent ajouter un groupe de ports pour vMotion. Ce groupe peut être créé en tant que commutateur standard virtuel (VSS, Virtual Standard Switch) ou commutateur distribué virtuel (VDS, Virtual Distributed Switch). Pour les besoins de notre exemple, nous allons créer un commutateur VSS.

1. Sélectionnez l'onglet **Configuration** puis sélectionnez **Networking**.
2. Cliquez sur **Properties...** pour vSwitch0.
3. Cliquez sur **Add...** pour créer un groupe de ports.
4. Sélectionnez **VMkernel** et cliquez sur **Next**.
5. Renseignez les propriétés du groupe de ports à l'aide des informations suivantes :
  * **Network Label :** nom approprié pour le groupe de ports.
  * **VLAN ID (Optional) :** ID VLAN pour le trafic vMotion (1101 dans notre exemple). L'ID VLAN permet d'autoriser VMware à baliser le trafic pour le réseau local virtuel spécifique.
  * Sélectionnez **Use this port group for vMotion**.
6. Cliquez sur **Next**.
7. Indiquez une **adresse IP portable** pour le réseau local virtuel. (Vous pouvez obtenir cette adresse IP de port depuis le portail SoftLayer : **Réseau > Gestion IP > VLAN**. Sélectionnez le réseau local virtuel approprié et, sous **Sous-réseaux** vous verrez une plage d'adresses IP portables. Si nous ne disposez pas d'adresse IP portable ou si vous avez épuisé le pool en cours, suivez la procédure de la section 'Commander des Adresses IP/sous-réseaux privés' pour commander des adresses IP portables supplémentaires<
8. Cliquez sur **Next** puis sur **Finish** pour terminer.

Utilisez la procédure suivante pour créer un groupe de ports pour le trafic de données de machines virtuelles.

1. Cliquez sur **Properties...** pour vSwitch0 et sélectionnez **Add, Virtual Machine**.
2. Renseignez **Port Group Properties** à l'aide des informations suivantes : 
  * **Network Label :** entrez le nom du groupe de ports, par exemple VM Data
  * **VLAN ID (Optional) :** indiquez un ID VLAN ; nous avons utilisé 1101 dans notre exemple. L'ID VLAN permet à VMware de baliser le trafic pour le réseau local virtuel.

### Facultatif - Installation de licences VMware de modules complémentaires (NSX, vRealize, vSAN, etc.)

L'environnement VMware est désormais actif et vous êtes prêt à poursuivre avec le déploiement de configurations supplémentaires, machines virtuelles invités ou modules complémentaires VMware. Les licences des modules complémentaires VMware peuvent également être achetés via le portail de contrôle IBM Cloud et ajoutées via la console vCenter. Pour plus d'informations sur la commande et la gestion des licences de modules complémentaires VMware, voir [VMware vSphere 6 - Commande et gestion des licences](vmware-vsphere-6-ordering-and-managing-licenses.html).

## Etapes suivantes
Vous disposez à présent d'un environnement VMware de base sur site unique s'exécutant dans un centre de données IBM Cloud. La configuration de base comporte seulement un magasin de données local, ce qui en fait une configuration simplifiée qui ne possède pas des fonctions telles que VMware DRS, HA (haute disponibilité), Storage DRS, ou un pare-feu.

Pour plus d'informations, voir [Foire aux questions : VMware](vmware-faq.html). 
