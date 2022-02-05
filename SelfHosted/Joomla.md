---
title: Joomla
description: 
published: true
date: 2022-02-05T21:09:52.032Z
tags: 
editor: markdown
dateCreated: 2022-02-05T21:09:52.032Z
---

# Présentation
**Joomla**
 
# Installation
# Tabs {.tabset}
## Docker-Compose
```yaml
version: '3.1'

services:
  joomla:
    image: joomla
    restart: always
    links:
      - joomladb:mysql
    ports:
      - 8080:80
    environment:
      - JOOMLA_DB_HOST: joomladb
      - JOOMLA_DB_PASSWORD: p
      - JOOMLA_DB_USER: joomla

  joomladb:
    image: mysql:5.6
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD: example
      - MYSQL_PASSWORD: p 
      - MYSQL_USER: joomla 
      - MYSQL_DATABASE: joomla
```

