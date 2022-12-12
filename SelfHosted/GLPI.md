---
title: GLPI
description: 
published: true
date: 2022-12-12T09:42:35.224Z
tags: docker, stack docker, glpi
editor: markdown
dateCreated: 2022-12-12T09:42:35.224Z
---

# Introduction
GLPI est un outil de gestion de parc informatique et de ticketing open source très populaire. Il est beaucoup utisiler dans le milieu de l'apprentissage.

# Installation
# Tabs {.tabset}
## Docker Compose


```yml
version: "3.2"
services:
  mariadb:
    image: mariadb:10.7
    container_name: mariadb
    hostname: mariadb
    volumes:
      - /var/lib/mysql:/var/lib/mysql
    environment:
      - MARIADB_ROOT_PASSWORD=pass
      - MARIADB_DATABASE=glpidb
      - MARIADB_USER=glpi_user
      - MARIADB_PASSWORD=glpi
    restart: always

  glpi:
    image: diouxx/glpi
    container_name : glpi
    hostname: glpi
    ports:
      - "810:80"
    volumes:
      - /etc/timezone:/etc/timezone:ro
      - /etc/localtime:/etc/localtime:ro
      - /var/www/html/glpi/:/var/www/html/glpi
    environment:
      - TIMEZONE=Europe/Paris
    restart: always
```
## Serveur LAMP
[zatoufly.fr - Installer GLPI 10 sur debian](https://zatoufly.fr/installer-glpi-10-sur-debian/)