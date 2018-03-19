---
copyright:
  years: 1994, 2017
lastupdated: "2017-09-15"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Configuration de réseaux de stockage virtuel (vSAN) pour la stabilité sur des contrôleurs de base LSI 3108

Afin d'aider à prévenir les défaillances liées aux équipements lors de l'exécution du réseau de stockage virtuel (vSAN) avec des contrôleurs de série LSI 3108, exécutez les commandes suivantes depuis le shell ESXi :

`esxcfg-advcfg -s 100000 /LSOM/diskIoTimeout`<br/>
`esxcfg-advcfg -s 4 /LSOM/diskIoRetryFactor`

Remarque :

* Ces commandes doivent être exécutées sur chaque hôte ESXi du cluster vSAN.
* Ces commandes sont effectives immédiatement. Aucun réamorçage n'est requis.
* Ces commandes se traduisent par des changements durables et restent configurées après réamorçage.

Pour plus d'informations, voir la rubrique de la base de connaissances VMware [Required vSAN and ESXi configuration for controllers based on the LSI 3108 chipset ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://kb.vmware.com/s/article/2144936){: new_window}.
