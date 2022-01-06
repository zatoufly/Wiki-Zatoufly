---
title: Windows Server 2019 - Serveur DHCP
description: 
published: 1
date: 2022-01-06T09:06:01.904Z
tags: 
editor: markdown
dateCreated: 2022-01-05T12:47:14.657Z
---

![windows_serveur_2019-banner.png](/microsoft/windows_server_2019/windows_serveur_2019-banner.png){.align-center}
 
 
# Présentation
Le protocole DHCP permet de fournir des adresses IP à des machines sur une plage d'ip définie par le serveur DHCP. Le Serveur DHCP fournit des adresses IP à des machines clientes sur un réseau.
 
> Faites attention à ne pas avoir deux serveurs DHCP sur votre réseau.
{.is-warning}
 
 
# Prérequis
- Machine sous Windows Server 2019
- Une adresse IP fixe
 
# Installation
 
### Ajoutez le rôle DHCP sur votre serveur
![winserv19-serveur-dhcp(1).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(1).jpg)
 
### Cliquez sur "terminer la configuration DHCP"
![winserv19-serveur-dhcp(2).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(2).jpg)
 
### Valider la post-installation DHCP
![winserv19-serveur-dhcp(3).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(3).jpg)
 
### Sélectionnez l'outil DHCP
![winserv19-serveur-dhcp(4).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(4).jpg)
 
### Créer une nouvelle étendue IPv4
![winserv19-serveur-dhcp(5).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(5).jpg)
 
### Nommez votre étendue
![winserv19-serveur-dhcp(6).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(6).jpg)
 
### Renseignez une plage d'IP ainsi que le masque de sous-réseau souhaité
![winserv19-serveur-dhcp(7).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(7).jpg)
 
### Ajoutez des exclusions si besoin
![winserv19-serveur-dhcp(8).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(8).jpg)
 
### Définissez la durée du bail DHCP
![winserv19-serveur-dhcp(9).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(9).jpg)
 
### Configurez le serveur maintenant
![winserv19-serveur-dhcp(10).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(10).jpg)
 
### Renseignez votre passerelle 
![winserv19-serveur-dhcp(11).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(11).jpg)
 
### Renseignez vos serveur DNS
![winserv19-serveur-dhcp(12).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(12).jpg)
 
### Renseignez des serveurs WINS si besoin
![winserv19-serveur-dhcp(13).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(13).jpg)
 
### Activer votre étendu
![winserv19-serveur-dhcp(14).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(14).jpg)
 
### Vérifier le fonctionnement de votre serveur DHCP avec une machine cliente
![winserv19-serveur-dhcp(15).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(15).jpg)
 
### Vérifier qu'un bail à été enregistrés pour la machine cliente 
![winserv19-serveur-dhcp(16).jpg](/microsoft/windows_server_2019/dhcp/winserv19-serveur-dhcp(16).jpg)
 
> Félicitation, votre serveur DHCP est configurée et fonctionnel
{.is-success}
