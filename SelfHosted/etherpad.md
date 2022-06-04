---
title: EtherPad
description: 
published: true
date: 2022-06-04T16:18:54.615Z
tags: 
editor: markdown
dateCreated: 2022-06-04T16:18:54.615Z
---

# Introduction
Etherpad est un bloc-note collaboratif open source et hébergeable sur ses serveurs. 

# Installation
# Tabs {.tabset}
## Docker Compose
```yml
version: '3.3'
services:
  etherpad:
    container_name: etherpad
    ports:
        - '9001:9001'
    environment:
      DB_TYPE: postgres
      DB_HOST: db
      DB_PORT: 5432
      DB_NAME: etherpad
      DB_USER: user
      DB_PASS: mdp
      DEFAULT_PAD_TEXT: Bienvenue sur etherpad ! # texte par defaut à la création d'un bloc-note
      TITLE: Etherpad # Titre de l'instance
      ADMIN_PASSWORD: admin # mot de passe de la page d'administration
    restart: always
    image: etherpad/etherpad
    
  db:
    image: postgres:11-alpine
    environment:
      POSTGRES_DB: etherpad
      POSTGRES_PASSWORD: mdp
      POSTGRES_USER: user
    logging:
      driver: "none"
    restart: always
    volumes:
      - /srv/docker/etherpad/db:/var/lib/postgresql/data
```