---
title: Open Media Vault - iSCSI
description: 
published: 1
date: 2021-12-23T10:36:24.475Z
tags: 
editor: markdown
dateCreated: 2021-12-21T19:01:36.042Z
---

# Créer une cible iSCSI
OpenMediaVault ne permet pas nativement de créer une cible iSCSI. Pour ce faire, nous avons besoin d'ajouter un paquet supplémentaire sur notre OMV.
 
Pour se faire on va se connecter en ssh sur OMV, une fois fait, exécuter la commande suivante :
 
```bash
wget -O - https://raw.githubusercontent.com/OpenMediaVault-Plugin-Developers/packages/master/install | bash
```
 
Ensuite allez sur l'interface web de votre OMV, dans la section plugins installer :
- openmediavault-lvm2
- openmediavault-tgt
 
## Création des volumes LVM
 
Dans l'onglet "Logical Volume Management" cliquez sur ajouter un Physical volumes. Ajoutez tous les disques que vous souhaitez utiliser.
 
![omv-cible-iscsi-1.png](/nas/omv/omv-cible-iscsi-1.png)
 
> Si vous voyez pas vos disques dans la liste, formater les dans l'onglet "Disques"
{.is-warning}
 
 
Ensuite allez dans l'onglet "Volume groups" en haut de la page, cliquez sur ajouter.
 
Nommez votre volume group et mettez-y tous vos disques.
 
![omv-cible-iscsi-2.png](/nas/omv/omv-cible-iscsi-2.png)
 
Pour finir allez dans l'onglet "Logical volumes", cliquez sur ajouter. Nommer le logical volume, renseigner le volume group précédemment créé puis mettez la taille que vous souhaitez lui donner.
 
![omv-cible-iscsi-3.png](/nas/omv/omv-cible-iscsi-3.png)
 
## Créer la cible iSCSI
 
Allez dans l'onglet "tgt" et activez le service.
 
Dans l'onglet "Targets" cliquez sur "Ajouter". Mettez le nom que vous souhaitez
Dans le Backing Store mettez `/dev/mapper/` suivi de : `volume_group-logical_volume`
 
Pour moi ça donne : `/dev/mapper/LVM_GRP-LVM_STORAGE`
 
Vous pouvez y mettre l'adresse d'un initiateur iSCSI.
 
![omv-cible-iscsi-4.png](/nas/omv/omv-cible-iscsi-4.png)
 
> Félicitation, vous avez créer une cible iSCSI
{.is-success}