---
title: XenServer - Installation
description: 
published: 1
date: 2022-01-05T11:46:52.543Z
tags: 
editor: markdown
dateCreated: 2022-01-05T11:46:52.543Z
---

![logo_xenserver.png](/virtualisation/xenserver/logo_xenserver.png =400x){.align-center}
 
# Introduction
XenServer est l'hyperviseur de chez Citrix.
 
Dans ce tutoriel, je l'installe en version 7.
 
# Prérequis
- l'image ISO de XenServer : https://www.citrix.com/downloads/citrix-hypervisor/product-software/xenserver-70-standard-edition.html
- Activer la virtualisation dans le BIOS
 
# Installation VMware ESXi
 
### Faites booter votre machine sur l'ISO d'ESXi
![xenserveur-installation-1.jpg](/virtualisation/xenserver/xenserveur-installation-1.jpg)
 
### Sélectionnez la langue de votre clavier
![xenserveur-installation-2.jpg](/virtualisation/xenserver/xenserveur-installation-2.jpg)
 
### Sélectionnez "OK"
![xenserveur-installation-3.jpg](/virtualisation/xenserver/xenserveur-installation-3.jpg)
 
### Acceptez la EULA
![xenserveur-installation-4.jpg](/virtualisation/xenserver/xenserveur-installation-4.jpg)
 
### Confirmer que la virtualisation à bien été activer dans votre BIOS
![xenserveur-installation-5.jpg](/virtualisation/xenserver/xenserveur-installation-5.jpg)
 
### Sélectionnez le disque où sera installé XenServer
![xenserveur-installation-6.jpg](/virtualisation/xenserver/xenserveur-installation-6.jpg)
 
### Sélectionnez le source du média d'installation
![xenserveur-installation-7.jpg](/virtualisation/xenserver/xenserveur-installation-7.jpg)
 
### Installer des paquets supplémentaires
![xenserveur-installation-8.jpg](/virtualisation/xenserver/xenserveur-installation-8.jpg)
 
### Vérifiez si le média d'installation n'est pas corrompue
![xenserveur-installation-9.jpg](/virtualisation/xenserver/xenserveur-installation-9.jpg)
 
### Créer un mot de passe
![xenserveur-installation-10.jpg](/virtualisation/xenserver/xenserveur-installation-10.jpg)
 
### Configurez votre interface RJ45
![xenserveur-installation-11.jpg](/virtualisation/xenserver/xenserveur-installation-11.jpg)
 
### Renseignez vos serveurs DNS
![xenserveur-installation-12.jpg](/virtualisation/xenserver/xenserveur-installation-12.jpg)
 
### Renseignez vos serveur NTP
![xenserveur-installation-13.jpg](/virtualisation/xenserver/xenserveur-installation-13.jpg)
 
### Confirmer l'installation
![xenserveur-installation-14.jpg](/virtualisation/xenserver/xenserveur-installation-14.jpg)
 
### Installation ou non des paquets supplémentaires
![xenserveur-installation-15.jpg](/virtualisation/xenserver/xenserveur-installation-15.jpg)
 
### Voici l'interface d'administration de XenServer
![xenserveur-installation-16.jpg](/virtualisation/xenserver/xenserveur-installation-16.jpg)
 
 
> Félicitation, XenServer est maintenant installé !
{.is-success}
 
# Installer un contrôleur (interface graphique)
XenServer par défaut ne possède pas d'interface web pour l'administration, cependant en vous rendant sur l'ip de ce dernier, vous aurez la possibilité de télécharger un contrôleur (logiciel) qui permettra d'administrer votre serveur avec une interface graphique.
 
### Allez sur l'interface web de votre serveur
![xenserver-controller-1.jpg](/virtualisation/xenserver/xenserver-controller-1.jpg)
 
### Installer le logiciel puis ajoutez un serveur
![xenserver-controller-2.jpg](/virtualisation/xenserver/xenserver-controller-2.jpg)
 
### Activer le WoL pour allumer votre serveur via le contrôleur
Faite un clique droit sur votre serveur -> propriétés -> Power ON
![xenserver-controller-3.jpg](/virtualisation/xenserver/xenserver-controller-3.jpg)
 
### Enfin, sélectionnez Wake-on-LAN
![xenserver-controller-4.jpg](/virtualisation/xenserver/xenserver-controller-4.jpg)