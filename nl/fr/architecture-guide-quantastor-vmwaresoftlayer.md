---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Guide d'architecture pour QuantaStor

Vous pouvez commander et configurer la solution de stockage partagé OSNexus QuantaStor pour un environnement VMware ESXi 5. Utilisez les informations suivantes avec le manuel d'instructions [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) pour configurer l'une de ces options de stockage dans votre environnement VMware.

## Etape 1 : Commande du stockage partagé QuantaStor

Avant de passer une commande pour du stockage, vous devez déterminer les spécifications qui répondent à vos exigences en matière de capacité et d'E-S. Ces spécifications incluent, mais ne se limitent pas à, la RAM serveur, le type et le nombre d'unités de disque, les unités SSD pour la mise en cache, la configuration RAID, ainsi que la configuration du réseau. Pour plus d'informations sur le choix de la configuration QuantaStor appropriée dans votre environnement, voir [QuantaStor Solution Design Guide for Virtualization ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide#Server_Virtualization){: new_window}.

Pour l'exemple d'environnement, une configuration plus petite pouvant assurer les besoins en capacité et E-S pour les machines virtuelles est utilisée. Assurez-vous de bien comprendre quels sont les besoins en capacité et E-S de vos machines virtuelles avant de passer commande. Bien que le serveur QuantaStor soit extensible, il est important de dimensionner initialement votre matériel afin d'éviter les temps d'attente au niveau de la configuration et du déploiement.

### Commande de QuantaStor

Suivez la procédure ci-après afin de commander un serveur QuantaStor.

