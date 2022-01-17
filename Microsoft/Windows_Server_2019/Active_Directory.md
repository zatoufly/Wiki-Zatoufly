---
title: Windows Server 2019 - Active Directory
description: 
published: true
date: 2022-01-17T14:16:55.072Z
tags: 
editor: markdown
dateCreated: 2022-01-14T20:22:27.226Z
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
## Créer utilisateur
Dans le centre d'administration de windows, dans outils séléctionnez "Utilisateurs et ordinateurs Active Directory"

Sélectionnez votre domaine, dans mon cas "zatoufly.lan" puis allez dans "Users"

![srvw19-createuser_01.jpg](/microsoft/windows_server_2019/adds/srvw19-createuser_01.jpg)

Faite un clique droit sur le dossier "Users" et cliquez sur "nouveau" puis "Utilisateur"

![srvw19-createuser_02.jpg](/microsoft/windows_server_2019/adds/srvw19-createuser_02.jpg)

Ici renseignez les informations de votre utilisateur

![srvw19-createuser_03.jpg](/microsoft/windows_server_2019/adds/srvw19-createuser_03.jpg)

Créer un mot de passe pour l'utilisateur.
Vous pouvez également séléctionnez quelques option qui peuvent e^tre intereessantes selon la politiques de sécurité de votre entreprise.

![srvw19-createuser_04.jpg](/microsoft/windows_server_2019/adds/srvw19-createuser_04.jpg)

Cliquez sur "Terminer" pour créer l'utilisateur

![srvw19-createuser_05.jpg](/microsoft/windows_server_2019/adds/srvw19-createuser_05.jpg)

> Félicitations, vous avez créer votre utilisateur
{.is-success}
## Ajoutez un client Windows 10/11 dans un AD
 
# Tabs {.tabset}
## Méthode graphique (W10)
 
Allez dans les paramètres -> systèmes -> à propos de -> paramètres avancés du système
![winserv19-ad_add_client_01.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_01.jpg)
 
Allez dans l'onglet "Nom de l'ordinateur"
![winserv19-ad_add_client_02.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_02.jpg)
 
Cliquez sur modifier
![winserv19-ad_add_client_03.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_03.jpg)
 
Renseignez un nom pour l'ordinateur et renseignez votre domaine
![winserv19-ad_add_client_04.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_04.jpg)
 
Authentifiez vous avec un utilisateur LDAP
![winserv19-ad_add_client_05.jpg](/microsoft/windows_server_2019/adds/winserv19-ad_add_client_05.jpg)
 
redémarrez votre machine
 
## En Powershell
 
Ouvez powershell en tant qu'administrateur, effectuer cette commande (avec votre nom DNS)
```powershell
Add-Computer -DomainName zatoufly.lan
```
 
Une page s'affiche pour vous connecter, puis redémarrer votre machine

## Fedora

Il faudra que votre fedora puisse joindre votre domaine, vous pouvez vérifiez avec :
```bash
ping -c2 zatoufly.lan
```

Ouvrez un terminal et tapez la commande :
vous pouvez utiliser le compte administrateur ou un compte pouvez faire adhérez un ordinateur à l'AD
```bash
realm join --user administrateur zatoufly.lan
```
Il faudra insérez le mot de passe du compte administrateur.

Si je regarde dans mon AD, j'ai bien ma Fedora qui s'est join au domaine.

![winservjoinfedora_01.jpg](/microsoft/windows_server_2019/adds/winservjoinfedora_01.jpg)

On peux également vérifiez avec la commande :
```bash
realm list
```

![winservjoinfedora_02.jpg](/microsoft/windows_server_2019/adds/winservjoinfedora_02.jpg)

On peux maintenant se connecter avec un utilisateur de l'AD :

```bash
su - jean@zatoufly.lan
```
Le mot de passe de l'utilisateur vous sera demandé.

Et si on liste les répertoires homes, on peux voir qu'un répertoire à été créer pour l'utilisateur de l'AD

```bash
ls /home
```


![winservjoinfedora_03.jpg](/microsoft/windows_server_2019/adds/winservjoinfedora_03.jpg)


# Créer une GPO
## Désactiver le CMD
 
Sélectionnez l'outil "Gestion de stratégie de groupe"
![winserv19-gpo_bloquer_cmd_01.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_01.jpg)
 
Créer une GPO sur le domaine
![winserv19-gpo_bloquer_cmd_02.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_02.jpg)
 
Nommez votre GPO
![winserv19-gpo_bloquer_cmd_03.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_03.jpg)
 
Modifier la GPO
![winserv19-gpo_bloquer_cmd_04.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_04.jpg)
 
Recherche "Désactiver l'accès à l'invite de commandes"
![winserv19-gpo_bloquer_cmd_05.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_05.jpg)
 
Activer la GPO
![winserv19-gpo_bloquer_cmd_06.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_06.jpg)
 
Faite un clic droit sur le GPO puis Appliquer
 
Mettez à jour la stratégie de l'ordinateur 
```powershell
gpupdate /force
```
 
![winserv19-gpo_bloquer_cmd_08.jpg](/microsoft/windows_server_2019/adds/winserv19-gpo_bloquer_cmd_08.jpg)