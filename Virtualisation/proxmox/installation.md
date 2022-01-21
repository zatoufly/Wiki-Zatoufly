---
title: Proxmox - Installation
description: 
published: true
date: 2022-01-21T10:16:24.996Z
tags: 
editor: markdown
dateCreated: 2022-01-18T12:01:20.532Z
---

![proxmox-banner.png](/virtualisation/proxmox/proxmox-banner.png)

# Introdution
Proxmox est un hyperviseur open source, très populaire des particuliers grâce à sa grande combabitilité avec du matériel grand public.

Dans ce tutoriel, je l'installe en version 6. La procédure n'a pas changer pour la version 7.

# Prérequis

- l'ISO de Proxmox récupèrable ici : https://www.proxmox.com/en/downloads

# Installation de Proxmox

Faite booter votre machine sur l'image ISO
![proxmox-installation-1.jpg](/virtualisation/proxmox/proxmox-installation-1.jpg)

Accepter la EULA
![proxmox-installation-2.jpg](/virtualisation/proxmox/proxmox-installation-2.jpg)

Séléctionnez le disque où sera installer proxmox
> Cliquez sur Options pour partitionnez votre disque et "gagnez" de l'espace de stockage
{.is-info}

![proxmox-installation-3.jpg](/virtualisation/proxmox/proxmox-installation-3.jpg)

Séléctionnez ext4 et la taille de la partition
![proxmox-installation-4.jpg](/virtualisation/proxmox/proxmox-installation-4.jpg)

Séléctionnez votre Timezone et la langue de votre clavier
![proxmox-installation-5.jpg](/virtualisation/proxmox/proxmox-installation-5.jpg)

Créer un mot de passe
![proxmox-installation-6.jpg](/virtualisation/proxmox/proxmox-installation-6.jpg)

Paramètrer l'interface réseau
![proxmox-installation-7.jpg](/virtualisation/proxmox/proxmox-installation-7.jpg)

Confirmer l'installation
![proxmox-installation-8.jpg](/virtualisation/proxmox/proxmox-installation-8.jpg)

Accéder à l'inferface web de proxmox
![proxmox-installation-9.jpg](/virtualisation/proxmox/proxmox-installation-9.jpg)

> L'utilisateur par défaut est **root**
{.is-info}


> Félicitation, Proxmox est maintenant installer !
> Vous aurez accès à l'interface web sur l'ip précédemment renseigner. 
{.is-success}

# Configurations
## Mise à jour
1. Connecter vous en SSH sur votre node proxmox

2. Modifier le fichier /etc/apt/sources.list.d/pve-enterprise.list

Remplacez la ligne 
```bash
deb https://enterprise.proxmox.com/debian/pve bullseye pve-enterprise
```
par
```bash
deb http://download.proxmox.com/debian/pve bullseye pve-no-subscription
```
3. Faites vos mise à jours

![proxmox-maj-1.jpg](/virtualisation/proxmox/proxmox-maj-1.jpg)

## le SWAP
Proxmox commence à utiliser le swap à partir de 60% de charge total de la RAM.
Pour changer cette valeur à 100%, connecter vous en ssh sur votre node proxmox.

1. modifer la valeur du swap
```bash
sysctl vm.swappiness=0
```

2. désactiver et réactiver le swap
```bash
swapoff -a
swapon -a
```

## Ajouter des templates conteneurs
Retrouvez le liste des templates que supporte proxmox ici : http://download.proxmox.com/images/system/

## Importer CA
https://pve.proxmox.com/wiki/Import_certificate_in_browser

Par défaut proxmox propose une connexion https non valide à son interface web. Pour certifié la validité du certificat à notre navigateur, on peux importer sur certificat préinstaller sur proxmox dans notre machine.

Connecter vous en SSH sur votre node proxmox. Et allez afficher le contenue du fichier pve-rrot-ca.pem :
```bash
cat /etc/pve/pve-root-ca.pem
```

Créer un fichier txt sur votre machine windows en le nommer `pve-root-ca.pem` (en changent bien l'extension .txt par .pem)

Ensuite copier dedans tout le contenue qui à été afficher par la commande "cat".

Enfin allez dans "option internet" sur windows et importer le certifiat .pem

# Problèmes connue
## Accès impossible à l'interface web après import de certificat
Pour résoudre ce problème, connecter vous en ssh sur votre node proxmox.

Supprimer les CA et regénérer les :
```bash
cd /etc/pve/nodes/$NODES
rm pve-ssl.key pve-ssl.pem 
pvecm updatecerts -f
```

redémarrer votre proxmox et le problème devrait être résolu. (supprimer les fichier CA proxy si celà fonctionne toujours pas)