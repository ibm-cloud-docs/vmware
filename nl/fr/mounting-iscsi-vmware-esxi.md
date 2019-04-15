---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Montage d'iSCSI VMWare ESXi
{: #mount-iscsi-esxi}

Le montage d'iSCSI dans VMWare ESXi peut être accompli avec quelques étapes et les seuls détails du serveur et du noeud de stockage.
{:shortdesc}

1. Connectez-vous à vSphere à l'aide de l'IP privée principale et des utilisateur **root** et mot de passe.
* Depuis la page d'accueil, cliquez sur l'onglet **Configuration**.
* Cliquez sur **Storage Adapters** puis sur **Add…**.
* Cliquez sur **OK** pour ajouter l'adaptateur logiciel iSCSI.
* Confirmez en cliquant sur **OK**.
* Après actualisation, vous voyez le nouvel adaptateur iSCSI dans la liste.
* Cliquez sur **Properties** dans le panneau inférieur.
* Depuis la fenêtre Properties, cliquez sur **Configure** vers le bas de la fenêtre et définissez **Name** sur le nom qualifié iSCSI (IQN) du serveur (information figurant sur la page du dispositif de stockage, sous les hôtes autorisés).
* Cliquez sur l'onglet **Dynamic Discovery** puis cliquez sur **Add...**.
* Le serveur iSCSI sera l'IP cible du dispositif de stockage. Cliquez ensuite sur le bouton **CHAP...**.
* Sélectionnez **Use CHAP** et décochez **Inherit from Parent**. Entrez le **nom d'utilisateur** (information figurant sur la page du dispositif de stockage, sous les hôtes autorisés) et le mot de passe correspondant.
* Sélectionnez **Do not use CHAP** sous la section Mutual CHAP puis cliquez sur **OK**.
* Le dispositif figure à présent dans la fenêtre Dynamic Discovery. Cliquez sur **Close**.
* Confirmez la réanalyse des dispositifs de stockage.
* Vous verrez ensuite le dispositif au bas de la page, en grisé et avec l'indication 'unmounted'.
* Cliquez avec le bouton droit de la souris sur le nom du dispositif et sélectionnez **attach**.
* Cliquez sur le menu **Datastore** situé dans la colonne de gauche, puis cliquez sur **add storage** et sélectionnez **Disc/LUN**.
* Cliquez sur le dispositif avec l'indication 'iqn'.
* Sélectionnez la version de système de fichiers de votre choix et cliquez sur **next**, puis continuez à suivre l'assistant.
* Une fois l'assistant terminé, vous pouvez utiliser l'interface iSCSI selon les besoins, via l'hôte ou les machines virtuelles que vous créez.



La procédure de connexion d'un dispositif Data Transfer Service iSCSI est similaire, si ce n'est que vous devez obtenir le nom qualifié iSCSI (IQN) du serveur. Vous allez exécuter la procédure suivante depuis la console ESXi :

Pour commencer, vous avez besoin d'une unité :

`esxcfg-scsidevs -a | grep iSCSI`

Vous devrez ensuite obtenir le nom qualifié iSCSI (dans le cas présent, vmhba33 est l'unité iSCSI) : 

`vmkiscsi-tool -I -l vmhba33`
