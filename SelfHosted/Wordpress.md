---
title: Wordpress
description: 
published: 1
date: 2022-01-14T11:14:34.244Z
tags: 
editor: markdown
dateCreated: 2021-12-01T21:59:11.694Z
---

 
![wordpress-banner.png](/wiki-assets/wordpress-banner.png)
# Présentation
**Wordpress** On ne le présente plus, le CMS le plus populaire de ces dernières années, il fait tourner la moitié des sites web qui existent. Sa réputation n'est pas volée car grâce à ses nombreux thèmes et plugins, il est extrêmement modulaire. Vous pourrez faire à peu prêt n'importe quel projet avec cette solution.
 
Il a le sérieux avantage d'avoir une très grande communauté, également francophone. Vous trouverez toujours un tutoriel pour arriver à vos fins.
 
 
 
C'est la solution que j'utilise pour créer des sites.
 
Site officiel : [wordpress.org](https://wordpress.org)
 
# Installation
# Tabs {.tabset}
 
## Serveur dédié
 
Dans ce tutoriel :
 
J’effectue l’installation sur une debian 11 
Je serais en utilisateur root
J’utilise l’éditeur de texte vim
J’installe Wordpress 5.8
 
### Prérequis
- Serveur LAMP
- Adresse ip fixe
 
### Installation de Wordpress
 
Avant de commencer, on met à jour nos dépôt et notre système.
 
```bash
apt update && apt full-upgrade -y
```
 
On télécharge Wordpress et on le décompresse dans /var/www
 
```bash
cd /tmp
wget https://wordpress.org/latest.tar.gz
tar xvf latest.tar.gz -C /var/www
```
 
Ensuite je donne les permissions à apache sur wordpress
 
```bash
chown -R www-data.www-data /var/www/html/wordpress/
```
 
### Création de la base de données
 
On va créer une base de données avec un utilisateur qui aura les permission sur cette dernière
 
```bash
mysql -u root
```
 
Dans la console de mariadb :
 
```SQL
create database wordpress;
create user ‘votreuser’@’localhost’ identified by ‘votremdp’;
grant all privileges on wordpress. * to ‘zatoufly’@’localhost’;
flush privileges;
exit;
```
 
Je modifie le fichier de conf "wp-config" pour renseigner notre base de données précédemment créée.
 
```bash
cd /var/www/html/wordpress
mv wp-config-sample.php wp-config.php
vim wp-config.php
```
 
remplacez :
- database_name_here -> le nom de la base de données
- username_here -> le nom de l'utilisateur SQL
- password_here -> le mot de passe de l'utilisateur SQL
 
Enregistrez le fichier.
 
### Création du Virtual Host
 
Pour ce faire, on va créer un fichier de conf et le remplir avec nos informations
 
```bash
vim /etc/apache2/sites-available/wordpress.conf
```
 
On va y mettre :
```
<VirtualHost *:80>
 
        DocumentRoot "/var/www/wordpress/"
        ServerName domain.com
 
        ErrorLog ${APACHE_LOG_DIR}/nextcloud.error
        CustomLog ${APACHE_LOG_DIR}/nextcloud.access combined
 
</VirtualHost>
```
 
ServerName : permet de donner à apache2 le nom de domaine ou sous-domaine
DocumentRoot : indique l’emplacement de notre site sur la machine
Les 2 autres lignes, servent à indiquer l’emplacement de nos log
 
> Oubliez pas d'ajouter un enregistrement de type A sur votre hébergement DNS
{.is-warning}
 
### Configuration de Wordpress
 
Sur votre navigateur allez à l’adresse de votre site.
 
Ici je sélectionne la langue souhaité 
 
![wordpress-1.png](/self-hosted/wordpress/wordpress-1.png)
 
Et je renseigne quelques informations, et je retiens bien de mdp fournis, il nous servira pour se connecter à wordpress.
 
![wordpress-2.png](/self-hosted/wordpress/wordpress-2.png)
 
 
## Docker-Compose 
```yaml
---
version: "2"
 
services:
   wordpress-db:
     container_name: wordpress-db
     image: mysql:5.7
     volumes:
       - /path/to/db:/var/lib/mysql
     restart: unless-stopped
     environment:
       MYSQL_ROOT_PASSWORD: root-password
       MYSQL_DATABASE: wordpress
       MYSQL_USER: utilisateur
       MYSQL_PASSWORD: password
 
   wordpress:
     container_name: wordpress
     depends_on:
       - wordpress-db
     image: wordpress:latest
     ports:
       - 80:80
     restart: unless-stopped
     volumes:
       - /path/to/uploads.ini:/usr/local/etc/php/conf.d/uploads.ini
       - /path/to/html:/var/www/html
     environment:
       WORDPRESS_DB_HOST: wordpress-db:3306
       WORDPRESS_DB_USER: utilisateur
       WORDPRESS_DB_PASSWORD: password
       WORDPRESS_DB_NAME: wordpress
```
 
# Sécurisé le serveur HTTP
> Une fois que wordpress à été initialiser 
{.is-warning}
 
Vous pouvez donner des permissions plus restrictives sur wordpress.
```bash
chmod 400 /var/www/html/wordpress/config.php
```
 
# Astuces
## Masquer le badge recaptcha
Si vous utilisez le service ReCaptcha v3 de google qui permet de se prémunir des spam sur les formulaires de contact, vous avez un badge qui s’affiche.
 
Il est possible de le faire disparaître selon les règles émissent par google :
 
- Avoir une mention visible dans la page du formulaire le lien vers la politique de confidentialité et les conditions d'utilisations :
Vous pouvez ajoutez ce texte par exemple avec les liens hypertextes :
 
Ce site est protégé par reCAPTCHA. La politique de confidentialité et les conditions d'utilisation de Google s'appliquent.
 
+ Mettre le lien suivant sur "politique de confidentialité" : https://policies.google.com/privacy
+ Mettre le lien suivant sur "conditions d'utilisation" : https://policies.google.com/terms
 
Pour faire disparaître le badge, ajouté ce code CSS dans votre thème :
```bash
.grecaptcha-badge { opacity:0;}
```