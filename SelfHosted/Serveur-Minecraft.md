---
title: Serveur Minecraft
description: 
published: 1
date: 2021-12-26T13:18:21.401Z
tags: 
editor: markdown
dateCreated: 2021-12-26T09:27:00.078Z
---

![minecraft-logo.png](/self-hosted/minecraft/minecraft-logo.png =400x){.align-center}
 
# Présentation
Le serveur de jeu minecraft vous permet d'avoir un serveur sur lequel jouer avec vos amis. Tout ça hébergé en local
 
# Prérequis
Dans ce tutoriel, je serais en utilisateur root sur une Debian 11.
- Une adresse ip fixe
- Une machine assez puissante (je recommande 4Go de ram et 2 cores cpu strict minimum)
- Un disque assez volumineux (100Go pour être large) pour stocker la map
 
# Installation
### Mettez à jour votre système
```bash
apt update && apt full-upgrade -y
```
### Installer Java
```bash
apt install openjdk-17-jdk -y
```
 
### Créer un utilisateur minecraft
```bash
adduser minecraft
usermod -aG sudo minecraft
```
 
### Créer un répertoire pour y stocker le serveur
```bash
mkdir /srv/minecraft
cd /srv/minecraft
```
 
### Télécharger Minecraft 
```bash
wget https://launcher.mojang.com/v1/objects/125e5adf40c659fd3bce3e66e67a16bb49ecc1b9/server.jar
```
> Dernière version disponible ici : https://www.minecraft.net/fr-fr/download/server
{.is-info}
 
### Créer un script de démarrage
```bash
vim start.sh
chmod +x start.sh
```
Contenue du fichier :
```bash
java -Xms1024M -Xmx2048M -jar server.jar nogui # Changez Xmx pour augmenter la RAM alloué à minecraft
```
 
### Initier votre serveur
```bash
./start.sh
```
 
### Acceptez la EULA
```bash
vim eula.txt
```
> Remplacez <kbd>false</kbd> par <kbd>true</kbd> 
{.is-info}
 
### Lancer votre serveur minecraft
```bash
./start.sh
```
 
> Votre serveur est configuré, vous pouvez y accéder en ajoutant un serveur à votre client minecraft à avec **votre-ip:25565** 
{.is-success}
 
# Configurations
## Commandes utiles
|     |     |
| --- | --- |
| `stop` | Arrête le serveur minecraft |
| `op zatoufly` | donne les droit administrateur à l'utilisateur zatoufly |