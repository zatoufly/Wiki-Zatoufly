---
title: Windows Server 2019 - Active Directory
description: 
published: 1
date: 2022-01-06T09:25:41.300Z
tags: 
editor: markdown
dateCreated: 2022-01-06T09:25:41.300Z
---

![windows_serveur_2019-banner.png](/microsoft/windows_server_2019/windows_serveur_2019-banner.png){.align-center}
 
 
# Présentation
Le rôle Active Directory  permet d'ajouter un annuaire LDAP. L'objectif principal est de fournir des services centralisés d'identification et d'authentification à un parc informatique utilisant des systèmes Windows.
 
Il permet également l'application de stratégie (GPO)
 
# Prérequis
- Machine sous Windows Server 2019
- Un mot de passe fort pour le compte administrateur
- Une adresse IP fixe
 
# Installation
 
### Ajoutez le rôle AD DS au serveur
![winserv19-active_directory_01.jpg](/microsoft/windows_server_2019/adds/winserv19-active_directory_01.jpg)
 
### Promouvoir le serveur en contrôleur de domaine
![winserv19-active_directory_02.jpg](/microsoft/windows_server_2019/adds/winserv19-active_directory_02.jpg)
 
### Ajoutez une nouvelle forêt et renseignez un nom dns
![winserv19-active_directory_03.jpg](/microsoft/windows_server_2019/adds/winserv19-active_directory_03.jpg)
 
### Renseignez le mot de passe du mode restauration des services d'annuaire
![winserv19-active_directory_04.jpg](/microsoft/windows_server_2019/adds/winserv19-active_directory_04.jpg)
 
### Déléguez le DNS au besoin
![winserv19-active_directory_05.jpg](/microsoft/windows_server_2019/adds/winserv19-active_directory_05.jpg)
 
### Renseignez un nom NETBIOS
![winserv19-active_directory_06.jpg](/microsoft/windows_server_2019/adds/winserv19-active_directory_06.jpg)
 
### Spécifiez l'emplacement de la base de données AD DS et de SYSVOL
![winserv19-active_directory_07.jpg](/microsoft/windows_server_2019/adds/winserv19-active_directory_07.jpg)
 
> à la fin de la configuration, votre serveur va redémarrer 
{.is-warning}
 
> Félicitation, votre service AD DS est configurée et fonctionnel
{.is-success}