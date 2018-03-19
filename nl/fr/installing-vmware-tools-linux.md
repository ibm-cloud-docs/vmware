---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-07"
---

# Installation de VMware Tools - Linux

VMware Tools est une suite d'utilitaires permettant d'améliorer les performances du système d'exploitation invité de la machine virtuelle et d'améliorer la gestion de la machine virtuelle. L'installation de VMware Tools dans le système d'exploitation invité est essentielle. Bien que le système d'exploitation invité puisse s'exécuter sans VMware Tools, vous perdez une fonctionnalité essentielle et l'aspect pratique.

Le service est nommé `vmware-guestd` sur les systèmes invités Linux, FreeBSD et Solaris. Le service `vmware-guestd` effectue les tâches suivantes au sein du système d'exploitation invité :

* Transmet les messages du système d'exploitation hôte au système d'exploitation invité.
* Exécute des commandes sur le système d'exploitation afin d'arrêter ou de redémarrer proprement un système Linux, FreeBSD ou Solaris lorsque vous sélectionnez des opérations d'alimentation sur le poste de travail.
* Synchronise l'heure du système d'exploitation invité avec celle du système d'exploitation hôte.
* Exécute des scripts permettant d'automatiser les opérations du système d'exploitation invité. Ces scripts s'exécutent lors du changement d'état d'alimentation de la machine virtuelle.

Le service démarre quand le système d'exploitation invité démarre.

Pour installer VMware Tools sur un serveur Linux, cliquez avec le bouton droit de la souris sur le serveur approprié dans votre client vSphere, survolez **Guest** et cliquez sur **Install/Upgrade VMware Tools**.

Ce lien monte une unité virtuelle de CD-ROM qui contient le fichier rpm des outils VMware Tools. Pour installer les outils après avoir monté l'unité virtuelle de CD-ROM, procédez comme suit :
1. Montez l'unité de CD-ROM en utilisant la commande `mount /dev/cdrom /mnt`.
2. Vérifiez que le fichier existe et est correctement monté en utilisant la commande `ls /mnt` sur le répertoire de montage. Vous verrez le fichier `VMWareTools-4.0.0-208167.i386.rpm`. 
3. Exécutez la commande `rpm –ivh /mnt/VMWareTools-4.0.0-208167.i386.rpm`.
4. Exécutez la commande suivante pour configurer VMware Tools pour le noyau d'exécution : `/usr/bin/vmware-config-tools.pl`. **Remarque :** Vous êtes invité à appuyer sur la touche **ENTREE** une fois à mi-parcours des mises à jour de configuration.
<!--Follow the on screen prompts and run the following command to complete the installation. commented out because there is no command shown in which to run--> 
**Remarque :** Il n'est pas nécessaire de redémarrer la machine virtuelle après l'installation des outils VMware Tools, mais cette opération est cependant recommandée.

Si les outils VMware Tools ont été correctement installés, “OK” s'affiche dans votre interface client vSphere.
