---
title: Nginx Proxy Manager
description: 
published: 1
date: 2021-12-01T08:50:36.145Z
tags: 
editor: markdown
dateCreated: 2021-12-01T08:50:36.145Z
---

![banner-nginx-reverse-proxy.png](/wiki-assets/banner-nginx-reverse-proxy.png)

# Présentation
**Nginx Proxy Manager** est un manager de reserve proxy, celà permet de publier un service SelfHoted sur Internet. Son fonctionnement est plutôt simple grâce à son interface web.

Il communique directement avec Let's Encrypt, afin de pouvoir fournir à vos services un certificat SSL gratuitement. 



Site officiel : [nginxproxymanager.com](https://nginxproxymanager.com/)


# Installation

## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```
version: '3'
services:
  nginx:
    image: 'jc21/nginx-proxy-manager:latest'
    container_name: nginx
    ports:
      - '80:80'
      - '81:81'
      - '443:443'
    restart: unless-stopped
    environment:
      DB_MYSQL_HOST: "db"
      DB_MYSQL_PORT: 3306
      DB_MYSQL_USER: "utilisateur"
      DB_MYSQL_PASSWORD: "mdp"
      DB_MYSQL_NAME: "nginx"
    volumes:
      - <path to data>:/data
      - < path to letsencrypt>:/etc/letsencrypt
    depends_on:
      - db
  db:
    image: 'jc21/mariadb-aria:latest'
    container_name: nginx-db
    restart: unless-stopped
    environment:
      MYSQL_ROOT_PASSWORD: 'npm'
      MYSQL_DATABASE: 'nginx'
      MYSQL_USER: 'utilisateur'
      MYSQL_PASSWORD: 'mdp'
    volumes:
      - <path to mysql>:/var/lib/mysql
```

> N'oubliez pas de changer les paramètres MYSQL pour des raisons de sécurité
{.is-warning}

> Veuillez ne pas modifier les ports 80 et 443, ces derniers sont nécessaires au bon fonctionnement du reverse proxy.
Ces ports doivent être ouvert vers la machine hôte pour pouvoir communiquer avec Internet. 
{.is-info}

# Configurations
Vous pouvez vous connecter à son interface via la port 81
Les identifiants par défaut de nginx proxy manager sont :
```
Email:    admin@example.com
Password: changeme
```
## Ajoutez un hôte
Pour ajoutez un Hôte, cliquez sur "Hosts" puis "Proxy Hosts"
Ici cliquez sur "Add Proxy Host"

Le nom de domaine indiquez dans "Domain Names" devra être enregistrez chez un fournisseur et devra pointez sur votre ip public.

|     |     |
| --- | --- |
| `Domain Names` | Indiquez votre nom de domaine ou sous-domaine |
| `Scheme` | Mettez y le protocole que votre application utilise |
| `Forward Hostname / IP` | Indiquez votre IP Public |
| `Forward Port` | Incrivez le port que votre service utilise |

![nginx-proxy-manager-host2.jpg](/wiki-assets/nginx-proxy-manager-host2.jpg)

Ensuite dans l'onglet "SSL"

|     |     |
| --- | --- |
| `SSL Certificate` | Séléctionnez "Let's Encrypt pour bénéficier d'un certificat SSL |
| `Force SSL` | Cochez pour redirigez les requêtes http en https |
| `Email Address for Let's Encrypt` | Indiquez un e-mail pour savoir quand le certificat expire |

Acceptez les termes d'utilisation de Let's Encrypt et cliquez sur "Save" pour ajoutez votre Hôte 

![nginx-proxy-manager-host1.jpg](/wiki-assets/nginx-proxy-manager-host1.jpg)





