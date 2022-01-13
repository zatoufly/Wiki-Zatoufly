---
title: MariaDB
description: 
published: 1
date: 2022-01-13T11:44:24.602Z
tags: 
editor: markdown
dateCreated: 2022-01-13T11:44:24.602Z
---

# Introduction
MariaDB est un serveur de base de données généralement utilisé pour dans serveur LAMP.
 
# Installation
# Tabs {.tabset}
## Debian
```bash
apt install mariadb-server
```
 
## RHEL
```bash
dnf install mariadb-server
```
 
# Commandes
 
|     |     |
| --- | --- |
| `create database test;` | créer une base de données |
| `show databases` | Affiche la liste des base de données |
| `create user test@localhost identified by 'p';` | Créer un utilisateur avec son mdp |
| `grant all privileges on test.* to test@localhost;` | Donne toutes les permissions à un utilisateur sur une base |
 
# mariadb-secure-installation
mariadb-secure-installation est un script à exécuter pour toutes installations de mariadb destinée à la production, cela permet de sécuriser votre serveur SQL.
 
lancer le script :
```bash
mariadb-secure-installation
```
répondez au question (voici un très bref résumé de ce qui est demandé): 
```
Demande d'entrer le mdp admin si il y a un 
unix_socket → n
Définit le mdp root de mariadb → y
Remove anonymous user → y
Disallow root login → y
Remove test database → y
Validation → y
```
