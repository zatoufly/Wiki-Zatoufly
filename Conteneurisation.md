---
title: Conteneurisation
description: 
published: true
date: 2022-02-18T14:17:15.583Z
tags: 
editor: markdown
dateCreated: 2022-01-18T11:57:41.193Z
---

# Introduction
La conteneurisation consiste à rassembler le code du logiciel et toutes ses dépendances dans une "image". Cette image permet de lancer un conteneur de manière isoler de la machine hôte.

Les conteneurs se partage le même noyau de système d'exploitation et isolent les processus de l'application du reste du système.

Un Hyperviseur virtualise du matérielle hardware avec un système d'exploitation tandis que la conteneurisation fait appel directement à l'OS de sa machine hôte

- [:whale: Docker *Installation, Commandes, Docker-Compose*](/Conteneurisation/Docker)
{.links-list}
- [:package: LXC/LXD *Installation, Commandes*](/Conteneurisation/LXC_LXD)
- [Kubernetes](/Conteneurisation/Kubernetes)