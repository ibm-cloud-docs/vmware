---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#  Migration et mise à niveau vers VMware vSphere 6

Développez ou déplacez vos environnements cloud VMware vers un centre de données {{site.data.keyword.BluSoftlayer_full}} rapidement et simplement en utilisant le panneau de commande de gestion VMware. Pour migrer et mettre à niveau des charges de travail vSphere, servez-vous de la procédure suivante comme d'un guide.
{:shortdesc}

1. Collectez vos données.
2. Passez en revue l'architecture existante :
  1. Utilisation des ressources (UC/mémoire/stockage).
  2. Suivi et taux de croissance des projets.
  3. Identification des projets à venir.
  4. Détermination des VLAN/sous-réseaux/etc. affectés qui sont déployés (disponibles dans le portail de contrôle).
  5. Recherche des sous-réseaux RFC1918 (privés) auto-définis utilisés pour la solution.
3. Consultez la documentation VMWare 6 et rejoignez les communautés VMWare :
  1. [Documentation VMware vSphere ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.vmware.com/nl/VMware-vSphere/index.html){: new_window}
  2. [VMware Technology Network  ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://communities.vmware.com/welcome){: new_window}
4. Mettez à jour la formation de votre équipe d'administrateurs pour la prise en charge de VMWare 6.
5. Planifiez et concevez une nouvelle architecture.
6. Sélectionnez un [centre de données ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud-computing/bluemix/data-centers){: new_window} basé sur la conformité. Travaillez avec le service commercial d'IBM Cloud pour affiner votre recherche d'emplacement candidat en fonction de la disponibilité et des produits/services.
7. Définissez les VLAN et sous-réseaux requis (IP privées et publiques portables).
8. Mettez au point les serveurs vSphere :
  1. Passez en revue le catalogue de serveurs IBM Cloud actuel. Les serveurs Intel Xeon v3 sont recommandés en association à des liaisons montantes redondantes, des blocs d'alimentation redondants et RAID-1 pour les disques locaux (d'amorçage).
  2. La plupart des clients disposant de VMWare respectent un plafond de capacité physique de N+1 (toutes les machines virtuelles peuvent être allouées facilement aux serveurs avec un noeud unique en moins (dédié à la maintenance, aux pannes, etc.). 
  3. De nombreux clients souhaitent un "plafond logiciel" plus élevé d'environ 80 % (capacité de 80 % sur la configuration de 'n' serveurs) par rapport au plus classique 60-75 % en raison de l'exécution courte de calcul.
  4. L'octroi de licence de système d'exploitation externe (Microsoft, Red Hat, par exemple) peut être nécessaire pour les invités vSphere depuis un fournisseur externe.
  5. Reportez-vous au document sur les meilleures pratiques [Performance Best Practices for VMware vSphere 6.0 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.vmware.com/files/pdf/techpaper/VMware-PerfBest-Practices-vSphere6-0.pdf){: new_window}
9. Mettez au point le serveur vCenter :
  1. En règle générale, une instance de serveur virtuel (VSI) de taille moyenne sert de point d'entrée aux petits environnements (8 vCPU + 16 Go RAM). En revanche, une solution non virtualisée (bare metal) sera utilisée pour les environnements plus grands.
  2. vCenter peut être déployé sur une machine virtuelle Windows VSI autonome en tant que module complémentaire de système d'exploitation ou en tant qu'appliance.
    1. Liens de référence :
        * [vCenter Server 6.0 requirements for installation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://kb.vmware.com/s/article/2107948){: new_window}
        * [VMware vCenter Server Performance and Best Practices ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.vmware.com/files/pdf/techpaper/vmware-vCenter6-perf.pdf){: new_window}
        * [Déploiement et configuration d'un dispositif vCSA (vCenter Server Appliance) avec VMware vSphere 6](vmware-vsphere-6-deploy-and-configure-vcenter-server-appliance-vcsa.html)
10. Serveurs non VMWare : Identifiez et planifiez les serveurs non VMWare (virtuels ou bare metal) qui peuvent être nécessaires, et adaptez votre plan en conséquence.
11. Stockage :
  1. Développez un plan de stockage pour l'environnement. 2 IOPS/Go d'endurance avec un espace d'image instantanée pour la virtualisation constitue un bon plan de stockage pour commencer, mais si des bases de données virtuelles ou d'autres applications haute performance sont utilisées, alors le niveau 4 IOPS/Go sera mieux adapté. Le stockage NFS est généralement recommandé.  
  2. Pour savoir quelle matrice de sélection utiliser, voir [Stockage à utiliser avec les systèmes VMware](select-storage-option-use-vmware.html).
  3. L'espace d'image instantanée est surtout utilisé comme mesure secondaire en cas de restaurations par point de cohérence. 10 % constitue une taille satisfaisante pour commencer car le processus est particulièrement efficace et peut être aisément redimensionné. 
12. Sauvegardes :
  1. Assurez-vous que la stratégie de sauvegarde existante fonctionne. Si aucune stratégie de sauvegarde n'existe, il faut en créer une.
  2. Vous pouvez utiliser votre propre solution de sauvegarde. Vous pouvez utiliser les fonctions de sauvegarde incluses avec la licence vSphere Enterprise Plus, des solutions tierces optimisées telles que VEEAM, ou des sauvegardes r1soft IBM Cloud traditionnelles.
13. Développez une stratégie de migration :
  1. Reportez-vous au document sur les meilleures pratiques [Best practices to install or upgrade to ESXi 6.0 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://kb.vmware.com/s/article/2109712){: new_window}.
  2. Passez en revue les configuration de DNS et/ou IP existantes et raccourcissez les durée de vie selon les besoins.
  3. Développez un plan pour les machines virtuelles afin d'inclure les hôte source et de destination, les IP source et de destination, ainsi que les entrées DNS associées.
  4. Dans la plupart des scénarios, il est préférable de migrer les machines virtuelles une à une puis de mettre à jour les configurations de réseau privé et public. Lorsque vous passer de versions plus anciennes à des versions plus récentes, il est généralement conseillé de simplement "copier et expédier" la machine virtuelle en l'arrêtant et en effectuant une opération de _déconnexion/connexion_ entre les environnements. Si vous passez d'un emplacement à un autre, un vMotion longue distance est possible.
  5. Développez des plans de test pour la vérification de l'environnement.
  6. Mettez en place une fenêtre de changement/maintenance avec les utilisateurs. Des fenêtres individuelles de maintenance de machine virtuelle peuvent s'appliquer pour le transfert de données, la configuration de la machine virtuelle, le changement et la propagation du DNS, ainsi que du temps consacré au traitement des incidents.
14. Déployez le nouvel environnement :
  1. [Initiation à VMware vSphere 6](vmware-vsphere-6-getting-started.html).
  2. Commandez les nouveaux serveurs vSphere et vCenter (ainsi que tout autre serveur nécessaire).
      **Remarque :** Assurez-vous que les liaisons montantes réseau "sans liaison" appropriées sont sélectionnées. 
  3. Commandez et configurez le stockage approprié : [Guide d'architecture pour IBM File Storage for IBM Cloud with VMware](/docs/infrastructure/FileStorage/architecture-guide-file-storage-vmware.html)
  4. Commandez les nouveaux réseaux locaux virtuels (VLAN) et sous-réseaux portables (des diagrammes d'architecture détaillés et des justifications peuvent être requis).
  5. Configurez vCenter pour la communication avec les serveurs vSphere et la configuration de l'environnement.
  6. Effectuez des sauvegardes dans l'environnement de production.
  7. Exécutez les plan de migration et les plans de test associés.
  8. Implémentez les sauvegardes dans le nouvel environnement. 
  9. Faites fonctionner le nouvel environnement. 
  10. Mettez l'environnement existant hors service. 
