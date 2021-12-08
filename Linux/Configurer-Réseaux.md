---
title: Configurer Réseaux
description: 
published: 1
date: 2021-12-08T12:33:09.747Z
tags: 
editor: markdown
dateCreated: 2021-12-08T12:33:09.747Z
---

# Debian et dérivées
## Changer IP
## Changer DNS
## Changer Hostname

# RedHat et dérivées

## Changer IP
Le nom de votre carte réseau peut varié, pour connaitre son nom utilisé : `ip addr`
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: ens18: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 2a:1b:a2:5b:09:bd brd ff:ff:ff:ff:ff:ff
    inet 192.168.10.204/24 brd 192.168.10.255 scope global noprefixroute ens18
       valid_lft forever preferred_lft forever
    inet6 fe80::281b:a2ff:fe5b:9bd/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```

Pour changez votre adresse ip, éditez le fichier `/etc/sysconfig/network-scripts/ifcfg-ens18` *à adapter selon le nom de votre carte*

### DHCP
Pour mettre votre interface en dhcp, modifier le paramètre : `BOOTPROTO=dhcp`
Oubliez pas de commentez ou supprimer les lignes qui servent à l'ip static : `IPADD`, `NETMASK`, `GATEWAY`, `DNS1`

Relancez votre carte réseau : `ifdown ens18` `ifup ens18`

## Changer DNS
## Changer Hostname