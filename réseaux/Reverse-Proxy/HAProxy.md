---
title: HAProxy
description: 
published: true
date: 2022-02-12T20:57:24.466Z
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

#

## Emplacement des fichiers de configuration

|     |     |
| --- | --- |
| `/etc/sysconfig` | configuration du daemon |
| `/etc/logrotate.d/haproxy` | si utilisation de logrotate |
| `/etc/haproxy/haproxy.cfg` | fichier de configuration des frontend/backend |
| `/var/lib/haproxy` | data de haproxy  |
| `/usr/sbin/haproxy` | binaire de haproxy |
| `/usr/share/haproxy` | template des pages d'erreur |

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
