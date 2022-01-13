---
title: Apache 2
description: 
published: 1
date: 2022-01-13T11:28:13.247Z
tags: 
editor: markdown
dateCreated: 2022-01-13T10:57:01.707Z
---

# Présentation
Apache2 est un serveur HTTP. Il est produit par la *Apache Software Foundation*, c'est un logiciel libre et open source.
 
On l'utilise généralement avec d'autres logiciels (base de données, interpréteur de code) pour constituer un serveur LAMP ou des variantes.
 
# Installation
# Tabs {.tabset}
## Debian
```bash
apt install apache2
```
 
## RHEL
```bash
dnf install apache2
```
# Configuration
Le fichier de configuration se trouve dans `/etc/apache2/apache2.conf`
 
## Cacher la version d'apache dans l'erreur forbidden
Dans le fichier apache2.conf, ajoutez cette ligne :
```bash
ServerTokens Prod
```
Rechargez apache avec <kbd>systemctl reload apache2</kbd>
 
 
# Commandes
|     |     |
| --- | --- |
| `a2ensite` | active un hôte virtuel  |
| `a2dissite` | désactiver un hôte virtuel |
| `apache2ctl -v` | affiche la version d'apache |
| `apache2ctl -t` | test de configuration d'apache |
| `apache2ctl -M` | Voir les modules d'apache chargés |
| `apache2ctl disable/enable apache2` | désactiver/active apache2 au démarrage du système |
| `a2enmod / a2dismod ` | Active ou désactive un module |
 
# Virtual Host
Les virtual host ou hôte virtuel permet de configurer plusieurs sites sur un même serveur. Châque hôte virtuel peut être basé sur un nom de domaine ou basé sur un port. Il dispose également d'un dossier racine où est situé le site.
 
## Configuration
Le virtual host de natif ce situe dans /etc/apache2/sites-available/000-default.conf
 
Répertoires :
- **/etc/apache2/sites-available** -> site disponibles
- **/etc/apache2/sites-enable** -> site actifs
 
Copier le et éditez le :
```bash
cd /etc/apache2/sites-available
cp 000-default.conf site1.conf
vim /glpi.conf
```
 
Votre fichier doit contenir ces informations :
 
```html
<VirtualHost *:80> # port d'écoute du virtual host
 
  ServerName : site1.domaine.org  # nom de domaine
  DocumentRoot : /var/www/site1 # dossier racine du site
 
</VirtualHost>
```
 
Enregistrez le virtual host, et activez le avec :
```bash
a2ensite site1.conf
systemctl reload apache2
```
Oubliez pas de recharger apache2
 
## Bloquer l'accès au site via l'IP
```html
<VirtualHost *:80>
        ServerName IP_DU_SERVEUR
 
        <Directory />
                Deny from all
        </Directory>
</VirtualHost>
```