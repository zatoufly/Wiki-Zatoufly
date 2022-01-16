---
title: XenServer - Gestion des VMs
description: 
published: true
date: 2022-01-16T20:20:42.780Z
tags: xenserver
editor: markdown
dateCreated: 2022-01-16T19:33:05.616Z
---

![logo_xenserver.png](/virtualisation/xenserver/logo_xenserver.png =400x){.align-center}
 
# Prérequis
- Un XenServer d'installer et configurée sur XenCenter
 
> Fonctionne également pour XCP-ng
{.is-info}
 
 
# Créer une VM
 
Dans XenCenter, cliquez sur New VM
 
![xenserver-installvm_01.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_01.jpg)
 
Sélectionnez le système d'exploitation que vous souhaitez installer
 
![xenserver-installvm_02.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_02.jpg)
 
Nommez votre machine virtuelle
 
![xenserver-installvm_03.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_03.jpg)
 
Sélectionnez votre fichier ISO dans votre library (doit être configurée au préalable)
 
![xenserver-installvm_04.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_04.jpg)
 
Sélectionnez sur quel node (hyperviseur) vous souhaitez exécuter la machine virtuelle
 
![xenserver-installvm_05.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_05.jpg)
 
Donnez lui un nombre de vCPU et une quantité de mémoire vive
 
![xenserver-installvm_06.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_06.jpg)
 
Sélectionnez le disque de stockage où sera enregistré la machine virtuelle
 
![xenserver-installvm_07.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_07.jpg)
 
Configurer les interfaces réseau de votre VM
 
![xenserver-installvm_08.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_08.jpg)
 
Vérifiez que les informations sont correct puis créer la VM
 
![xenserver-installvm_09.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_09.jpg)
 
On peux voir que notre machine virtuelle à bien été créer
 
![xenserver-installvm_10.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_10.jpg)
 
# Créer une template
Convertir une VM en template rendra inutilisable votre machine virtuelle. La template vous permet de créer une configuration type d'une machine pour ensuite la dupliquer à volonté. Cela permet de gagner du temps.
 
Faites un clique droit sur la machine que vous souhaitez convertir et cliquez sur "Convert to Template...
"
![xenserver-converttemplate_01.jpg](/virtualisation/xenserver/gestion_vm/xenserver-converttemplate_01.jpg)
 
Valider l'avertissement
 
![xenserver-converttemplate_02.jpg](/virtualisation/xenserver/gestion_vm/xenserver-converttemplate_02.jpg)
 
Vous voilà avec une template d'un debian
 
![xenserver-converttemplate_02.jpg](/virtualisation/xenserver/gestion_vm/xenserver-converttemplate_03.jpg)
 
# Déplacer une VM
Déplacer une VM est faisable uniquement dans un cluster d'hyperviseur. Il faudra que la VM soit stockée sur un support de stockage exporter au hyperviseur (en iSCSI, NFS, SMB, etc..) Il faudra également que ce support soit accessible par les deux hyperviseur.
 
Faites un clique droit sur la VM à déplacer puis cliquez sur "Move VM"
 
![xenserver-movevm_01.jpg](/virtualisation/xenserver/gestion_vm/xenserver-movevm_01.jpg)
 
Sélectionnez le node où sera transférez la VM
 
![xenserver-movevm_02.jpg](/virtualisation/xenserver/gestion_vm/xenserver-movevm_02.jpg)
 
Sélectionnez votre support de stockage externe
 
![xenserver-movevm_03.jpg](/virtualisation/xenserver/gestion_vm/xenserver-movevm_03.jpg)
 
Cliquez sur continuer
 
![xenserver-movevm_04.jpg](/virtualisation/xenserver/gestion_vm/xenserver-movevm_04.jpg)
 
Cliquez sur "Finish" pour valider l'opération
 
![xenserver-movevm_05.jpg](/virtualisation/xenserver/gestion_vm/xenserver-movevm_05.jpg)
 
On peut voir que ma VM à bien été migrer
 
![xenserver-movevm_06.jpg](/virtualisation/xenserver/gestion_vm/xenserver-movevm_06.jpg)
 
# Copier une VM
 
Faite une clique droit sur la VM à copier et cliquez sur "Copy VM"
 
![xenserver-copyvm_01.jpg](/virtualisation/xenserver/gestion_vm/xenserver-copyvm_01.jpg)
 
Sélectionnez sur quel node vous souhaitez copier la VM.
 
![xenserver-copyvm_02.jpg](/virtualisation/xenserver/gestion_vm/xenserver-copyvm_02.jpg)
 
Nommez la copie de la VM
 
![xenserver-copyvm_03.jpg](/virtualisation/xenserver/gestion_vm/xenserver-copyvm_03.jpg)
 
Sélectionnez "Full copy" pour copier entièrement la VM et sélectionnez où elle sera stockez
 
![xenserver-copyvm_04.jpg](/virtualisation/xenserver/gestion_vm/xenserver-copyvm_04.jpg)
 
On peut voir que la VM à bien été copiés
 
![xenserver-copyvm_05.jpg](/virtualisation/xenserver/gestion_vm/xenserver-copyvm_05.jpg)
 
# Supprimer une VM
 
Faites une clique droit sur la VM à supprimer et cliquez sur "Delete VM"
 
![xenserver-delvm_01.jpg](/virtualisation/xenserver/gestion_vm/xenserver-delvm_01.jpg)
 
Confirmer la suppression de la VM
 
![xenserver-delvm_02.jpg](/virtualisation/xenserver/gestion_vm/xenserver-delvm_02.jpg)
 
La machine virtuelle à bien été supprimée.
 
![xenserver-delvm_03.jpg](/virtualisation/xenserver/gestion_vm/xenserver-delvm_03.jpg)