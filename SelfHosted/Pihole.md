---
title: Pihole
description: 
published: 1
date: 2021-12-05T09:39:39.388Z
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
- à venir
{.links-list}
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
  -p 53:53/tcp \ # dns 
  -p 53:53/udp \ # dns 
  -p 67:67/ucp \ # dhcp 
  -p 80:80/tcp \ # interface wen 
  -v /path/to/etc-pihole:/etc/pihole \
  -v /path/to/etc-dnsmasq.d:/etc/dnsmasq.d \
  --restart unless-stopped \
  pihole/pihole:latest
```
> Pour des raisons de sécurité, changer le port de l'interface web ainsi que le mot de passe.
> Si vous comptez pas utiliser pihole en tant que dhcp, enlever le port 67 de la configuration
{.is-warning}

# Configurations  