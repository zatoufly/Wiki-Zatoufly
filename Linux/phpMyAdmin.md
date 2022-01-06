---
title: phpMyAdmin
description: 
published: 1
date: 2022-01-06T09:57:32.311Z
tags: 
editor: markdown
dateCreated: 2022-01-06T09:57:32.311Z
---

# Introduction
phpMyAdmin permet de gérer ses bases de données SQL, ainsi que de les exporter et importer avec une grande facilité via son interface web.
 
# Prérequis
- Un serveur LAMP
- Adresse IP fixe
 
> **J'effectue ce tuto** :
> -> Sur une debian 11
> -> en utilisateur root
> -> avec phpMyAdmin 5.1.1
{.is-info}
 
# Installation
 
### Mettez à jour vos dépôts et la machine
```bash
apt update && apt full-upgrade -y
```
 
### Installer les dépendances
```bash
apt install php-mysqli php-mbstring php-xml
```
 
### Télécharger phpMyAdmin
> La dernière version ce trouve ici  :https://phpmyadmin.net/downloads
{.is-info}
 
```bash
cd /tmp
wget files.phpmyadmin.net/phpMyAdmin/5.1.1/phpMyAdmin-5.1.1-all-languages.tar.gz
```
 
### Dézipper et déplacer phpMyAdmin dans /var/www/html
```bash
tar xvf phpMyAdmin-5.1.1-all-languages.tar.gz
mv phpMyAdmin-5.1.1-all-languages phpMyAdmin
mv phpMyAdmin /var/www/html
```
 
### Attribuer les droits à apache sur phpMyAdmin
```bash
chown -R www-data:www-data /var/www/html/phpMyAdmin
```
 
### Supprimer l'archive
```bash
rm -fr /tmp/phpMyAdmin-5.1.1-all-languages.tar.gz
```
 
> Pour vous connecter utilisez un utilisateur SQL
{.is-info}
 
> Félicitation, phpMyAdmin est installé. vous pouvez vous connecter à : http://votre-ip/phpMyAdmin
{.is-success}