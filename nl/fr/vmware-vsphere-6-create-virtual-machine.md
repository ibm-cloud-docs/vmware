---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-10"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Création d'une machine virtuelle avec VMware vSphere 6 

1. Cliquez avec le bouton droit de la souris sur l'adresse IP de votre noeud principal dans le panneau d'inventaire de votre client vSphere.
2. Dans la fenêtre de configuration, sélectionnez **Custom**.
3. Donnez à la machine virtuelle un nom approprié puis cliquez sur **Next**.
4. Sélectionnez l'emplacement de stockage des fichiers de machine virtuelle puis cliquez sur **Next**.
* Le menu Virtual Machine Version permet d'utiliser différents types de cluster. Comme il s'agit d'un nouveau cluster et que vous n'avez pas besoin d'une prise en charge des versions antérieures, sélectionnez **Virtual Machine Version 8**. **Remarque :** Si vous utilisez le client Web pour créer un cluster, utilisez la version 11.
5. Sélectionnez le type de **système d'exploitation**.
6. Définissez le nombre de processeurs virtuels (sur la page CPUs) puis cliquez sur **Next**
  1. **Remarque :** Vous pouvez changer le nombre d'UC ultérieurement si les ressources sont disponibles. 
7. Définissez la quantité de mémoire pour la machine virtuelle. Cliquez sur **Next**
  1. **Remarque :** Vous pouvez changer la quantité de mémoire ultérieurement si les ressources sont disponibles. 
8. A la section réseau, vous devrez connecter les deux contrôleurs NIC. NIC 1 correspond au réseau privé et NIC 2 au réseau public. Le type d'adaptateur est “Flexible”. Assurez-vous que la case “Connect at Power On” (connexion à la mise sous tension) est sélectionnée. 
9. Laissez l'écran du contrôleur SCSI sur la valeur par défaut “LSI Logic Parallel”. Sur l'écran de sélection d'un disque, sélectionnez **Create a new virtual disk** (créer un disque virtuel). Conservez les valeurs par défaut des écrans **Advanced Options** et **Ready to Complete**. Votre nouvelle machine virtuelle est à présent créée. Pour commencer le chargement de votre support d'installation, cliquez sur le nom du serveur dans la liste d'inventaire puis cliquez sur **Edit Virtual machine Settings** sous Basic Tasks.
<!--* false-->
10. Avec CD/DVD Drive 1 sélectionné, sélectionnez **Connect at power** sous Device Status. Pour spécifier un fichier ISO situé dans votre magasin de données, cliquez sur **Browse**.
* Les fichiers ISO téléchargés dans le magasin de données par défaut Storage1 peuvent être sélectionnés ici. Vous voyez également les dossiers contenant les fichiers de configuration/journaux (configuration à la section Datastore de l'étape 3 du processus de création de machine virtuelle) pour toutes les machines virtuelles de serveur.
11. Une fois votre image ISO sélectionnée, vous êtes prêt à lancer le processus d'installation de votre système d'exploitation.
* Une fois votre machine virtuelle invitée opérationnelle, si la prise en charge existe, installez les outils [VMWare Tools ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://kb.vmware.com/s/article/1014294){: new_window}.
* Pour plus d'informations sur les instructions de mise en réseau, voir [Configuration d'un réseau de machines virtuelles](/docs/infrastructure/virtualization/virtual-machine-network-setup.html).
