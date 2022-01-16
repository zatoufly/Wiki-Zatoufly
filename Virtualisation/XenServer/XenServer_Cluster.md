---
title: XenServer - Cluster
description: 
published: true
date: 2022-01-16T20:44:22.300Z
tags: xenserver
editor: markdown
dateCreated: 2022-01-16T20:44:22.300Z
---

![logo_xenserver.png](/virtualisation/xenserver/logo_xenserver.png =400x){.align-center}
 

# Introduction
Un cluster ou pool est une technique qui consiste à regrouper plusieurs hyperviseurs appelés “noeud” ou “node”, afin de permettre une meilleure gestion des ressources et ainsi augmenter la HA (High Availability)

# Prérequis
- Deux XenServer d'installer
- XenCenter installer sur un client
- Un disque virtuelle iSCSI créer ([sur windows dans ce tuto](/Microsoft/Windows_Server_2019/Cible-iSCSI))
 
> Fonctionne également pour XCP-ng
{.is-info}
 
 
# Installation

Dans ce tutoriel, j’utilise XenServer comme Hyperviseur, voici le schéma ci dessous de ma solution :

![xenserver-makecluster_01.jpg](/virtualisation/xenserver/xenserver-makecluster_01.jpg)

Sur XenCenter on va pouvoir créer notre cluster. En haut de de l’application, cliquez sur “New Pool”


![xenserver-makecluster_02.jpg](/virtualisation/xenserver/xenserver-makecluster_02.jpg)

Ensuite cliquez sur le bouton “Add New Server” en bas pour ajouter vos deux Hyperviseurs, le premier serveur ajoutez sera le serveur dit “Master” par défaut.

![xenserver-makecluster_03.jpg](/virtualisation/xenserver/xenserver-makecluster_03.jpg)

Ensuite on peut créer le Cluster avec “Create Pool” en bas

On va maintenant ajoutez le disque iSCSI précédemment créé, pour cela faite un clique droit sur votre Cluster puis cliquez sur “Add SR”


![xenserver-makecluster_04.jpg](/virtualisation/xenserver/xenserver-makecluster_04.jpg)

Ici on choisi un disque iSCSI

![xenserver-makecluster_05.jpg](/virtualisation/xenserver/xenserver-makecluster_05.jpg)

Vous pouvez changez son nom par défaut si besoin

![xenserver-makecluster_06.jpg](/virtualisation/xenserver/xenserver-makecluster_06.jpg)

Indiquez le l’IP de votre serveur windows et cliquez sur “Scan Target Host”

![xenserver-makecluster_07.jpg](/virtualisation/xenserver/xenserver-makecluster_07.jpg)

Ensuite sélectionnez la target IQN, j’ai choisi la première en IPv4 

![xenserver-makecluster_08.jpg](/virtualisation/xenserver/xenserver-makecluster_08.jpg)

Ensuite il recherchera un Target LUNs automatiquement

![xenserver-makecluster_09.jpg](/virtualisation/xenserver/xenserver-makecluster_09.jpg)

Votre disque iSCSI est maintenant ajoutez au cluster

![xenserver-makecluster_10.jpg](/virtualisation/xenserver/xenserver-makecluster_10.jpg)

Vos VMs / images ISO devront être stocker dans le disque virtuel iSCSI afin que les deux nodes puissent y avoir accès 