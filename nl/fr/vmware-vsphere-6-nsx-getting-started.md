---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-14"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Initiation à VMware vSphere 6 NSX 

NSX est déployé en tant qu'autorisation de licence pour être appliqué à votre infrastructure. {{site.data.keyword.BluSoftlayer_full}} fournit les licences sur une base par processeur (la tarification ne change pas pour le nombre de coeurs par UC). Une licence NSX est obligatoire pour chaque serveur qui utilise un composant NSX (Management (gestion), Control (contrôle) ou Data Plane (plan de données)). NSX ajoute des fonctions réseau supplémentaires à la plateforme. Vous pouvez créer un réseau dissocié robuste pour la sécurité système, la segmentation des locataires et les environnements cloud hybrides qui étendent les fournisseurs ou les extensions à partir de clouds privés sur site.
{:shortdesc}

Vous pouvez ajouter des pare-feux, équilibrage de charge, VPN, services NAT, segmentation micro basée VXLAN à votre environnement avec prise en charge pour l'automatisation via une API RESTful.

## Ajout de licences
Les licences sont ajoutées aux serveurs via le processus suivant :
1. Connectez-vous à vCenter Server à l'aide du client vSphere.
* Sous **Administration**, cliquez sur **Licensing**.
* Cliquez sur **Solutions**.
* Dans la liste des produits, cliquez sur **VMware NSX for vSphere**.
* Cliquez sur **License Key** ou **Enter New license key**.
* Cliquez sur **OK**.

## Installation de NSX

1. Déployez NSX Manager.
* Enregistrez NSX Manager auprès de vCenter Server.
* Le client Web vSphere déploie les instances de contrôleur NSX via NSX Manager.
* Préparez les hôtes vSphere en utilisant le gestionnaire NSX Manager pour installer les VIB (vSphere Installation Bundle) sur les hôtes du cluster.
* Une fois les contrôleurs NSX déployés sur l'ensemble des hôtes applicables, définissez et configurez les composants NSX tels que les passerelles Edge Gateway, équilibreurs de charge et pare-feux.

## Considérations relatives au déploiement

L'activation de NSX pour une solution requiert l'utilisation de noeuds vSphere supplémentaires par rapport aux noeuds de traitement standard.

**NSX Manager**<br />
IBM Informix Virtual Appliance on Management Cluster possède une relation 1:1 avec vCenter. Les fonctions vSphere de haute disponibilité classiques sont recommandées. NSX Manager inclut des fonctions de sauvegarde planifiée/à la demande et requiert une connectivité IP avec vCenter, le contrôleur, les ressources NSX Edge et les hôtes ESXi. NSX Manager est déployé sur le même sous-réseau/VLAN que vCenter, mais cela n'est pas strictement obligatoire. Dimensionnement typique de machine virtuelle :

|Edition NSX|vCPU|Mémoire|Disque OS|
|---|---|---|---|
|6.2 Small|4|12 Go|60 Go|
|6.2 Default|4|16 Go|60 Go|
|6.2 Large Scale|4|24 Go|60 Go|
{: caption="Tableau 1. Dimensionnement classique de machine virtuelle par NSX Manager" caption-side="top"}

**Noeuds de contrôleur NSX**<br />
Des noeuds de contrôleur NSX sont déployés en tant que dispositifs virtuels depuis l'interface utilisateur du gestionnaire NSX Manager. Chaque dispositif communique via une adresse IP distincte qui se trouve généralement sur le même sous-réseau que le gestionnaire, mais ceci ne constitue pas une obligation matérielle. Il est recommandé de déployer au moins trois machines virtuelles de contrôleur sur au moins trois noeuds vSphere physiques distincts. Celles-ci agissent comme active-active-active avec la délinéation de travail définie par NSX Manager. En cas de défaillance d'un noeud, une reprise des "règles majoritaires" a lieu afin de redistribuer la charge de travail sur les contrôleurs restants. NSX n'applique pas de manière native cette pratique de conception. Vous pouvez utiliser les règles vSphere natives de non-affinité pour éviter de déployer plus d'un noeud de contrôleur sur le même serveur ESXi. Le dimensionnement typique par machine virtuelle est le suivant :

|Machines virtuelles de contrôleur|vCPU|Réservation|Mémoire|Disque OS|
|---|---|---|---|---|
|3|4|2048 Mhz|4 Go|20 Go|
{: caption="Tableau 2. Dimensionnement classique de machine virtuelle de contrôleur NSX" caption-side="top"}

**Commutateur NSX**
Un commutateur distribué virtuel (VDS) mis à niveau est déployé sur l'ensemble des hôtes afin d'implémenter des fonctions distribuées.

**Passerelle de service NSX Edge Services Gateway**<br />
Déployée en tant que dispositifs de machine virtuelle multi-fonction selon les besoins dans l'environnement. A des fins de routage uniquement, un cluster actif comportant jusqu'à huit passerelles peut être déployé. Pour tout autre service, déployé dans un déploiement actif-en attente. Les communications externes à l'environnement des machines virtuelles requièrent l'affectation, par IBM Cloud, d'adresses IP portables afin d'inclure les pools NAT, VIP et noeuds finaux de réseau privé virtuel.

|Format de passerelle|vCPU|Mémoire|Usage spécifique|
|---|---|---|---|
|X-Large|6|8 Go|Convient pour : LB haute performance L7|
|Quad-Large|4|1 Go|Convient pour : déploiement FW et ECMP haute performance|
|Large|2|1 Go|Small DC & service unique|
|Compact|1|512 Mo|Petits déploiements ou utilisation de service unique ou PoC|
{: caption="Tableau 3. Services NSX Edge" caption-side="top"}

