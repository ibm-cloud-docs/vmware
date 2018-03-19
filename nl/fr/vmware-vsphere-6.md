---
copyright:
  years: 1994, 2017
lastupdated: "2017-08-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Options de licence VMware 

Les administrateurs VMware peuvent rapidement mettre au point des caractéristiques cloud hybride abordables via un déploiement sur un cloud global {{site.data.keyword.BluSoftlayer_full}} de niveau entreprise. Facteur clé de différenciation {{site.data.keyword.BluSoftlayer_notm}}, les charges de travail et catalogues vSphere peuvent être mis à disposition dans l'environnement VMware vSphere au sein de centres de données {{site.data.keyword.BluSoftlayer_notm}} sans modifications des machines virtuelles ou invités VMware. Ces déploiements sont rendus possibles par l'utilisation d'un hyperviseur vSphere et d'une plateforme de gestion/orchestration communs.

Outre l'offre de licence vSphere 6 Enterprise Plus License, {{site.data.keyword.BluSoftlayer_notm}} propose chaque mois l'octroi de licences mensuelles pour vCenter, NSX, vRealize, vSAN et Site Recovery Manager (SRM).

## VMware vSphere

**Utilisation prévue :** plateforme OS de virtualisation de serveur bare metal qui extrait les ressources de processeur, mémoire, stockage et réseau afin de créer plusieurs serveurs virtuels sur un serveur physique unique. Plusieurs serveurs physiques peuvent être mis en cluster afin de créer un cloud privé. 

**Interface utilisateur :** clients vCenter, API VMware, interface CLI VMware

**Fonctionnalités :**
* Migration active vMotion
* Haute disponibilité
* Tolérance aux pannes
* Réplication
* Virtualisation Nvidia GRID vGPU 
* Optimisation de la capacité de charge de travail
* Planificateur DRS (Distributed Resources Scheduler)
* Allocation dynamique
* Contrôle des E-S réseau

## VMware vCenter

**Utilisation prévue :** centraliser la gestion des ressources de calcul pour chaque hôte vSphere. Si les hôtes vSphere peuvent être gérés de manière individuelle, le fait de les placer sous le contrôle vCenter active les fonctionnalités suivantes :

**Interface utilisateur :** client Web, client lourd, API VMware, interface CLI VMware

**Fonctionnalités :**
* Contrôle centralisé et visibilité pour tous les aspects des hôtes vSphere gérés et des machines virtuelles invitées.
* Fournit un panneau unique de vue d'interface via le client Web vCenter pour le réseau de calcul et la gestion du stockage.
* Optimisation proactive. Active l'allocation et l'optimisation des ressources pour une efficience maximale sur les hôtes vSphere.
* Fonction de gestion étendue pour d'autres modules complémentaires intégrés tels que NSX, vRealize, vSAN et Site Recovery Manager (SRM).
* Surveillance, alerte, planification. Les administrateurs de cloud peuvent afficher des événements et des alertes dans le client Web vCenter, ainsi que configurer des actions planifiées.
* Moteur d'automatisation. vCenter est le moteur qui exécute les tâches qui lui sont envoyées via l'interface Web d'API vSphere. VMware vRealize Automation et vRealize Orchestration sont des exemples d'applications menant des actions vCenter via l'API VMware.

## VMware NSX

**Utilisation prévue :** NSX fournit des fonctions SDN (mise en réseau définie par logiciel) cruciales pour la prise en charge des opérations de plateforme cloud.

**Interface utilisateur :** clients vCenter, API VMware, interface CLI VMware

**Fonctionnalités :**
* Equilibrage de charge
* Pare-feux
* Routage
* Commutateurs logiques
* Réseau privé virtuel
* Segmentation VxLAN/Points d'extrémité du tunnel

## VMware vRealize

**Utilisation prévue :** La suite VMware vRealize Suite est une plateforme de gestion cloud prête pour un usage en entreprise, que vous pouvez utiliser pour gérer un cloud hybride hétérogène. 

**Interface utilisateur :** clients vCenter, API VMware, interface CLI VMware

**Modèle de licence :** par processeur par mois

**Fonctionnalités :**
* vRealize Automation : distribution automatisée d'infrastructure, d'applications et de services informatiques personnalisés
* vRealize Operations : orchestration intelligente de la gestion de la santé, des performances, de la capacité et des configurations
* vRealize Log Insight : gestion des journaux en temps réel et analyse de journal

## VMware vSAN

**Utilisation prévue :** VMware vSAN est une technologie de stockage distribué qui active des unités de stockage local sur chaque hôte vSphere pour être agrégées et mises en pool sur une unité de stockage non-partagée qui est accessible à l'ensemble des hôtes d'un cluster vSAN.

**Interface utilisateur :** clients vCenter, API VMware, interface CLI VMware

**Fonctionnalités :**
* Stockage basé sur des hôtes distribués
* Architecture non-partagée (Shared-nothing)
* Augmentation jusqu'à 64 noeuds
* Faible temps d'attente
* Tolérance aux pannes configurable

## VMware Site Recovery Manager (SRM)

**Utilisation prévue :** VMware Site Recovery Manager (SRM) active la disponibilité et la mobilité des applications sur des sites se trouvant dans des environnements cloud privés. En profitant pleinement de l'encapsulation et de l'isolement des machines virtuelles, Site Recovery Manager active l'automatisation simplifiée de la reprise après incident afin de répondre aux objectifs de temps de reprise (RTO). SRM permet également de réduire les coûts associés aux plans de continuité des opérations, et d'atteindre des résultats prévisibles à faible risque pour la reprise d'un environnement virtuel.

**Interface utilisateur :** clients vCenter, API VMware, interface CLI VMware

**Fonctionnalités :**
* Test de reprise sans interruption
* Flux de travaux d'orchestration automatisés
* Reprise automatisée des paramètres de réseau et de sécurité
* Extensibilité pour l'automatisation personnalisée
* Orchestration de cross-vCenter vMotion
* Plans de reprise après incident centralisés
* Gestion basée sur des règles
