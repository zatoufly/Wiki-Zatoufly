---
title: LXC / LXD
description: 
published: true
date: 2022-01-17T10:20:22.260Z
tags: 
editor: markdown
dateCreated: 2022-01-17T10:20:22.260Z
---

# Introduction
LXC LXD est sortie en 2014 (1 ans après docker) développé par Canonical.
Il permet de conteneuriser des systèmes uniquement (pas d'application : nginx, mariadb, etc...)

Un des avangates de LXC/LXD réside dans la gestion des snapshots.

# Installation
```bash
apt install lxd lxd-client 
ou :
apt install lxc
```

# Commandes
Liste des images disponible : https://uk.lxd.images.canonical.com/

|     |     |
| --- | --- |
| `lxc list` | liste les conteneurs |
| `lxc image list` | liste les images local |
| `lxd init` | initialise l'installation de lxc/lxd |
| `lxc image copy images:alpine/3.12 local: --alias <donner un nom>` | pull une image |
| `lxc launch <image> <nom conteneur>` | créer un conteneur |
| `lxc exec <nom conteneur> -- <commande>` | exécuter une commande dans un conteneur |
| `lxc rm --force` | initialise l'installation de lxc/lxd |
| `lxc stop <conteneur>` | arrête le conteneur |
| `lxc start <conteneur>` | démarre un conteneur |
| `lxc rm <conteneur>` | supprime un conteneur |
| `lxc info <conteneur> ` | voir des information liée au conteneur |
| `lxc file edit <conteneur>/path/to/file` | éditez un fichier dans un conteneur |
| `lxc file push path/to/file.html <conteneur>/var/www/index.html` | push le conteneur du fichier |
| `lxc snapshot <conteneur> <nom de la snapshot>` | créer une snapshot |
| `lxc restore <conteneur> <nom de la snapshot>` | restaurer une snapshot |
| `lxc copy <conteneur> <nom conteneur copier>` | dupliquer un fichier |