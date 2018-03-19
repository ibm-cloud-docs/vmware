---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-30"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilisation de manuels d'instructions pour des déploiements VMware

Les administrateurs VMware peuvent rapidement mettre au point des caractéristiques cloud hybride abordables via un déploiement sur le cloud global {{site.data.keyword.BluSoftlayer_full}} de niveau entreprise. Les charges de travail et catalogues vSphere peuvent être mis à disposition dans des environnements VMware vSphere au sein de centres de données {{site.data.keyword.cloud_notm}} sans avoir à modifier de machine virtuelle ou d'invité VMware. Ces déploiements sont rendus possibles par l'utilisation d'un hyperviseur vSphere et d'une plateforme de gestion/orchestration communs. Des implémentations vSphere peuvent également optimiser d'autres composants de la suite VMware vCloud Suite – vCloud Automation Center, vCenter Operations Management Suite, vSAN, vCloud Network & Security, Site Recovery Manager, vCenter Orchestrator, et NSX.

L'objectif principal de la série de manuels d'instructions VMware est d'aider les administrateurs vSphere pour le déploiement d'environnements VMware vSphere au sein d'une infrastructure IBM Cloud. Ces manuels ne sont pas destinés à vous former à l'administration de vSphere. Pour plus d'informations sur l'administration de vSphere, voir [VMware Education ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://mylearn.vmware.com/mgrreg/index.cfm){: new_window}.

{{site.data.keyword.cloud_notm}} possède plusieurs fonctions spécifiques qui fournissent aux administrateurs VMware la flexibilité de consommer des instances et du réseau bare metal, du stockage, ainsi que des constructions de sauvegarde et reprise en libre-service. Vous pouvez utiliser ces éléments pour déployer des implémentations de vSphere pleinement fonctionnelles, ce qui peut permettre d'étendre ou de remplacer des implémentations sur site (VMware@Home).

Les manuels d'instructions suivants sont disponibles pour les administrateurs :

* [Build a Single Site VMware Environment](/docs/infrastructure/virtualization/advanced-single-site-vmware-reference-architecturesoftlayer.html) : En tant qu'administrateur vSphere, vous êtes guidé tout au long de la procédure de génération de votre environnement, notamment pour l'utilisation du stockage par blocs de type Endurance ou Performance ou de QuantaStor.
* [Migrate vSphere Workloads ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_Migrating%20Workloads_v1%200.pdf){: new_window} : Scénarios destinés à vous aider à migrer des charges de travail [machines virtuelles (VM)] vers VMware après déploiement de votre implémentation vSphere sur un centre de données IBM Cloud.
* [Leverage NSX® ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wpc.c320.edgecastcdn.net/00C320/VMware_at_SoftLayer_CookBook_NSX_v1.1.pdf){: new_window} : Vous pouvez optimiser VMware NSX afin de fournir des constructions de mise en réseau définie par logiciel (SDN) pour les déploiements VMware@SoftLayer.
* [Catalogic ECX ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wpc.c320.edgecastcdn.net/00C320/CatalogicECX@SoftLayer_CDM.pdf){: new_window} : Vous pouvez gérer et analyser CopyData dans une infrastructure informatique hybride. Cette infrastructure est déployée sur l'infrastructure IBM Cloud via la plateforme intelligente Copy Data Management de Catalogic Software, ECX, et en utilisant NetApp Private Storage et l'infrastructure VMware vSphere.
* [VMware Back Up ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_BURA_v1%201.pdf){: new_window} : Ce manuel d'instructions décrit des approches alternatives à la sauvegarde, la récupération et l'archivage de charges de travail (machines virtuelles) basées VMware qui s'exécutent dans un déploiement VMware.
* [VMware Disaster Recovery ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wpc.c320.edgecastcdn.net/00C320/VMware@SoftLayer_DR.pdf){: new_window} : Ce manuel d'instructions détaille deux cas d'utilisation établissant une solution de reprise après incident via VMware. La première s'associe à un environnement VMware sur site qui permet la récupération d'une charge sur site ou vice-versa. La seconde récupère des charges de travail VMware sur un second centre de données {{site.data.keyword.cloud_notm}}.
* [Vormetric Encryption of VMware ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wpc.c320.edgecastcdn.net/00C320/VMware@Softlayer%20Vormetric%20Encryption%20v1.2.pdf){: new_window} : Cas d'utilisation illustrant la façon dont Vormetric protège les charges de travail VMware en chiffrant les données de machine virtuelle.
* [Deploy a trusted cloud solution with IBM, VMware, and HyTrust ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wpc.c320.edgecastcdn.net/00C320/DeploymentGuide_IBM_Intel_HyTrust_VMware_v1%200.pdf){: new_window} : Vous pouvez intégrer les différents éléments d'architecture pour créer une chaîne sécurisée depuis le matériel jusqu'à l'hyperviseur et aux applications de gestion.


**Remarque :** Les manuels d'instructions sont destinés à des administrateurs vSphere expérimentés. Certains de sujets traités partent du principe que le lecteur possède les compétences de base en matière de déploiement pour installer et configurer vSphere et vCenter.
