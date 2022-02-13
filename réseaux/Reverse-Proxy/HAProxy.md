---
title: HAProxy
description: 
published: true
date: 2022-02-13T13:00:49.017Z
tags: 
editor: markdown
dateCreated: 2022-02-12T19:23:12.893Z
---

# Présentation
HAProxy est un logiciel gratuit et open source, c'est un serveur proxy très connue surtout pour faire du load balancing (répertition de charges) de serveur web.

# Installation

# Tabs {.tabset}
## Debian

```bash
apt update && apt full-upgrade -y
apt install haproxy
```

# Configuration

## Emplacement des fichiers de configuration

|     |     |
| --- | --- |
| `/etc/sysconfig` | configuration du daemon |
| `/etc/logrotate.d/haproxy` | si utilisation de logrotate |
| `/etc/haproxy/haproxy.cfg` | fichier de configuration des frontend/backend |
| `/var/lib/haproxy` | data de haproxy  |
| `/usr/sbin/haproxy` | binaire de haproxy |
| `/usr/share/haproxy` | template des pages d'erreur |

Element du fichier de configuration :
- Frontend : ce que le proxy reçoit (écoute tel IP, tel port)
- Backend : où la requête est rediriger 
- global : s'applique à haproxy lui même
- default : s'applique au backend et fronted si ils sont pas configuré

# Backend & Frontend

```bash
frontend myapp_front
        bind *:80
        default_backend myapp_back

backend myapp_back
        server srv_nginx 192.168.20.4:80 
```

# Load Balancing
```bash
frontend myapp_front
        bind *:80
        default_backend myapp_back

backend myapp_back
        balance roundrobin
        server srv_nginx 192.168.20.4:80
        server srv_apache 192.168.20.5:80
```

## Algorithmes

# Tabs {.tabset}
## RoundRobin
roundrobin envoie le client une fois sur le nombre de serveurs dans le pool (fait une boucle)
```bash
backend load1
	balance roundrobin
  server srv1 192.168.10.2:80
  server srv2 192.168.10.3:80
  server srv3 192.168.10.4:80
```
### RoundRobin Weighted
RoundRobin mais avec de la pondération

Si weight = 0 aucun trafic envoyer sur le serveur (mode maintenance)
```bash
backend load1
	balance roundrobin
  server srv1 192.168.10.2:80 weight 1
  server srv2 192.168.10.3:80 weight 2
  server srv3 192.168.10.4:80 weight 3
```
Le trafic est envoyé 1/6 sur le serveur 1
                     2/6 sur le serveur 2
                     3/6 sur le serveur 3

## Leastconn
Prend en compte le serveur qui a le plus de connexionx en cours, il envoie le trafic vers le serveur avec le moins de client connecté.

Utile pour les bases de données
```bash
backend load1
	balance leastconn
  server srv1 192.168.10.2:80
  server srv2 192.168.10.3:80
  server srv3 192.168.10.4:80
```
### Leastconn Weighted
Leastconn mais avec pondération

Si weight = 0 aucun trafic envoyer sur le serveur (mode maintenance)
```bash
backend load1
	balance leastconn
  server srv1 192.168.10.2:80 weight 1
  server srv2 192.168.10.3:80 weight 2
  server srv3 192.168.10.4:80 weight 3
```
Le trafic est envoyé 1/6 sur le serveur 1
                     2/6 sur le serveur 2
                     3/6 sur le serveur 3

## Hash uri
weight possible
```bash
backend load1
	balance roundrobin
  server srv1 192.168.10.2:80
  server srv2 192.168.10.3:80
  server srv3 192.168.10.4:80
```
## First connexion
Dans l'ordre de la liste.
Pour économiser des ressouces et d'adapter réellement à la charge (machine up pour débordement)

```bash
backend load1
	balance roundrobin
  server srv1 192.168.10.2:80 maxconn 5
  server srv2 192.168.10.3:80 maxconn 5
  server srv3 192.168.10.4:80 maxconn 5
```
Envoie les 5 premier client sur le srv1, une fois fois passe au srv2, etc


# ACL
Les ACL dans HAproxy permettent de rediriger un nom de domaine dns vers un serveur. C'est la fonction reverse proxy pour faire simple.

```bash
frontend myapp_front
        bind *:80
        mode http

        acl myapp_front hdr_dom(host) -i speed.local
        use_backend load if myapp_front

backend load
        server srv_librespeed 192.168.10.5:5252
```

# Interface graphique

accessible sur ip:9000/stats

```bash
listen stats
        bind *:9000
        stats enable
        stats uri /stats
        stats refresh 2s
        stats auth zatoufly:password
```

ajouter ces l'option pour activer les description dans les fronted/backend/global 
```bash
stats show-desc
stats show-legends
```
ajoutez dans fronted :
```bash
description mon message
```

# Forward For
Le Forward For permet de sauvegarder l'ip du client

# Tabs {.tabset}
## Méthode 1

```bash
frontend myapp_front
	bind *:80
  mode http
  default_backend load
  http-request set-header Forwarded for=%[src]
  
backend load
	server load1 192.168.10.20:80
```

## Méthode 2

```bash
frontend myapp_front
	bind *:80
  mode http
  option forwardfor
  default_backend load
  
backend load
	server load1 192.168.10.20:80
```

# SSL/TLC
# Tabs {.tabset}
## Terminaison TLS
Le serveur web est en HTTP, et HAproxy gère le certificat TLS

```bash
frontend myapp_front
        bind *:80
        bind *:443 ssl crt /etc/ssl/zatoufly/zatoufly.pem no-sslv3 #emplacement ssl
        redirect scheme https if !{ ssl_fc } # rediction http -> https
        mode http
```

## Passthrough
Le serveur web gère lui même sont certificat

```bash
frontend myapp_front
        bind *:443
        mode tcp
```


## Réencryption
Le serveur web gère son certificat et un deuxième certificat sur HAproxy 

```bash
frontend myapp_front
        bind *:80
        bind *:443 ssl crt /etc/ssl/zatoufly/zatoufly.pem no-sslv3 #emplacement ssl
        redirect scheme https if !{ ssl_fc } # rediction http -> https
        mode http
        default_backend pool_load
        
backend pool_load
				mode http
        server srv1 192.168.10.1:443 check ssl verify none
```