1. Connectez-vous au portail [{{site.data.keyword.slportal_full}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){: new_window} et cliquez sur **Compte > Passer une commande**.
2. Sélectionnez {{site.data.keyword.baremetal_short}}, Au mois dans l'écran contextuel.
3. Sélectionnez le serveur approprié avec la possibilité de stocker le nombre de disques nécessaires depuis votre environnement dans la page Liste des Serveurs. [Pour l'exemple d'environnement, un système 12 coeurs (i.e. Hex Core double) avec 12 baies d'unité est sélectionné.]
4. Entrez les options de configuration suivantes :
  * **Centre de données :** Emplacement des réseaux locaux virtuels (VLAN) et hôtes ESXi précédemment créés
  * **Serveur :** Processeur double Hex Core Xeon
  * **Mémoire RAM :** 64 Go
  * **Système d'exploitation :** OSNexus QuantaStor 3.x (4 To)
  * **Disques durs :**
    * Disques 1 et 2 : 500 Go SATA en RAID 1
    * Modèle de partition : Linux Basic
    * Disques 3 à 10 : 600 Go SAS 15K en RAID-10
  * **Bande passante publique :** Réseau privé uniquement
  * **Débits des ports de liaison montante :** 10 Gbps, liaisons montantes de réseau privé redondantes
5. Cliquez sur le bouton pour **continuer votre commande**.

**Remarque :** Le serveur de stockage est configuré avec deux interfaces réseau sans liaison afin que deux sous-réseaux différents puissent être utilisés pour équilibrer la charge de trafic à destination de la grappe de stockage.

### Fin de la configuration

Vous avez à présent un dispositif QuantaStor dans votre chariot. Vous allez donc devoir affecter les réseau local virtuel, nom d'hôte et domaine privés à l'appareil afin qu'il puisse être correctement mis à disposition. 

1. Affectez les réseaux VLAN suivants et créez des noms d'hôte pour les appareils : hôte QuantaStor – VLAN de back end : (1102 dans l'environnement)
2. Sélectionnez votre mode de règlement, acceptez les dispositions, puis cliquez sur Finaliser la commande.

**Remarque** Ne passez pas à l'étape 3 avant que le serveur ne soit à disposition et accessible via le VPN ou le serveur virtuel.

## Etape 2 : Activation de l'adaptateur logiciel iSCSI pour les hôtes de gestion et de capacité

L'adaptateur logiciel iSCSI doit être activé sur chaque hôte de gestion et de capacité, et son nom qualifié iSCSI (IQN) collecté avant le montage de volumes iSCSI. Utilisez la procédure suivante pour activer l'adaptateur logiciel iSCSI :

1. Accédez à un hôte de gestion ou de capacité ESXi et sélectionnez Manage, Storage, Storage Adapters (gérer, stockage, adaptateurs de stockage).
2. Cliquez sur le signe plus (+) de couleur verte et ajoutez l'adaptateur logiciel iSCSI.
3. Cliquez sur le vmhba qui correspond à l'adaptateur logiciel iSCSI et enregistrez le nom iSCSI (Figure 1) à la section Adapter Details une fois l'adaptateur activé.
4. Exécutez les étapes 1 à 3 pour chaque adaptateur logiciel iSCSI sur chaque hôte de gestion et de capacité ESXi.

## Etape 3 : Configuration de QuantaStor

Une fois le serveur mis à disposition, vous pouvez configurer le dispositif de stockage partagé. Plus précisément, vous configurez le réseau et des volumes iSCSI, et vous affectez des volumes à des hôtes. 

Par exemple, le volume vmk3 possède vmnic0 qui se connecte au sous-réseau privé portable A sur le réseau local virtuel de stockage. Le volume vmk4 possède vmnic2 qui se connecte au sous-réseau privé portable B sur le réseau local virtuel de stockage. Le serveur QuantaStor possède également deux adaptateurs de réseau privés, eth4 et eth6, qui se connectent au réseau local virtuel de stockage.

### Configuration du réseau

1. Ouvrez un navigateur Web et accédez à l'adresse IP de QuantaStor qui figure sur la page **Equipements** du portail [{{site.data.keyword.slportal_short}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){: new_window}.
2. Entrez le **nom d'administrateur** et le **mot de passe** (figurant à la section des mots de passe de la page **Device Details**). Avant de poursuivre, notez les appareils réseau privé qui sont utilisés par le serveur QuantaStor, par exemple eth4.
3. Accédez à **Storage System > Network Ports**.
4. Sélectionnez l'adaptateur privé qui est actif (exemple : eth4) dans la liste des adaptateurs de réseau. Cliquez avec le bouton droit de la souris et sélectionnez **Modify Network Port** dans le menu contextuel. 
5. Désélectionnez la case **iSCSI Enabled** pour désactiver les connexions iSCSI sur cet adaptateur puis cliquez sur **OK**.
6. Sélectionnez l'adaptateur privé qui n'est pas actif mais est affecté au réseau privé (exemple : eth6).
7. Cliquez avec le bouton droit de la souris sur l'adaptateur eth6 et sélectionnez **Modify Network Port** dans le menu contextuel. 
8. Sélectionnez un **type de configuration** **Static** dans l'écran **Modify Network Port**.
9. Entrez une adresse IP privée principale, un sous-réseau et une passerelle pour l'adaptateur. Utilisez une adresse de la ligne Storage si vous utilisez la feuille de travail VLAN du manuel d'instructions [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html).
10. Désélectionnez la case **iSCSI Enabled** pour désactiver les connexions iSCSI à cet adaptateur.
11. Cliquez avec le bouton droit de la souris sur l'adaptateur privé et sélectionnez **Enable Network Port** pour rendre l'adaptateur actif une fois qu'il est configuré avec une adresse IP.
12. Cliquez sur **OK** pour activer le port lors de la vérification de l'adresse IP.

### Ouverture d'un ticket de demande de service

Vous devez ouvrir un ticket de demande de service après que vous avez configuré un deuxième adaptateur avec une adresse IP privée principale. L'ouverture de ce ticket permet de s'assurer que l'adresse IP utilisée n'est pas prise si une autre machine est mise à disposition sur le VLAN.

1. Cliquez sur **Support** > **Ajouter ticket** et entrez les informations suivantes :
  * Objet : Question de réseau privé
  * Titre : Réserver et affecter une adresse IP privée
  * Associer des unités : 'Sélectionnez le serveur QuantaStor'
  * Détails : Réservation et affectation sur le réseau local virtuel. Cette adresse IP est utilisée pour le second adaptateur du serveur QuantaStor.

### Configuration de QuantaStor

A présent que la grappe peut accepter des connexions depuis les deux adaptateurs, les interfaces virtuelles de ces adaptateurs qui se trouvent sur les sous-réseaux Storage Path A et Storage Path B (chemins de stockage A et B) doivent être affectées. 

  1. Cliquez avec le bouton droit de la souris sur l'interface de l'adaptateur privé initial (eth4) et sélectionnez **Create Virtual Interface** dans le menu contextuel.
  2. Entrez l'adresse IP privée portable et le sous-réseau de l'adaptateur sur l'écran contextuel qui s'affiche, et assurez-vous que **iSCSI Enabled** est coché.
  3. Utilisez une adresse de la ligne du chemin de stockage A si vous utilisez la feuille de travail VLAN.
  4. Enregistrez l'adresse IP utilisée à la section des remarques (Notes) de la page des adresses IP portables.
  5. Sélectionnez l'interface de l'adaptateur privé initial (eth4) pour lier l'interface virtuelle puis cliquez sur **OK**.
  6. Cliquez avec le bouton droit de la souris sur l'interface de l'autre adaptateur privé (eth6) et sélectionnez **Create Virtual Interface** dans le menu contextuel.
  7. Entrez l'adresse IP privée portable et le sous-réseau de l'adaptateur et assurez-vous que **iSCSI enabled** est coché sur l'écran contextuel qui s'affiche.
  8. Utilisez une adresse de la ligne du chemin de stockage B si vous utilisez la feuille de travail VLAN.
  9. Enregistrez cette adresse IP comme utilisée à la section des remarques (Notes) de la page des adresses IP portables.
  10. Sélectionnez l'interface de l'autre adaptateur privé (eth6) pour lier l'interface virtuelle puis cliquez sur **OK**.

Une fois le serveur QuantaStor configuré avec des adresses IP et des interfaces virtuelles, vous devez configurer le routage afin de vous assurer que le trafic sortant utilise la bonne interface (car il existe deux contrôleurs NIC sur des sous-réseaux différents).

1. Utilisez SSH pour accéder au serveur QuantaStor avec vos données d'identification root et ajoutez les lignes suivantes à /etc/network/interfaces. Hypothèse : eth4 et eth6 sont les contrôleurs NIC sur le réseau privé :
  * post-up ip route add 10.0.0.0/8 via dev eth4
  * post-up ip route add 10.0.0.0/8 via dev eth6 table eth6
  * post-up ip rule add from table eth6

### Création d'un pool de stockage

Vous devez ensuite créer un pool de stockage qui sera utilisé pour allouer des volumes avant que vous ne puissiez créer des volumes et des partages.

1. Cliquez avec le bouton droit de la souris sur **Storage Pools** et sélectionnez **Create Storage Pool**.
2. Entrez les informations suivantes dans l'écran **Create Storage Pool** :
  * Nom (Name) : Entrez le nom approprié pour le pool de stockage. Exemple : StoragePool-01
  * Type de pool (Pool Type) : Valeur par défaut (zfs)
  * Profil d'E-S (I/O Profile) : Virtualisation
  * Disques à utiliser pour le pool de stockage (Disks to Utilize for the Storage Pool) : sdb
3. Cliquez sur **OK**.

Si sdb n'est pas disponible pour ajout au pool, c'est qu'il existe une partition qui est marquée comme amorçable. Vous devez utiliser gdisk sur la console de Quantastor pour retirer la partition ainsi que toute entrée /etc/fstab. Vous devrez ensuite créer des volumes pour la consommation d'ESXi.

### Création de volumes de stockage iSCSI

Vous devez créer deux volumes de stockage. Un volume est utilisé pour les machines virtuelles de gestion sur le cluster de gestion, et l'autre pour les machines du cluster de capacité. Exécutez la procédure suivante pour créer les volumes de stockage iSCSI :

1. Cliquez avec le bouton droit de la souris sur **Storage Volumes** et sélectionnez **Create Storage Volume** dans le menu contextuel. 
2. Entrez les informations pour les volumes de stockage. **Remarque :** Même si votre configuration peut différer en fonction de la charge de travail et de la capacité de stockage, l'exemple montre les valeurs du Tableau 1 et du Tableau 2 pour chaque volume de stockage.

|Zone|Valeur|
|---|---|
|Nom|Mgmt-LUN0|
|Pool de stockage|[Nom du pool de stockage configuré à l'étape précédente]|
|Taille|500 Go|
|% réservation|50|
|Compression|Activée|
{: caption="Tableau 1. Volume de gestion iSCSI" caption-side="top"}

|Zone|Valeur|
|---|---|
|Nom|Capacity-LUN0|
|Pool de stockage|[Nom du pool de stockage configuré à l'étape précédente]|
|Taille|3 To|
|% réservation|50|
|Compression|Activée|
{: caption="Tableau 2. Volume de capacité iSCSI" caption-side="top"}

### Affectation d'un accès hôte aux volumes

Vous devez configurer QuantaStor pour autoriser l'accès depuis les hôtes ESXi via le nom qualifié iSCSI de chaque hôte une fois les volumes configurés.

1. Accédez à la page d'administration de QuantaStor et cliquez avec le bouton droit de la souris sur le menu **Hosts** puis sélectionnez **Add Host**.
2. Entrez les informations suivantes dans l'écran **Add Host** :
  * Nom d'hôte (Host Name) : Entrez un nom d'hôte approprié. Le nom d'hôte ne contient pas le nom de domaine qualifié complet (FQDN), mais il doit décrire l'hôte. Exemple : MyESXiHostName
  * Type de système d'exploitation (Operating System Type) : VMware
  * Initiateur (Initator) : bouton d'option du nom qualifié iSCSI (IQN) 
  * Nom qualifié iSCSI (iSCSI Qualified Name) : IQN de l'hôte correspondant.
3. Cliquez sur **OK**.

Suivez cette procédure pour chaque hôte de gestion et de capacité de l'environnement ESXi.

Après avoir ajouté chaque hôte dans les clusters de gestion et de capacité, procédez comme suit :

1. Cliquez avec le bouton droit de la souris sur le menu **Host Groups** et sélectionnez **Create Host Group…**.
2. Entrez 'ManagementCluster' dans la zone **Name** et sélectionnez tous les hôtes faisant partie du cluster de gestion.
3. Cliquez sur **OK**. Un groupe d'hôtes sera créé que vous pourrez affecter à un volume particulier. 

Répétez cette procédure pour le cluster de capacité.

1. Cliquez sur le menu **Storage Volumes**.
2. Cliquez avec le bouton droit de la souris sur le volume **Mgmt-Lun0** et sélectionnez **Assign/Unassign Host Access**.
3. Vérifiez que **Mgmt-Lun0** est une option du menu déroulant et sélectionnez le groupe d'hôtes que vous avez créé à l'étape précédente. Cette option permet à chaque hôte ESXi du cluster de gestion d'accéder au volume Mgmt-Lun0. Procédez de même pour **Capacity-LUN0**

## Etape 4 : Montage du ou des volumes sur les clusters de gestion/capacité

Connectez-vous au client Web vSphere et accédez à **Hosts** sous **vCenter Inventory Lists**.

Utilisez la procédure suivante pour monter le volume sur les hôtes ESXi :

1. Sélectionnez un hôte et cliquez sur **Manage, Storage,** > **Storage Adapters**.
2. Sélectionnez **Targets** > **Dynamic Discovery** > **Add…**.
3. Entrez l'adresse IP affectée au dispositif de stockage QuantaStor sur le chemin de stockage A de l'écran **Add Send Target Server**.
4. Laissez **3260** comme port et cliquez sur **OK**.
5. Cliquez sur **Dynamic Discovery** > **Add…**. Répétez les étapes 4 et 5 pour le chemin de stockage B.

L'hôte ESXI est prêt à réanalyser l'adaptateur logiciel iSCSI pour détecter le volume Mgmt-Lun0.

1. Sélectionnez l'icône **Rescan Storage Adapters** (Figure 9) sur l'écran **Storage Adapters**.
2. Laissez l'option par défaut sur l'écran contextuel qui s'affiche et cliquez sur **OK**.
3. Cliquez sur **Actions, New Datastore** une fois le volume détecté et formatez-le en tant que **VMFS-5**.
4. Vérifiez que le formatage a abouti puis cliquez sur **Storage Devices, Device Details, Edit Multipathing…**.
5. Sélectionnez **Round Robin** pour la politique de sélection de chemin d'accès (**Path Selection Policy**) et cliquez sur **OK**.

A présent que le volume Mgmt-Lun0 est connecté à un hôte unique, vous devez revenir aux autres hôtes de gestion du cluster et répéter le processus d'ajout du volume. Toutefois, vous n'aurez pas besoin de formater le volume puisqu'il l'est déjà (VMFS-5) et est affiché comme tel après la reconnaissance.

## Etape 5: Désactivation de l'accusé de réception retardé sur les hôtes vSphere ESXi

L'accusé de réception retardé (delayed ACK) doit être désactivé une fois les unités logiques de stockage connectées aux hôtes de gestion et de capacité.

1. Accédez à l'environnement vSphere et sélectionnez **Storage Adapters** > **iSCSI Software Adapter** > **Advanced Options**.
2. Cliquez sur **Edit** et faites défiler jusqu'à la fin l'écran des options avancées. 
3. Décochez la case **DelayedAck** puis cliquez sur **OK**.

Pour plus d'informations sur le "delayed ACK" concernant VMware, voir la [base de connaissances VMware](https://kb.vmware.com/s/article/1002598).

Vous pouvez à présent revenir au manuel d'instructions [Advanced Single-Site VMware Reference Architecture](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) et terminer la configuration de l'environnement.
