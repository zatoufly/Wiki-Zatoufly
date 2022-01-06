---
title: Windows Server 2019 - Active Directory
description: 
published: 1
date: 2022-01-06T09:46:26.403Z
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
 
# Configurations
## Ajoutez un client Windows 10/11 dans un AD
 
# Tabs {.tabset}
## Méthode graphique (W10)
 
1. Allez dans les paramètres -> systèmes -> à propos de -> paramètres avancés du système
![winserv19-ad_add_client_01.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_01.jpg)
 
2. Allez dans l'onglet "Nom de l'ordinateur"
![winserv19-ad_add_client_02.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_02.jpg)
 
3. Cliquez sur modifier
![winserv19-ad_add_client_03.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_03.jpg)
 
4. Renseignez un nom pour l'ordinateur et renseignez votre domaine
![winserv19-ad_add_client_04.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_04.jpg)
 
5. Authentifiez vous avec un utilisateur LDAP
![winserv19-ad_add_client_05.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_05.jpg)
 
6. redémarrez votre machine
 
## En Powershell
 
1. Ouvez powershell en tant qu'administrateur, effectuer cette commande (avec votre nom DNS)
```powershell
Add-Computer -DomainName zatoufly.lan
```
 
2. Une page s'affiche pour vous connecter, puis redémarrer votre machine

# Créer une GPO
## Désactiver le CMD

### Séléctionnez l'outil "Gestion de stratégie de groupe"
![winserv19-gpo_bloquer_cmd_01.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_01.jpg)

### Créer une GPO sur le domaine
![winserv19-gpo_bloquer_cmd_02.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_02.jpg)

### Nommez votre GPO
![winserv19-gpo_bloquer_cmd_03.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_03.jpg)

### Modifier la GPO
![winserv19-gpo_bloquer_cmd_04.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_04.jpg)

### Recherche "Désactiver l'accès à l'invite de commandes"
![winserv19-gpo_bloquer_cmd_05.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_05.jpg)

### Activer la GPO
![winserv19-gpo_bloquer_cmd_06.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_06.jpg)

### Faite un clic droit sur le GPO puis Appliquer

### Mettez à jour la stratégie de l'ordinateur 
```powershell
gpupdate /force
```

![winserv19-gpo_bloquer_cmd_08.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_08.jpg)


















