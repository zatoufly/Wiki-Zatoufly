---
title: Configurer Réseaux
description: 
published: true
date: 2022-01-17T13:49:23.499Z
tags: 
editor: markdown
dateCreated: 2022-01-14T20:20:43.155Z
---

# Debian et dérivées

## Changer IP

### IP statique

Pour connaitre son adresse ip utiliser : `ip a`  
Pour modifier son ip éditer le fichier `/etc/network/interfaces`  
Voici un exemple de configuration en IP statique :

```
allow-hotplug ens18
iface ens18 inet static
  address 192.168.20.1/24
  gateway 192.168.20.254
```

OU

```
allow-hotplug ens18
iface ens18 inet static
  address 192.168.20.1
  netmask 255.255.255.0
  gateway 192.168.20.254
```


### DHCP

Voici un exemple de configuration en DHCP :

```
allow-hotplug ens18
iface ens18 inet dhcp
```

## Changer DNS

Pour changer le DNS ça se passe dans le fichier `/etc/resolv.conf`  
Voici un exemple de configuration :

```bash
nameserver 192.168.10.2 # DNS Principal
nameserver 8.8.8.8 # DNS secondaire
```

## Changer Hostname

Pour voir quel est son hostname effectué la commande suivante : `hostnamectl`  
Pour le changez, il suffit de faire : `hostnamectl -set nom-hostname`

- [En vidéo *sur youtube*](https://www.youtube.com/watch?v=dXqDPO0knJk)
{.links-list}


# RedHat et dérivées

## Changer IP

Le nom de votre carte réseau peux varier, pour connaître son nom utilisé : `ip a`

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
### IP static

Pour affecter une adresse ip static à votre interface modifier le paramètre `BOOTPROTO=static`  
Ajoutez également ces 3 lignes :

```
IPADDR=192.168.10.10
NETMASK=255.255.255.0
GATEWAY=192.168.10.1
```
> Après avoir sauvegarder le fichier de configuration, 
relancez votre carte réseau : <kbd>ifdown ens18</kbd> puis <kbd>ifup ens18</kbd>
{.is-warning}

### DHCP

Pour mettre votre interface en dhcp, modifier le paramètre : `BOOTPROTO=dhcp`  
Oubliez pas de commenter ou supprimer les lignes qui servent à l'ip static : `IPADDR`, `NETMASK`, `GATEWAY`, `DNS1`

> Après avoir sauvegarder le fichier de configuration, 
relancez votre carte réseau : <kbd>ifdown ens18</kbd> puis <kbd>ifup ens18</kbd>
{.is-warning}



## Changer DNS

Pour changer votre DNS ça se passe également dans `/etc/sysconfig/network-scripts/ifcfg-ens18`  
Ajoutez à la fin du fichier :

```
DNS1=192.168.10.2
DNS2=1.1.1.1
```

> Après avoir sauvegarder le fichier de configuration, 
relancez votre carte réseau : <kbd>ifdown ens18</kbd> puis <kbd>ifup ens18</kbd>
{.is-warning}

## Changer Hostname

Pour voir quel est son hostname effectué la commande suivante : `hostnamectl`  
Pour le changez, il suffit de faire : `hostnamectl -set nom-hostname`