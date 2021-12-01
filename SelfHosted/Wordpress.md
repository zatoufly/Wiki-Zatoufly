---
title: Wordpress
description: 
published: 1
date: 2021-12-01T21:59:11.694Z
tags: 
editor: markdown
dateCreated: 2021-12-01T21:59:11.694Z
---


![wordpress-banner.png](/wiki-assets/wordpress-banner.png)
# Présentation
**Wordpress** on ne le présente plus, le CMS le plus populaire de ces dernières années, il fait tourné la moitié des site web qui existe. ça réputation n'est pas volée car grâce à ses nombreux thèmes et plugins, il est extrênement modulaire. Vous pourrez faire à peu prêt n'importe quel projet avec cette solution.

Il a le sérieux avantage d'avoir une très grande communauté, également francophone. vous trouverez toujours un tutoriel pour arrivez à vos fin.



C'est la solution que j'utilise pour créer des sites.

Site officiel : [wordpress.org](https://wordpress.org)

# Installation
## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
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
