---
title: Pihole
description: 
published: 1
date: 2021-12-12T09:37:51.660Z
tags: 
editor: markdown
dateCreated: 2021-12-05T09:39:39.388Z
---

![pihole-banner.png](/wiki-assets/pihole-banner.png){.align-center}

# Présentation
**Pihole** est un serveur de DNS avec une interface web, son principal atout est le filtrage de domaine, en d'autre termes il permet de bloquer les pubs, trackeurs, etc .. Vous pouvez y ajoutez des enregistrements de type A, AAAA et CNAME. 

Il peut être aussi utilisez comme serveur DHCP.

Site officiel : [pi-hole.net](https://pi-hole.net/)

# Installation
## Bare Metal

Connecetez vous au serveur et installer l'outils curl pour récupèrer le script d'installation officiel de pihole

```bash
apt install curl -y
```

Ensuite on récupère le script

```bash
cd /tmp
curl -sSL https://install.pi-hole.net | bash
```

Le script devrait automatiquement s'éxécute. Plus tard pihole affiche un message d'avertissement puis un autre pour vous donner un lien si vous souhaiter effectuer des donation au projet.

MEDIA

MEDIA

Un message pour vous avertir que pihole à besoin d'une adresse ip static pour correctement fonctionner. 

MEDIA

Ensuite séléctionnez quel provider DNS vous souhaitez utilisén pour ma part je prend Quad9

MEDIA

Pihole vous fournit une blacklist de DNS par défaut, garder là pour filtrer les pubs de votre réseau.

MEDIA

Activer ou non l'interface web, je vous conseille de l'activer.

MEDIA

Installer le serveur web lighttpd pour que l'interface web fonctionne.

MEDIA

Ici séléctionnez si vous souhaitez avoir les log ou non, je vous conseille de les désactiver si vous avez installer pihole sur une carte SD, pour éviter de trop l'user à terme

MEDIA

Séléctionnez la politique de "vie privée" que vous souhaiter donner à pihole.

MEDIA		

Pihole va terminer sa configuration et vous affichera quelques informations utiles comme le mot de passe de l'interface web.

MEDIA

Maintenant rendez vous sur votre navigateur pour accéder à l'interface web de pihole à l'addresse http://ip-serveur/admin

MEDIA

> Félicitations, vous avez installer pi-hole sur votre réseau !
{.is-success}


## Docker-Compose ([Plus d'informations](https://docs.linuxserver.io/general/docker-compose))
```yaml
version: "3"

services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp" # dns
      - "53:53/udp" # dns
      - "67:67/udp" # dhcp
      - "80:80/tcp" # interface web
    environment:
      TZ: 'Europe/Paris'
      WEBPASSWORD: 'password' # mot de passe de l'interface web
    volumes:
      - '/path/to//etc-pihole:/etc/pihole/'
      - '/path/to/etc-dnsmasq.d:/etc/dnsmasq.d/'
		cap_add: # recommandé si utilisation du dhcp
      - NET_ADMIN
    restart: unless-stopped
```
## Docker cli ([Plus d'informations](https://docs.docker.com/engine/reference/commandline/cli/))
```bash
docker run -d \
  --name pihole \
  -e TZ Europe/Paris \
  -e WEBPASSWORD 'password' \
  -p 53:53/tcp `# dns` \
  -p 53:53/udp `# dns` \
  -p 67:67/ucp `# dhcp` \
  -p 80:80/tcp `# interface web` \
  -v /path/to/etc-pihole:/etc/pihole \
  -v /path/to/etc-dnsmasq.d:/etc/dnsmasq.d \
  --restart unless-stopped \
  pihole/pihole:latest
```
> Pour des raisons de sécurité, changer le port de l'interface web ainsi que le mot de passe.
> Si vous comptez pas utiliser pihole en tant que dhcp, enlever le port 67 de la configuration
{.is-warning}

# Configurations 

## Changer mot de passe

Pour changer de mot de passe tappez la commande suivante sur le serveur où est installer pihole :

```bash
pihole -a -p
```