---
title: Linux SSH
description: 
published: 1
date: 2021-12-24T13:18:32.050Z
tags: 
editor: markdown
dateCreated: 2021-12-24T13:07:21.233Z
---

# Présentation
Secure Shell ou SSH est un protocole permettant d'établir une communication chiffrée entre une machine locale et une machine distante. Grâce à SSH, on peut se connecter à distance sur une machine si cette dernière dispose d'un serveur SSH

La sécurité du chiffrement peut se faire via différentes méthodes : mot de passe ou un système de clés publique / privée

# Se connecter via mdp
Pour se connecter en SSH, la machine distance devra disposer d'un serveur ssh.

Vous pouvez vous connecter avec des utilitaires tel que Putty
Ou en ligne de commande :

Il faudra utiliser un utilisateur de la machine distante. Ainsi que son adress IP ou son nom DNS.
La commande utilisera le port 22 par défaut.
```bash
ssh utilisateur@192.168.1.2
```

Pour se connecter avec un port spécifique :
```bash
ssh utilisateur@192.168.1.2 -p 9056
```

# Installation

# Tabs {.tabset}
## Debian
```bash
apt install openssh-server
```
## RedHat
```bash
dnf install openssh-server
```
## Gentoo
```bash
emerge net-misc/openssh
```
# Configuration

Le fichier de configuration d'openssh ce situe : `/etc/ssh/sshd_config`

> Il faudra rechargez le configuration du fichier pour chaque modification apporté :
> <kbd>systemctl reload sshd</kbd>
{.is-warning}


## Désactiver les connexions root

Décommenter et modifier la ligne **PermitRootLogin**

```bash
PermitRootLogin no
```
Réactiver les connexions root en ssh :
```bash
PermitRootLogin prohibit-password
```

## Changer le port

Le ssh utilise le port 22 par défaut, pour le changer, modifier la ligne **Port**
```bash
Port 2596
```
Une fois le fichier rechargez, utiliser le port que vous avez séléctionnez dans votre fichier.

## Autoriser/Interdire des utilisateurs
Pour ajoutez une liste d'utilisateur autoriser à se connecter, ajoutez les lignes :
```bash
AllowUsers user1 user2
```

Pour refuser la connexion de certains utilisateur : 
```bash
DenyUsers user1 user2
```

## Autoriser/Interdire des groupes
Pour ajoutez une liste de groupes autoriser à se connecter, ajoutez les lignes :
```bash
AllowGroups groupe1 groupe2
```

Pour refuser la connexion de certains groupes : 
```bash
DenyGroups groupe1 groupe2
```

## Afficher une bannière
Il est possible d'ajouter une bannière (message) lors de la connexion via ssh.

Décommenté la ligne "Banner" dans le fichier de configuration /etc/ssh/sshd_config et mettez y le nom du fichier de la bannière :
```bash
Banner /etc/banner
```

Il faudra créer le fichier dans `/etc/banner` et y insérez notre bannière