---
title: NFS
description: 
published: 1
date: 2022-01-13T12:28:03.402Z
tags: 
editor: markdown
dateCreated: 2022-01-13T12:28:03.402Z
---

# Introduction
# Serveur
## Installation
```bash
apt install nfs-kernel-server
systemctl enable nfs-server.service
```

# Créer un partage NFS

```bash
mkdir /srv/partagenfs
chown nobody:nogroup /srv/partagenfs
chmod 755 /srv/partagenfs
nano /etc/exports
```
dans le fichier ajoutez cette ligne :

```bash
/srv/partagenfs 192.168.100.0/24(rw,sync,anonuid=65534,anongid=65534,no_subtree_check)
```

Chargez le contenue du fichier export :
```bash
exportfs -a
```

Afficher les partages montées :
```bash
showmount -e [IP du serveur]
```

# Client
## Installation
```bash
apt install nfs-common
```

## Connecter un partage NFS

```bash
mkdir /media/partagenfs
vim /etc/fstab
```
ajouter la ligne : 

```bash
192.168.100.121:/srv/partagenfs /media/partagenfs nfs4 defaults,user,exec 0 0
```
Enregistez le fichier et monté le partage :
```bash
mount -a
```
---
Vous pouvez également monter un partage de manière temporaire, exécuter cette commande :
```bash
mount -t nfs4 192.168.100.121:/srv/partagenfs /media/partagenfs
```

Pour démonter un partage NFS :
```bash
umount partagenfs
```