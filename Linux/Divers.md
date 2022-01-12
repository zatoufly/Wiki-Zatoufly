---
title: Divers
description: 
published: 1
date: 2022-01-12T21:57:31.121Z
tags: 
editor: markdown
dateCreated: 2021-12-12T16:07:15.890Z
---

## Ajoutez des variables PATH
Pour ajouter une variable PATH, éditez le fichier ~/.bashrc
ajoutez y les variables, exemples :
```bash
export PATH=$PATH:/usr/local/sbin
export PATH=$PATH:/usr/sbin
export PATH=$PATH:/sbin
```
 
## Installer GNOME
J'effectue ce tutoriel sur une debian.
 
Mettez à jour votre machine
```bash
apt update && apt full-upgrade
```
 
installer gnome
```bash
tasksel install desktop gnome-desktop
```
 
Ajoutez les outils pour les pc portables :
```bash
tasksel install laptop
```
 
démarrer l'environnement gnome par défaut :
```bash
systemctl set-default graphical.target
```
 
redémarrer votre machine :
```bash
reboot
```
 
## Supprimer GNOME
supprimer les paquet de gnome :
```bash
tasksel remove desktop gnome-desktop laptop
```
 
mettez le démarrer en mode CLI par défaut :
```bash
systemctl set-default multi-user.target
```