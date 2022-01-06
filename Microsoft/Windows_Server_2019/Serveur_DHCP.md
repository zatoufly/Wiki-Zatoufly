---
title: Windows Server 2019 - Serveur DHCP
description: 
published: 1
date: 2022-01-06T09:02:52.293Z
tags: 
editor: markdown
dateCreated: 2022-01-05T12:47:14.657Z
---

![windows_serveur_2019-banner.png](/microsoft/windows_server_2019/windows_serveur_2019-banner.png){.align-center}
 
 
# Présentation
Le service de routage permet de connecter plusieurs réseaux entre eux.
 
 
# Prérequis
- Machine sous Windows Server 2019
- Une interface WAN et une interface LAN au minimum
- Une adresse IP fixe
 
# Installation
 
### Ajoutez un rôle à votre serveur
![winserv19-routage_01.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_01.jpg)
 
### Ajoutez le rôle "Accès à distance"
![winserv19-routage_02.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_02.jpg)
 
### Sélectionnez le rôle Routage
![winserv19-routage_03.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_03.jpg)
 
### Sélectionnez l'outil "Routage et accès distant"
![winserv19-routage_04.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_04.jpg)
 
### Configurez et activer le routage et l'accès à distance
![winserv19-routage_05.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_05.jpg)
 
### Sélectionnez le mode NAT
![winserv19-routage_06.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_06.jpg)
 
### Sélectionnez votre interface WAN
![winserv19-routage_07.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_07.jpg)
 
### Valider la configuration
![winserv19-routage_08.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_08.jpg)
 
### Votre service de routage est opérationnel
![winserv19-routage_09.jpg](/microsoft/windows_server_2019/routage/winserv19-routage_09.jpg)
 
> Félicitation, votre service de routage est configurée et fonctionnel
{.is-success}