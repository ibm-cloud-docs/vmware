---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Commande de licences VMware

Les administrateurs VMware comprennent qu'ils peuvent rapidement atteindre les caractéristiques de cloud hybride abordables via un déploiement dans {{site.data.keyword.BluSoftlayer_full}}. L'une des caractéristiques est que les charges de travail et catalogues vSphere sont mis à disposition dans les environnements VMware vSphere au sein de centres de données {{site.data.keyword.cloud_notm}} sans modifications des machines virtuelles ou invités VMware. L'utilisation d'un hyperviseur vSphere et d'une plateforme de gestion/orchestration communs rendent ces déploiements possibles.
{:shortdesc}

L'implémentation de vSphere active également l'utilisation d'autres composants. Le Tableau 1 comporte une liste de produits VMware disponibles à la commande via le portail client {{site.data.keyword.slportal}}. Les informations de tarification sont disponibles sous [IBM Cloud for VMware Solutions](http://www.softlayer.com/vmware-solutions).

|Nom du produit|
|---|
|VMware vCenter Server Standard|
|VMware vSphere Enterprise Plus|
|VMware vRealize Operations Enterprise Edition|
|VMware vRealize Automation Enterprise|
|VMware vRealize Automation Advanced|
|VMware NSX-V|
|VMware Integrated OpenStack (VIO)|
|Virtual SAN Standard Tier 1 (0 - 20 To)|
|Virtual SAN Standard Tier 2 (21 - 64 To)|
|Virtual SAN Standard Tier 3 (65 - 124 To)|
|VMware Site Recovery Manager (SRM)|
{: caption="Tableau 1. Produits VMware disponibles sur le portail client" caption-side="top"}

Utilisez la procédure suivante pour commander des licences pour les produits VMware figurant dans le tableau 1 :
1. Connectez-vous au portail [{{site.data.keyword.slportal_short}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://control.softlayer.com/){: new_window}.
2. Cliquez sur **Equipements > Gérer > Licences VMware**. 
3. Cliquez sur **Commander des licences VMware** dans le coin supérieur droit.
4. Cliquez sur la liste déroulante sous **Ajouter une licence...** pour afficher la liste des produits VMware et du nombre d'UC pour les licences que vous souhaitez commander.
  * **Remarque :** VMware vSphere Enterprise Plus (ESXi 6.0) ne peut pas être commandé via cette procédure. Ce produit est commandé en tant que système d'exploitation demandé lorsque vous commandez votre serveur bare metal. 
5. Vous pouvez voir le prix du produit VMware sélectionné à l'extrême droite de l'écran.
6. Cliquez sur **Continuer** pour commander les licences, ou bien cliquez sur **Ajouter une licence** pour ajouter d'autres licences.
  * Lorsque vous cliquez sur **Continuer**, vous êtes ramené à la page **Licences VMware**, qui affiche vos produits et clés de licence VMware.
7. Téléchargez les **fichiers d'installation** à partir du lien fourni. Vous devez disposer d'une connexion SSL au réseau privé IBM Cloud pour accéder à la page de téléchargement.
8. Téléchargez les produits VMware appropriés puis installez-les manuellement dans votre environnement vSphere.
