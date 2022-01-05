---
title: Windows Server 2019 - Serveur Cible iSCSI
description: 
published: 1
date: 2022-01-05T12:10:34.086Z
tags: 
editor: markdown
dateCreated: 2022-01-05T12:10:34.086Z
---

![windows_serveur_2019-banner.png](/microsoft/windows_server_2019/windows_serveur_2019-banner.png){.align-center}


# Présentation
l'iSCSI (internet Small Computer System Interface) est basé sur le protocole IP et est destiné à faire du stockage par le réseau.

# Installation

### Ajoutez le rôle "Serveur Cible iSCSI" à votre serveur
![winserver19-serveur-iscsi-1.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-1.jpg)

### Démarrer l'assistant de créer de disque virtuel iSCSI
![winserver19-serveur-iscsi-2.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-2.jpg)

### Séléctionnez l'emplacement du disque iSCSI
![winserver19-serveur-iscsi-3.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-3.jpg)

### Nommez le
![winserver19-serveur-iscsi-4.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-4.jpg)

### Indiquez le taille du disque iSCSI
![winserver19-serveur-iscsi-5.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-5.jpg)

### Créer une nouvelle cible iSCSI
![winserver19-serveur-iscsi-6.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-6.jpg)

### Nommez la cible iSCSI
![winserver19-serveur-iscsi-7.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-7.jpg)

### Renseigner les serveurs qui utiliseront le disque iSCSI
Cette page vous permet de spécifier les initiateurs qui peuvent accéder au disque virtuel, en permettant à la cible d'être découverte par une liste définie d'initiateurs. Vous pouvez utiliser l'IQN, le nom DNS ou l'adresse IP.

![winserver19-serveur-iscsi-8.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-8.jpg)

### Activer ou non CHAP 
![winserver19-serveur-iscsi-9.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-9.jpg)

### Créer votre disque virtuel iSCSI
![winserver19-serveur-iscsi-10.jpg](/microsoft/windows_server_2019/winserver19-serveur-iscsi-10.jpg)