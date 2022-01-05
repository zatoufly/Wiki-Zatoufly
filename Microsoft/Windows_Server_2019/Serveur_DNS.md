---
title: Serveur DNS
description: 
published: 1
date: 2022-01-05T14:02:59.396Z
tags: 
editor: markdown
dateCreated: 2022-01-05T14:02:59.396Z
---

![windows_serveur_2019-banner.png](/microsoft/windows_server_2019/windows_serveur_2019-banner.png)

# Introduction
Le Serveur DNS (Domain Name System) permet de traduire un nom domaine en adrese IP ou autres enregistrement

# Prérequis
- Une machine éxécuter Windows Server 2019
- Adresse IP fixe

# Installation

### Installater le rôle DNS
![winserv19-serveur-dns_01.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_01.jpg)

### Séléctionnez l'outil DNS
![winserv19-serveur-dns_02.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_02.jpg)

## Etendu directe

### Ajoutez une nouvelle étendu directe
![winserv19-serveur-dns_03.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_03.jpg)

### Séléctionnez Zone principale 
![winserv19-serveur-dns_04.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_04.jpg)

### Renseignez le domaine que vous souhaitez
![winserv19-serveur-dns_05.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_05.jpg)

### Créer un fichier de zone
![winserv19-serveur-dns_06.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_06.jpg)

### Désactiver les mise à jour dynamiques
![winserv19-serveur-dns_07.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_07.jpg)

### Terminer la configuration
![winserv19-serveur-dns_08.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_08.jpg)

## Etendu inversé

### Ajoutez une zone de recherche inversé
![winserv19-serveur-dns_09.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_09.jpg)

### Créer une zone principal
![winserv19-serveur-dns_10.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_10.jpg)

### Séléctionner IPv4
![winserv19-serveur-dns_11.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_11.jpg)

### Renseignez l'ID réseau
![winserv19-serveur-dns_12.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_12.jpg)

### Créer un nouveau fichier de zone
![winserv19-serveur-dns_13.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_13.jpg)

### Désactiver les mise à jour dynamiques
![winserv19-serveur-dns_14.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_14.jpg)

### Terminer la configuration
![winserv19-serveur-dns_15.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_15.jpg)

# Ajoutez un enregistrement

Il existe plusieurs type d'enregistement :

1. De type A ou AAAA pour faire pointer un sous-domaine vers une adresse IPv4 ou IPv6 respectivement
2. De type CNAME pour faire pointer le sous-domaine "www" vers la même adresse IP que votre domaine racine (exemple : zatoufly.lan)
3. De type MX pour indiquer quel serveur de messagerie Google, Hotmail, ... devront utiliser pour envoyer les mails vers vos adresses e-mails "contact@zatoufmy.lan".
4. De type TXT pour prouver à Google Analytics ou d'autres services en ligne que vous êtes bien le propriétaire de votre site

### 1. Ajoutez un enregistrement de type A
![winserv19-serveur-dns_16.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_16.jpg)

### 2. Renseignez le sous domaine et l'IP que vous souhaitez pointer
![winserv19-serveur-dns_17.jpg](/microsoft/windows_server_2019/dns/winserv19-serveur-dns_17.jpg)