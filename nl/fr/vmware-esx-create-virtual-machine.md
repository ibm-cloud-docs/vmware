---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Création d'une machine virtuelle VMware ESX
{: #create-esx-vm}

Pour créer une machine virtuelle, suivez cette procédure.
{:shortdesc}

1. Cliquez avec le bouton droit de la souris sur l'adresse IP de votre noeud principal dans le panneau d'inventaire de votre client vSphere.
2. Sélectionnez **Custom** (personnaliser) dans la fenêtre de configuration.
3. Donnez à la machine virtuelle un nom approprié puis cliquez sur **Next**.
4. Sélectionnez l'emplacement de stockage des fichiers de machine virtuelle puis cliquez sur **Next**.
5. Depuis **Virtual Machine Version**, sélectionnez **Virtual Machine Version 8**. <!-- since we are using vSphere instead of the Web Client to create it (in which case we would use version 11 instead).-->
6. Sélectionnez le système d'exploitation (**Operating System**).
7. Sélectionnez le nombre de processeurs virtuels (**CPU page**) ainsi que la quantité de **mémoire** que vous souhaitez pour créer la machine virtuelle. **Remarque :** Vous pouvez changer le nombre de processeurs et la quantité de mémoire ultérieurement si les ressources sont disponibles. A la section réseau, vous devrez connecter deux contrôleurs NIC, NIC 1 étant le réseau privé et NIC 2 le réseau public. Ce type d'adaptateur sera “Flexible”. Assurez-vous que l'option connexion à la mise sous tension (**Connect at Power On**) est sélectionnée.
8. Gardez l'écran du **contrôleur SCSI** sur la valeur par défaut “LSI Logic Parallel”. Sur l'écran de **sélection d'un disque**, sélectionnez **Create a new virtual disk** (créer un disque virtuel). Les valeurs par défaut des écrans **Advanced Options** et **Ready to Complete** doivent également être conservées. La création d'une machine virtuelle est à présent terminée.  

Pour commencer le chargement de votre support d'installation, cliquez sur le nom du serveur dans la liste d'inventaire. Cliquez ensuite sur **Edit Virtual machine Settings** (éditer les paramètres de la machine virtuelle) sous **Basic Tasks** (tâches de base).

9. Avec **CD/DVD Drive 1** sélectionné, cochez la case **Connect at power** sous Device Status. Pour spécifier un fichier ISO situé dans votre magasin de données, cliquez sur **Browse**.
10. Les fichiers ISO téléchargés dans le magasin de données par défaut Storage1 peuvent être sélectionnés ici. Vous voyez également les dossiers contenant les fichiers de configuration/journaux (configuration à la section **Datastore** de l'étape 3 du processus de création de machine virtuelle) pour toutes les machines virtuelles de serveur.

Une fois votre image ISO sélectionnée, vous êtes prêt à lancer le processus d'installation de votre système d'exploitation.

Pour plus d'informations sur la configuration d'un réseau de machines virtuelles, voir [Configuration d'un réseau de machines virtuelles](/docs/infrastructure/virtualization/virtual-machine-network-setup.html){:new_window}.
