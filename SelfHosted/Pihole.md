---
title: Pihole
description: 
published: true
date: 2022-10-01T20:14:12.137Z
tags: 
editor: markdown
dateCreated: 2022-01-18T11:59:52.672Z
---

![pihole-banner.png](/wiki-assets/pihole-banner.png){.align-center}

# Présentation
**Pihole** est un serveur de DNS avec une interface web, son principal atout est le filtrage de domaine, en d'autre termes il permet de bloquer les pubs, trackers, etc .. Vous pouvez y ajouter des enregistrements de type A, AAAA et CNAME. 

Il peut aussi être utilisé comme serveur DHCP.

Site officiel : [pi-hole.net](https://pi-hole.net/)

# Installation
# Tabs {.tabset}
## Bare Metal

Connectez vous au serveur et installer l'outil curl pour récupérer le script d'installation officiel de pihole

```bash
apt install curl -y
```

Ensuite on récupère le script

```bash
cd /tmp
curl -sSL https://install.pi-hole.net | bash
```

Le script devrait automatiquement s'exécuter. Plus tard, pihole affiche un message d'avertissement puis un autre pour vous donner un lien si vous souhaitez effectuer des donations au projet.

![pihole-installation-1.jpg](/self-hosted/pihole/pihole-installation-1.jpg =60%x)

![pihole-installation-2.jpg](/self-hosted/pihole/pihole-installation-2.jpg =60%x)

Un message pour vous avertir que pihole à besoin d'une adresse ip statique pour correctement fonctionner. 

![pihole-installation-3.jpg](/self-hosted/pihole/pihole-installation-3.jpg =60%x)

Ensuite sélectionnez quel provider DNS vous souhaitez utiliser pour ma part je prends Quad 9

![pihole-installation-4.jpg](/self-hosted/pihole/pihole-installation-4.jpg =60%x)

Pihole vous fournit une blacklist de DNS par défaut, garder là pour filtrer les pubs de votre réseau.

![pihole-installation-5.jpg](/self-hosted/pihole/pihole-installation-5.jpg =60%x)

Activer ou non l'interface web, je vous conseille de l'activer.

![pihole-installation-6.jpg](/self-hosted/pihole/pihole-installation-6.jpg =60%x)

Installer le serveur web lighttpd pour que l'interface web fonctionne.

![pihole-installation-7.jpg](/self-hosted/pihole/pihole-installation-7.jpg =60%x)

Ici sélectionnez si vous souhaitez avoir les logs ou non, je vous conseille de les désactiver si vous avez installé pihole sur une carte SD, pour éviter de trop l'user à terme

![pihole-installation-8.jpg](/self-hosted/pihole/pihole-installation-8.jpg =60%x)

Sélectionnez la politique de "vie privée" que vous souhaitez donner à pihole.

![pihole-installation-9.jpg](/self-hosted/pihole/pihole-installation-9.jpg =60%x)		

Pihole va terminer sa configuration et vous affichera quelques informations utiles comme le mot de passe de l'interface web.

![pihole-installation-10.jpg](/self-hosted/pihole/pihole-installation-10.jpg =60%x)

Maintenant rendez-vous sur votre navigateur pour accéder à l'interface web de pihole à l'adresse http://ip-serveur/admin

![pihole-installation-11.jpg](/self-hosted/pihole/pihole-installation-11.jpg =80%x)

> Félicitations, vous avez installé pi-hole sur votre réseau !
{.is-success}


## Docker-Compose
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
      - '/path/to/etc-pihole:/etc/pihole/'
      - '/path/to/etc-dnsmasq.d:/etc/dnsmasq.d/'
    cap_add: # recommandé si utilisation du dhcp
      - NET_ADMIN
    restart: unless-stopped
```
> Pour des raisons de sécurité, changer le port de l'interface web ainsi que le mot de passe.
> Si vous ne comptez pas utiliser pihole en tant que dhcp, enlever le port 67 de la configuration.
{.is-warning}
## Docker cli
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
> Si vous ne comptez pas utiliser pihole en tant que dhcp, enlever le port 67 de la configuration.
{.is-warning}

# Configurations 

## Changer mot de passe

Pour changer de mot de passe tapez la commande suivante sur le serveur où est installé pihole :

```bash
pihole -a -p
```
## Mettre à jour

```bash
pihole -up
```