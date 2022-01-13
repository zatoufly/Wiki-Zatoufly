---
title: apt
description: 
published: 1
date: 2022-01-13T12:05:00.068Z
tags: 
editor: markdown
dateCreated: 2022-01-13T12:05:00.068Z
---

# Introduction
apt ou advanced packaging Tool est un gestionnaire de paquets utilisé sous Debian.
 
# Commandes
|   commandes | |
| --- | --- |
| `apt update` | met à jour la liste des paquets disponibles |
| `apt upgrade` | met à jour les paquet du systèmes |
| `apt full-upgrade` | apt upgrade + supprimer les dépenses inutilisés / obsolètes |
| `apt search [paquet]` | cherche les paquets |
| `apt show [paquet]` | affiche les informations sur un paquet |
| `dpkg -l` | liste tout les paquets installé sur le système |
 
 
|  Installation de paquet   |     |
| --- | --- |
| `apt install [paquet]` | installer un paquet |
| `dpkg -i [ficher .deb]` | installe un paquet en .deb |
| `apt install -f` | installe les dépenses en cas d'erreur du fichier .deb |
 
 
|  Désinstallation de paquet   |     |
| --- | --- |
| `apt remove [paquet]` | désinstalle le paquet |
| `apt autoremvove [paquet]` | désinstalle le paquet et ses dépendances |
| `--purge` | supprime les fichier de configuration |
