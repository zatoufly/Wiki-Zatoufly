---
title: Nextcloud
description: 
published: 1
date: 2022-01-13T11:48:08.951Z
tags: 
editor: markdown
dateCreated: 2021-12-20T21:35:31.512Z
---

![nextcloud_logo.svg.png](/self-hosted/nextcloud/nextcloud_logo.svg.png =300x){.align-center}
 
# Présentation
Nextcloud est un projet open source qui permet littéralement d'avoir un OneDrive ou Google Drive hébergé chez soi, on le combine très souvent avec un NAS.
 
C'est une solution très complète et stable, il propose beaucoup d'intégration mais également un client mail, agenda, contact, éditeur de texte et de la synchronisation de photos et fichiers sur tous les systèmes d'exploitation.
 
Site officiel : [nextcloud.com](https://nextcloud.com/)
 
# Installation
# Tabs {.tabset}
## Bare Metal
 
### Prérequis
Dans ce tutoriel, je serais en utilisateur root sur une Debian 11. j'installe la version 23 de nextcloud.
 
> Il vous faudra une adresse ip fixe sur votre machine
{.is-warning}
 
### Installation du serveur LAMP
Mettez à jour vos dépôts.
```bash
apt update && apt upgrade -y
```
Ensuite installer apache2, mariadb ainsi que php et quelques extensions requises pour nextcloud.
```bash
apt install apache2 mariadb-server php php-imagick php-common php-mysql php-fpm php-gd php-json php-curl  php-zip php-xml php-mbstring php-bz2 php-intl php-bcmath php-gmp -y
```
 
### Installation de nextcloud
 
On télécharge les fichiers de nextcloud
```bash
cd /tmp
wget https://download.nextcloud.com/server/releases/nextcloud-23.0.0.zip
```
 
Installer unzip et décompresser l'archive dans /var/wwww
```bash
apt install unzip -y
unzip nextcloud-23.0.0.zip -d /var/www/
```
 
Donner les permissions à apache sur l'installation de nextcloud
 
```bash
chown -R www-data:www-data /var/www/nextcloud
```
 
### Configuration de MariaDB
Ici, j’utilise MariaDB pour la partie base de données (SQL). On va créer une base de données, un utilisateur et lui attribuer les droits sur cette base de données.
 
```bash
mysql -u root
```
 
Dans le terminal de MariaDB :
 
```SQL
create database nextcloud;
create user nextcloud@localhost identified by ‘motdepasse’;
grant all privileges on nextcloud.* to nextcloud@localhost;
flush privileges;
exit 
```
 
### Création du virtual host
 
Créer un fichier nextcloud.conf dans /etc/apache2/sites-available/
 
Remplacez nextcloud.exemple.com par votre sous-domaine.
 
Oubliez pas de créer un enregistrement de type A pour ce sous domaine dans votre éditeur de zone DNS (OVH pour ma part)
 
```bash
vim /etc/apache2/sites-available/nextcloud.conf
```
 
Dans ce fichier, mettez y la configuration ci-dessous (en modifiant ServerName)
 
```bash
<VirtualHost *:80>
 
        DocumentRoot "/var/www/nextcloud"
        ServerName nextcloud.example.com
 
        ErrorLog ${APACHE_LOG_DIR}/nextcloud.error
        CustomLog ${APACHE_LOG_DIR}/nextcloud.access combined
 
        <Directory /var/www/nextcloud/>
            Require all granted
            Options FollowSymlinks MultiViews
            AllowOverride All
 
           <IfModule mod_dav.c>
               Dav off
           </IfModule>
 
        SetEnv HOME /var/www/nextcloud
        SetEnv HTTP_HOME /var/www/nextcloud
        Satisfy Any
 
       </Directory>
 
</VirtualHost>
```
 
Une fois le fichier enregistrez, activer le virtual host :
 
```bash
a2ensite nextcloud.conf
systemctl reload apache2
```
 
## Docker-Compose
 
## Docker cli
 
# Astuces
En cas de perte d'un mot de passe, vous pouvez réinitialiser avec cette commande : 
```bash
sudo -u www-data php /var/www/nextcloud/occ user:resetpassword utilisateur
```
