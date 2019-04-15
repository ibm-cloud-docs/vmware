---
copyright:
  years: 1994, 2017
lastupdated: "2017-11-20"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# Stockage à utiliser avec les systèmes VMware
{: #vmware-storage}

Vous disposez de plusieurs options quand vient la question du stockage. Il peut s'agir de stockage privé, partagé, ou bien de solutions de stockage propres. Utilisez les informations suivantes pour vous aider à déterminer la solution la mieux adaptée à votre charge de travail.

Le Tableau 1 répertorie les niveaux de stockage ainsi que le type de charge de travail correspondant.
<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tableau 1. Niveaux de stockage</caption>
	<tbody>
		<tr>
			<td style="width:160px;">
				<p>&nbsp;</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Niveau 1</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Niveau 2</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Niveau 3</strong></p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Utilisation professionnelle</strong></p>
			</td>
			<td style="width:160px;">
				<p>Applications, bases de données et données de production hautes performances et/ou à haute disponibilité</p>
			</td>
			<td style="width:160px;">
				<p>Application, bases de données et données de test et développement non-indispensables à la mission</p>
			</td>
			<td style="width:160px;">
				<p>stockage, sauvegarde et archivage de données non-indispensables à la mission</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Performances</strong></p>
			</td>
			<td style="width:160px;">
				<p>Elevées (SSD, SAS)</p>
			</td>
			<td style="width:160px;">
				<p>Moyennes (SAS, SATA)</p>
			</td>
			<td style="width:160px;">
				<p>Faibles (SATA)</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Opérations d'E-S/s garanties</strong></p>
			</td>
			<td style="width:160px;">
				<p>Oui</p>
			</td>
			<td style="width:160px;">
				<p>Non</p>
			</td>
			<td style="width:160px;">
				<p>Non</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Haute disponibilité (HA)</strong></p>
			</td>
			<td style="width:160px;">
				<p>Oui</p>
			</td>
			<td style="width:160px;">
				<p>Non</p>
			</td>
			<td style="width:160px;">
				<p>Non</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Réplication</strong></p>
			</td>
			<td style="width:160px;">
				<p>Oui</p>
			</td>
			<td style="width:160px;">
				<p>Oui</p>
			</td>
			<td style="width:160px;">
				<p>Non</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:160px;">
				<p><strong>Instantanés</strong></p>
			</td>
			<td style="width:160px;">
				<p>Oui</p>
			</td>
			<td style="width:160px;">
				<p>Non</p>
			</td>
			<td style="width:160px;">
				<p>Non</p>
			</td>
		</tr>
	</tbody>
</table>


## Options de stockage privé et partagé VMware

Plusieurs options de stockage s'offrent à vous. Pour le stockage privé, vous pouvez choisir des options de disque local, VSAN ou QuantaStor. Pour le stockage partagé, vous pouvez sélectionner le stockage de type Endurance ou Performance. Si vous optez pour votre propre stockage, il existe plusieurs options “privées”, notamment NetApp OnTap Edge, NetApp Private Storage (NPS), {{site.data.keyword.IBM}} Spectrum Accelerate, ainsi que le stockage défini par logiciel. Dans un souci de commodité, le Tableau 2 et le Tableau 3 fournissent une comparaison côte à côte des options. 

## Options de stockage privé

Il existe plusieurs options de stockage pour la connexion à VMware dans un environnement à service exclusif : 

* Local
* vSAN
* QuantaStor
* NetApp Data OnTap Edge
* NPS
* IBM Spectrum Accelerate

<a name="Local"></a>
## Stockage local

Commandez {{site.data.keyword.baremetal_short}} depuis le portail client IBM Cloud avec ESX et sélectionnez les disques souhaités [SATA, SA SCSI ou SSD].
 
Vous pouvez utiliser votre propre licence ESX, mais vous devez ouvrir un ticket auprès du support afin de les informer du changement.

* Charges de travail recommandées : Niveau 3
* Performances : limitées, dépendent du niveau RAID et du type de disque. Les unités SSD impliquent une augmentation de coûts pour de meilleures performances.
* Evolutivité : limitée au nombre d'emplacements d'unité sur le châssis
* Protocoles : non applicable
* Coût : faibles frais d'investissement (CAPEX) et dépenses opérationnelles (OPEX)
* Haute disponibilité : non disponible
* Réplication : [vSphere Replication Virtual Appliance ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Fiabilité : plusieurs points de défaillance uniques



## vSAN [1]

* Charges de travail recommandées : Niveau 1
* Performances : 90K+ IOPS par hôte selon la configuration hôte
* Evolutivité : VMDK version 5.5 jusqu'à 2 To, VMDK version 6.0 jusqu'à 62 To. Ajoutez des noeuds supplémentaires.
* Protocoles : propriétaires
* Coût : moyen pour les frais d'investissement et les dépenses opérationnelles
* Haute disponibilité : prise en charge pour les défaillances de disque et d'hôte. Les domaines de défaillance sont pris en charge à compter de la version 6 de VMware.
* Réplication : [vSphere Replication Virtual Appliance ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://pubs.vmware.com/srm-51/index.jsp?topic=%2Fcom.vmware.srm.install_config.doc%2FGUID-E654F2D8-7D56-4A81-9568-E85172A7022D.html){: new_window}
* Réplication et reprise après incident :
    1. Planifier une sauvegarde de machine virtuelle via VMware vCenter Server
    2. Créer un instantané de machine virtuelle
    3. Data DE créé pour la machine virtuelle
    4. Restaurer la machine virtuelle
 * Fiabilité : tolère jusqu'à trois défaillances d'hôte pour au moins sept hôtes. Les domaines de défaillance ont été introduits à la version 6 de VMware.   

[1] Une nouvelle fonction de vSan 6.2, les clusters étendus, permet aux hôtes de se trouver sur différents pods du même centre de données (tests de validation en cours). <!-- Should this in progress mention be removed? -->

vSAN 5.5 est disponible uniquement avec une licence de type BYOL (Bring Your Own License, licence à fournir). Cette version est prise en charge par VMware uniquement si vous utilisez un contrôleur de disques Avago LSI MegaRAID SAS 9361-8i. 

vSAN 6.0 est disponible directement sur le portail IBM Cloud avec une base de facturation par licence d'UC.

## QuantaStor

Le manuel [OSNexus Solution Design Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://wiki.osnexus.com/index.php?title=Solution_Design_Guide){: new_window} peut être utilisé comme aide pour connecter VMware avec QuantaStor.

* Charges de travail recommandées : Niveaux 2 et 3 
* Performances:  variables en fonction du nombres d'unités, du niveau RAID et de l'utilisation des disques (iSCSI ou NFS)  
* Evolutivité : la version 3 châssis unique prend en charge 128 To ; aucun ajout ou augmentation. 
* Protocoles : iSCSI, NFS et SMB 
* Coût : élevé pour les frais d'investissement et les dépenses opérationnelles 
* Haute disponibilité : non disponible  
* Réplication : fonctions de réplication intégrées ; pas de SRA disponible. Possibilité d'utiliser le dispositif vSphere Replication Appliance 
* Fiabilité : point de défaillance unique pour le boîtier et le contrôleur RAID.


<a name="NetApp"></a>
## NetApp Data OnTap Edge

Vous devez acheter un appareil NetApp auprès de NetApp ou d'IBM. Vous devez l'installer sur un {{site.data.keyword.baremetal_short}} de votre centre de données {{site.data.keyword.BluSoftlayer}}.

Pour plus d'informations sur la connexion de VMware avec NetApp, visitez les liens suivants :
* [NetApp ONTAP Select ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.netapp.com/us/products/platform-os/data-ontap-edge/index.aspx){: new_window}
* [Data ONTAP Edge: Build a data center on a server with NetApp fundamentals ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.netapp.com/us/media/ds-data-ontap-edge.pdf){: new_window}

* Charges de travail recommandées : Niveaux 2 et 3
* Performances : variables en fonction du nombre d'unités et du niveau RAID
* Evolutivité : prend en charge 110 To ; pas d'ajout.
* Protocoles : iSCSI, NFS et SMB
* Coût : moyen pour les frais d'investissement et les dépenses opérationnelles
* Haute disponibilité : non disponible
* Réplication : prend en charge SnapMirror ; également réalisable via [vRealize Automation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.vmware.com/products/vrealize-automation){: new_window} (vRA).
* Fiabilité : point de défaillance unique pour le boîtier et le contrôleur RAID.

<a name="NPS"></a>
## Stockage privé NetApp

Vous devez acheter un appareil NetApp auprès de NetApp ou d'IBM. Vous devez l'installer sur l'un des sites de collocation à proximité de votre centre de données IBM Cloud et le connecter à l'aide de la solution Direct Link Colocation ou Direct Link Cloud.

Pour plus d'informations sur la connexion de VMware avec NetApp, visitez les liens suivants : 
* [NetApp Private Storage for IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* [Solution brief: NetApp Private Storage for IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.netapp.com/us/media/ds-3619_tcm10-127472.pdf){: new_window}


* Charges de travail recommandées : Niveau 1
* Performances : dépend du modèle NetApp
* Evolutivité : prend en charge l'ajout d'unités et de châssis pour accroître la capacité et les opérations d'E-S par seconde (IOPS)
* Protocoles : iSCSI, NFS et SMB
* Coût : élevé pour les frais d'investissement et les dépenses opérationnelles
* Haute disponibilité : têtes et contrôleurs doubles
* Réplication : prend en charge SnapVault et SnapMirror ; également réalisable via [vRealize Automation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.vmware.com/products/vrealize-automation).
* Fiabilité : haute redondance et prise en charge des E-S multi-accès (MPIO)

<a name="IBM"></a>
## IBM Spectrum Accelerate

L'option de stockage privé IBM Spectrum Accelerate n'est pas disponible sur le portail client IBM Cloud. <!-- Click here for the instructions on how to build the offering. *commented out because there is no link -->

* Charges de travail recommandées : Niveau 1
* Performances : dépend du nombre de disques, d'unités SSD (facultatif), et de la quantité de mémoire accordée à la machine virtuelle de chaque “noeud”.
* Evolutivité : Echelles ~8 - 325 To utilisables
  * Capacité minimale : 3 machines virtuelles x 6 unités
  * Capacité maximale : 15 machines virtuelles x 12 unités
  * Augmente jusqu'à 144 grappes virtuelles et plus de 40 Po utilisables via IBM Hyper-Scale Manager
  * Extension de capacité sans interruption par l'ajout de noeuds supplémentaires
  * Prise en charge d'unité SSD de 1 x 500 ou 800 Go par noeud
* Protocoles : iSCSI uniquement
* Coût : dépend du modèle de tarification et des machines physiques déployées pour les noeuds ; frais d'investissement élevés, dépenses opérationnelles moyennes à faibles selon les licences
  * Tarification par binaire (Tio) de capacité utilisable
  * N'est pas lié à une configuration matérielle spécifique. Exemple : une licence 200 Tio peut être déployée de différentes façons – une instance 200 Tio, deux instances 100 Tio, ou quatre instances 50 Tio
  * Deux types de licence proposés : licence permanente [inclut un an d'abonnement et de service (S&S)] et licence mensuelle (inclut S&S)
* Haute disponibilité : solution en cluster
* Réplication : réalisable via [vRealize Automation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.vmware.com/products/vrealize-automation){: new_window}
 ou SRA, qui peut être utilisé pour une réplication depuis un système IBM XIV physique avec le gestionnaire VMware Site Recovery Manager (SRM)
  * [vSphere Replication ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.vmware.com/products/vsphere/replication.html){: new_window}
  * [VMware vCenter Site Recovery Manager version 5.x guidelines for IBM XIV Gen3 Storage System ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www-356.ibm.com/partnerworld/wps/servlet/ContentHandler/stg_ast_sto_wp_vmware_vcenter_recovery_gen3){: new_window}
* Fiabilité : haute redondance et prise en charge des E-S multi-accès (MPIO). Tout noeud disponible peut gérer le cluster. Les fonctions suivantes ne sont actuellement pas prises en charge par IBM Spectrum Accelerate sur les systèmes matériels IBM XIV:
  * Mise en miroir sur trois sites
  * IBM Hyper-Scale Mobility (iSCSI)
  * USG version 6
  * Unités de disque de 6 To
  * Norme Storage Management Initiative Specification (SMI-S) 1.6
  * Chiffrement des données au repos
  * Licence vStorage for API Array Integration (VAAI) désormais alignée sur les volumes virtuels (VVol)
  * vCenter Operations Manager (VCop)
  * Pour plus d'informations sur le système de stockage IBM XIV Storage System, voir [Platform and application integration for IBM XIV Storage System ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www-01.ibm.com/support/knowledgecenter/STJTAG/hsg/hsg_kcwelcomepage_xiv.html){: new_window}

## Options de stockage partagé

Il existe deux options de stockage que vous pouvez utiliser pour vous connecter à VMware dans un environnement multilocataire : le stockage par blocs et le stockage de fichiers.

### Stockage par blocs et de fichiers

Commandez le {{site.data.keyword.baremetal_short}} depuis le portail client IBM Cloud avec ESX.

Dans VMware, trois valeurs prédéfinies <!--**Authorize** (**Block** or **File**) **Storage SoftLayer** --> sont fournies dans l'onglet **Host Device Details Storage** – Username, Password (pour l'authentification CHAP) et Host IQN.

Pour plus d'informations sur la mise à disposition de stockage par blocs, voir [Mise à disposition et gestion du stockage par blocs](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Pour plus d'informations sur la mise à disposition de stockage de fichiers, voir [Mise à disposition et gestion d'IBM File Storage for IBM Cloud](/docs/infrastructure/FileStorage/provisioning-file-storage.html).

* Charges de travail recommandées : Niveaux 1, 2 et 3
* Deux façons d'optimiser les performances :
    1. Niveaux IOPS Endurance : disponible en 0,25, 2, 4 ou 104 IOPS par Go
    2. IOPS allouées aux performances : indiquez les opérations d'entrée-sortie par seconde indépendamment de la capacité. Recommandé pour les charges de travail avec des exigences de performance bien définies.
    * Paramètres de performance de stockage prévisible
    * Plusieurs volumes peuvent être segmentés afin d'atteindre des niveaux IOPS plus élevés et davantage de capacité de traitement
* temps d'attente <10 ms jusqu'à 48 000 IOPS
* Evolutivité : commander entre 20 Go et 12 To. Vous ne pouvez pas redimensionner le volume une fois celui-ci commandé.
* Protocoles : iSCSI et NFS
* Coût : élevé pour les frais d'investissement (10x pour un réseau SAN de même taille) et les dépenses opérationnelles
* Haute disponibilité : têtes et contrôleurs doubles
* Réplication : instantané et réplication fournis via le réseau privé IBM Cloud ; également réalisable via [vRealize Automation ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.vmware.com/products/vrealize-automation){: new_window}, mais pas SRA.
* Fiabilité : haute redondance ; iSCSI utilise une connexion E-S multi-accès (MPIO) ; le stockage basé NFS est routé via des connexions TCP/IP. Instantané et réplication activés.

Le tableau 2 répertorie les avantages et inconvénients du stockage privé dans un environnement à service exclusif.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tableau 2. Options de stockage privé VMware - Pour et Contre</caption>
	<tbody>
		<tr>
			<td colspan="7" style="width:638px;">
				<p><strong>VMware &ndash; Stockage privé (à service exclusif)</strong></p>
			</td>
		</tr>
		<tr>
			<td rowspan="2" style="width:101px;">
				<p><strong>Facteurs clé / option de stockage</strong></p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:87px;">
				<p>Local</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:95px;">
				<p>SAN virtuel</p>
			</td>
			<td bgcolor="#C6D9F1" rowspan="2" style="width:99px;">
				<p>QuantaStor</p>
			</td>
			<td bgcolor="#C6D9F1" colspan="2" style="width:159px;">
				<p align="center">NetApp</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p>IBM Spectrum Accelerate</p>
			</td>
		</tr>
		<tr>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>OnTap Edge</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:80px;">
				<p>NPS</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:96px;">
				<p align="center">&nbsp;</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Type</strong></p>
			</td>
			<td style="width:87px;">
				<p>Local</p>
			</td>
			<td style="width:95px;">
				<p>SDS</p>
			</td>
			<td style="width:99px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>SDS</p>
			</td>
			<td style="width:80px;">
				<p>Monolithique</p>
			</td>
			<td style="width:96px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Performances</strong></p>
			</td>
			<td style="width:87px;">
				<p>Basées sur les spécifications SSD/SA-SCSI ; RAID 5/10 peut être utilisé pour des gains en lecture/écriture.</p>
			</td>
			<td style="width:95px;">
				<p>90K+ IOPS par hôte en fonction de la configuration hôte. 100 machines virtuelles par hôte, 32 hôtes par cluster, 3 200 machines virtuelles par cluster, seulement 2 048 protégées (version 5.5)</p>
				<p>Jusqu'à 20K IOPS, 200 machines virtuelles par hôte, 64 hôtes par cluster et 6 000 machines virtuelles protégées par cluster (version 6.0).</p>
			</td>
			<td style="width:99px;">
				<p>Basées sur les types et le nombre de disques sélectionnés, ainsi que les configurations RAID et l'utilisation d'iSCSI ou de NFS.</p>
			</td>
			<td style="width:80px;">
				<p>Basées sur les types et le nombre de disques sélectionnés, ainsi que les actions de configuration RAID.</p>
			</td>
			<td style="width:80px;">
				<p>Dépendent du modèle.</p>
			</td>
			<td style="width:96px;">
				<p>Basées sur les types et le nombre de disques sélectionnés, ainsi que les configurations RAID et éventuellement l'utilisation de disque SSD par noeud d'hyperviseur.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Evolutivité</strong></p>
			</td>
			<td style="width:87px;">
				<p>Croissance limitée en taille et en débit d'entrées-sorties de disque</p>
			</td>
			<td style="width:95px;">
				<p>Disque de machine virtuelle (VMDK) jusqu'à 2 To avec la version 5.5, et 62 To avec la version 6.0.</p>
				<p>Ajouter davantage de noeuds.</p>
			</td>
			<td style="width:99px;">
				<p>QS unique jusqu'à 128 To (3.x). Pas d'ajout ou d'augmentation.</p>
			</td>
			<td style="width:80px;">
				<p>Jusqu'à 10 To ; pas d'ajout.</p>
			</td>
			<td style="width:80px;">
				<p>Oui, ajouter des répertoires de disque pour capacité et IOPS.</p>
			</td>
			<td style="width:96px;">
				<p>Mises à l'échelle de ~8 à 325 To d'espace utilisable.</p>
				<p>Capacité min. : 3 machines virtuelles x 6 unités.</p>
				<p>Capacité max. : 15 machines virtuelles x 12 unités.</p>
				<p>Augmente jusqu'à 144 grappes virtuelles et plus de 40 Po utilisables via IBM Hyper-Scale Manager.</p>
				<p>Extension de capacité sans interruption via l'ajout de noeuds supplémentaires.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocoles</strong></p>
			</td>
			<td style="width:87px;">
				<p>N/A</p>
			</td>
			<td style="width:95px;">
				<p>Propriétaire</p>
			</td>
			<td style="width:99px;">
				<p>iSCSI/NFS/SMB</p>
			</td>
			<td colspan="2" style="width:159px;">
				<p align="center">iSCSI/NFS/SMB</p>
			</td>
			<td style="width:96px;">
				<p>iSCSI</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Cas d'utilisation</strong></p>
			</td>
			<td style="width:87px;">
				<p>Charges de travail niveaux 2 et 3</p>
			</td>
			<td style="width:95px;">
				<p>Charges de travail de niveau 1</p>
			</td>
			<td style="width:99px;">
				<p>Charges de travail niveaux 2 et 3</p>
			</td>
			<td style="width:80px;">
				<p>Charges de travail niveaux 2 et 3</p>
			</td>
			<td style="width:80px;">
				<p>Charges de travail de niveau 1</p>
			</td>
			<td style="width:96px;">
				<p>Charges de travail de niveau 1</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Haute disponibilité (HA)</strong></p>
			</td>
			<td style="width:87px;">
				<p>Disponible avec RAID</p>
			</td>
			<td style="width:95px;">
				<p>Oui ; défaillance de disque et hôte ; domaines de défaillance (version 6.0)</p>
			</td>
			<td style="width:99px;">
				<p>Non disponible dans IBM Cloud.</p>
			</td>
			<td style="width:80px;">
				<p>N/A</p>
			</td>
			<td style="width:80px;">
				<p>Oui ; contrôleurs et têtes doubles.</p>
			</td>
			<td style="width:96px;">
				<p>Oui ; solution en cluster.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Configurabilité</strong></p>
			</td>
			<td style="width:87px;">
				<p>Nombre et type des disques ; niveaux RAID</p>
			</td>
			<td style="width:95px;">
				<p>Contrôleurs spécifiques requis.</p>
			</td>
			<td style="width:99px;">
				<p>UC, mémoire, cache, nombre et type des disques, niveaux RAID.</p>
			</td>
			<td style="width:80px;">
				<p>UC, mémoire, cache, nombre et type des disques, niveaux RAID.</p>
			</td>
			<td style="width:80px;">
				<p>À définir</p>
			</td>
			<td style="width:96px;">
				<p>UC, mémoire, cache, nombre et type des disques, SSD, mise en cache, configuration de port iSCSI. QOS multilocation.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Reprise après incident et réplication</strong></p>
			</td>
			<td style="width:87px;">
				<p>Utiliser vRA pour la réplication ; pas de SRA.</p>
			</td>
			<td style="width:95px;">
				<p>Utiliser vRA pour la réplication.</p>
			</td>
			<td style="width:99px;">
				<p>Réplication intégrée ; aucun SRA disponible.</p>
			</td>
			<td style="width:80px;">
				<p>Peut utiliser vRA pour la réplication, SnapMirror.</p>
			</td>
			<td style="width:80px;">
				<p>Peut utiliser vRA pour la réplication, SnapMirror, SnapVault.</p>
			</td>
			<td style="width:96px;">
				<p>vRA ou SRA pris en charge ; réplication entre unités SDS et/ou Physical XIV.</p>
				<p>Instantanés pris en charge ; reprise d'application via IBM FlashCopy Manager.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Fiabilité</strong></p>
			</td>
			<td style="width:87px;">
				<p>Point de défaillance unique sans haute disponibilité.</p>
			</td>
			<td style="width:95px;">
				<p>Tolère jusqu'à trois défaillances d'hôte avec sept hôtes.</p>
				<p>Domaines de défaillance introduits à la version 6.0.</p>
			</td>
			<td style="width:99px;">
				<p>Point de défaillance unique (boîtier et contrôleur RAID), pas de haute disponibilité.</p>
			</td>
			<td style="width:80px;">
				<p>Point de défaillance unique (boîtier et contrôleur RAID), pas de haute disponibilité.</p>
			</td>
			<td style="width:80px;">
				<p>Connexion E-S multi-accès (MPIO) hautement redondante.</p>
			</td>
			<td style="width:96px;">
				<p>Connexions E-S multi-accès (MPIO) iSCSI hautement redondantes ; tout noeud peut gérer le cluster. </p>
			</td>
		</tr>
	</tbody>
</table>

Tableau 2 Liens de documentation :
<!-- Internal link to exercise caution with QuantaStor: https://w3-connections.ibm.com/forums/html/topic?id=5c037198-96b8-43be-af21-edb47e4cf0bb#repliesPg=0-->
* NetApp OnTap Edge : Non disponible sur le portail client – apportez votre propre solution.
  * [Data ONTAP Installation and Administration Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://library.netapp.com/ecm/ecm_download_file/ECMP1200031){: new_window}
  * [Data ONTAP Express Setup Guide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://library.netapp.com/ecm/ecm_download_file/ECMP1369085){: new_window}
* [NetApp Private Storage for IBM Cloud ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.netapp.com/us/solutions/cloud/private-storage-cloud/softlayer.aspx){: new_window}
* Spectrum Accelerate : Non disponible sur le portail client – apportez votre propre solution.
  * [Working with an IBM Spectrum Accelerate system ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/support/knowledgecenter/STJTAG/com.ibm.help.xivgen3.doc/MT/UG/xiv_mt_deploying_spectrum_accelerate.html){: new_window}

Le tableau 3 répertorie les avantages et inconvénients du stockage partagé dans un environnement à service partagé.

<table border="1" cellpadding="0" cellspacing="0">
        <caption>Tableau 3. Options de stockage partagé VMware - Pour et Contre</caption>
	<tbody>
		<tr>
			<td colspan="3" style="width:638px;">
				<p><strong>Stockage partagé VMware (à service partagé)</strong></p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Facteurs clé / options de stockage</strong></p>
			</td>
			<td bgcolor="#C6D9F1" style="width:266px;">
				<p align="center">Endurance du stockage par blocs et de fichiers</p>
			</td>
			<td bgcolor="#C6D9F1" style="width:271px;">
				<p align="center">Performances du stockage par blocs et de fichiers</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Type</strong></p>
			</td>
			<td style="width:266px;">
				<p>SDS</p>
			</td>
			<td style="width:271px;">
				<p>SDS</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Performances</strong></p>
			</td>
			<td style="width:266px;">
				<p>Disponible en 0,25, 2, 4 ou 104 IOPS par Go</p>
				<p>Paramètres de performance de stockage prévisible</p>
				<p>Plusieurs volumes peuvent être segmentés afin d'atteindre des niveaux IOPS plus élevés et davantage de capacité de traitement</p>
			</td>
			<td style="width:271px;">
				<p>Le client met à disposition le niveau de performance souhaité en fonction des besoins de charge de travail et du point de prix.</p>
				<p>&nbsp;</p>
				<p>Paramètres de performance de stockage prévisible</p>
				<p>Plusieurs volumes peuvent être segmentés afin d'atteindre des niveaux IOPS plus élevés et davantage de capacité de traitement</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Evolutivité</strong></p>
			</td>
			<td style="width:266px;">
				<p>Tailles de volume entre 20 Go et 12 To. Pas de redimensionnement possible une fois la commande validée.</p>
			</td>
			<td style="width:271px;">
				<p>Tailles de volume entre 20 Go et 12 To. Pas de redimensionnement possible une fois la commande validée.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Protocoles</strong></p>
			</td>
			<td style="width:266px;">
				<p>iSCSI et NFS.</p>
			</td>
			<td style="width:271px;">
				<p>iSCSI et NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Connexions hôte</strong></p>
			</td>
			<td style="width:266px;">
				<p>Huit maximum pour iSCSI et 64 pour NFS.</p>
			</td>
			<td style="width:271px;">
				<p>Huit maximum pour iSCSI et 64 pour NFS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Cas d'utilisation</strong></p>
			</td>
			<td style="width:266px;">
				<p>Charges de travail de niveau 1, 2 et 3 :</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 0,25 IOPS par Go : faible intensité d'E-S. Des exemples d'application incluent le stockage de boîtes aux lettres ou de partages de fichiers au niveau du département.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 2 IOPS par Go : usage général. Des exemples d'application incluent des applications Web de sauvegarde de petites bases de données ou des images disque de machine virtuelle pour un hyperviseur.</p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 4 IOPS par Go : intensité élevée d'E-S. Des exemples d'application incluent des bases de données transactionnelles et autres bases sensibles aux performances. </p>
				<p style="margin-left:9.85pt;">&middot;&nbsp;&nbsp; 10 IOPS par Go : intensité élevée d'E-S. Des exemples d'applications incluent des analyses.</p>
			</td>
			<td style="width:271px;">
				<p>Charges de travail de niveau 1, 2 et 3 :</p>
				<p>Le stockage basé iSCSI des E-S multi-accès est idéalement conçu pour les applications d'E-S intensives telles que les bases de données relationnelles, qui nécessitent des niveaux prévisibles de performance. Les volumes de stockage sont fournis dans des tailles allant de 20 Go à 12 To, avec une plage d'opérations d'E-S par seconde (IOPS) sélectionnable par l'utilisateur et allant de 100 à 48 000 IOPS.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Haute disponibilité</strong></p>
			</td>
			<td style="width:266px;">
				<p>Oui, contrôleurs et têtes doubles.</p>
			</td>
			<td style="width:271px;">
				<p>Oui, contrôleurs et têtes doubles.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Configurabilité</strong></p>
			</td>
			<td style="width:266px;">
				<p>Taille et IOPS uniquement.</p>
			</td>
			<td style="width:271px;">
				<p>Taille et IOPS uniquement.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Reprise après incident et réplication</strong></p>
			</td>
			<td style="width:266px;">
				<p>Instantané et réplication fournis, exécution via le réseau privé IBM Cloud. Possibilité d'utiliser vRA pour la réplication au niveau machine virtuelle ; pas de SRA.</p>
			</td>
			<td style="width:271px;">
				<p>Instantané et réplication fournis, exécution via le réseau privé IBM Cloud. Possibilité d'utiliser vRA pour la réplication au niveau machine virtuelle ; pas de SRA.</p>
			</td>
		</tr>
		<tr>
			<td style="width:101px;">
				<p><strong>Fiabilité</strong></p>
			</td>
			<td style="width:266px;">
				<p>Hautement redondant, connexion MPIO, stockage de fichiers basé NFS, connexions TCP/IP routées. Instantanés et réplication activés.</p>
			</td>
			<td style="width:271px;">
				<p>Hautement redondant, connexion MPIO, stockage de fichiers basé NFS, connexions TCP/IP routées. </p>
			</td>
		</tr>
	</tbody>
</table>

Tableau 3 Liens de documentation :
* [Stockage par blocs](/docs/infrastructure/BlockStorage/index.html)
* [Stockage de fichiers](/docs/infrastructure/FileStorage/index.html)
