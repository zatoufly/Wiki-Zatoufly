---
title: XenServer - Gestion des VMs
description: 
published: true
date: 2022-01-16T19:44:54.717Z
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

Séléctionnez le système d'exploitation que vous souhaitez installer

![xenserver-installvm_02.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_02.jpg)

Nommez votre machine virtuelle

![xenserver-installvm_03.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_03.jpg)

Séléctionnez votre fichier ISO dans votre library (doit être configurée au préalable)

![xenserver-installvm_04.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_04.jpg)

Séléctionnez sur quel node (hyperviseur) vous souhaité exécuter la machine virtuelle

![xenserver-installvm_05.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_05.jpg)

Donnez lui un nombre de vCPU et une quantité de mémoire vive

![xenserver-installvm_06.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_06.jpg)

Séléctionnez le disque de stockage où sera enregistez la machine virtuelle

![xenserver-installvm_07.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_07.jpg)

Configurer les interfaces réseau de votre VM

![xenserver-installvm_08.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_08.jpg)

Vérifiez que les informations sont correct puis créer la VM

![xenserver-installvm_09.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_09.jpg)

On peux voir que notre machine virtuelle à bien été créer

![xenserver-installvm_10.jpg](/virtualisation/xenserver/gestion_vm/xenserver-installvm_10.jpg)