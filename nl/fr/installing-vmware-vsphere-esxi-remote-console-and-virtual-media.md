---
copyright:
  years: 1994, 2017
lastupdated: "2017-12-18"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Installation de VMware vSphere ESXi via la console distante et le support virtuel
{: #installing-vsphere-esxi}

Le déploiement d'ESX depuis le support d'installation est similaire quelle que soit la version et peut être utilisé dans des scénarios BYOL (Bring Your Own License, licence à fournir). 

## Exigences
* Une instance de machine virtuelle (VM) qui peut accéder au réseau privé [par exemple, une instance de serveur virtuel (VSI) installée avec Windows ou Linux, avec un navigateur activé pour Java, accessible via vpn.softlayer.com ou une IP publique IP]. L'instance VSI doit être sur le même réseau privé que les adresses Intelligent Platform Management Interface (IPMI) du serveur.
* Une copie de l'image ISO du programme d'installation de VMware ESXi VIM.

<!--## Steps -->

## Connexion à IPMI
1. Téléchargez l'image ISO VMware dans l'instance VSI spécifiée dans les exigences (Les instances de serveur virtuel doivent disposer d'un accès Web public.)
2. Collectez les informations de connexion et d'adresse IPMI depuis le portail client.
3. Sélectionnez **Equipements** > **Liste des unités** > **[Serveur]** > puis l'onglet **Gestion à distance**.
4. Connectez-vous via le bureau distant (RDP) ou Remote X à l'instance VSI qui stocke l'image ESXi.
5. Ouvrez un navigateur Web dans la session RDP et entrez l'adresse d'IPMI que vous avez collectée à l'étape 2.
6. Connectez-vous à la console IPMI avec les données d'identification qui figurent également à l'étape 2 (il s'agit généralement de root).
* Notez votre niveau d'accès utilisateur IPMI. Il peut s'agir du niveau administrateur. Il est possible que vous rencontriez un problème lorsque vous montez votre stockage distant si celui-ci est défini sur **Operator**. Remplissez un ticket de demande de service afin d'augmenter vos données d'identification IPMI si vous ne parvenez pas à monter le support.
7. Vérifiez que vous êtes sur la page de connexion puis cliquez sur **Remote Control** > **Console Redirection** > **Launch Console**.

## Connexion d'image ISO
1. Dans l'afficheur de la machine virtuelle multinoyaux (KVM), sélectionnez **Virtual Media** > **Virtual Storage**. Votre système d'exploitation et la version de Java peuvent nécessiter d'autoriser l'accès à l'afficheur basé Java.
2. Cliquez sur l'onglet **CDROM & ISO** de la fenêtre Virtual Storage. Pour le type d'unité logique, sélectionnez **ISO File** et cliquez sur **Open Image**.
3. Accédez à l'image ISO d'ESXi et cliquez sur **OK**. Cliquez ensuite sur **Plug in**.
4. Une fois l'image ISO connectée à la session, cliquez sur **OK**.
* Revenez à la page Web d'IPMI et cliquez sur **Remote** > **Control** > **Reset Server** > **Perform Action** pour redémarrer le serveur.

### Installation et fin de la configuration du réseau
1. Installez ESXi.
* Une fois l'installation terminée, veillez à **déconnecter** l'image ISO afin de pouvoir redémarrer le serveur. 
2. Redémarrez le serveur.
3. Configurez l'adresse IP du serveur après son redémarrage.
4. Collectez les détails de l'onglet Configuration sur l'unité.

Vous pouvez désormais gérer l'hôte ESXi.

Pour plus d'informations sur la configuration du stockage par blocs de type Endurance ou Performance, voir [Mise à disposition et gestion du stockage par blocs](/docs/infrastructure/BlockStorage/provisioning-block_storage.html).

Pour plus d'informations sur la configuration de QuantaStor, voir le [Guide d'architecture pour QuantaStor](architecture-guide-quantastor-vmwaresoftlayer.html).
