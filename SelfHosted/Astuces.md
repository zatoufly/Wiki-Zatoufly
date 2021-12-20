---
title: Astuces
description: 
published: 1
date: 2021-12-20T21:47:09.341Z
tags: 
editor: markdown
dateCreated: 2021-12-20T21:47:09.341Z
---

# Let's Encrypt sur Apache
Let's Encrypt vous permet de mettre n'importe quel virtual host d'apache en https gratuitement et simplement.

On peut l'installer comme ceci :

```bash
apt install certbot python3-certbot-apache
```

Et on peut réclamer à let's encrypt notre certificat SSL :

```bash
certbot --apache --agree-tos --redirect --staple-ocsp --email votre_email@example.com -d subdomain.example.com
```

N'oubliez pas de recharger la configuration d'apache :

```bash
systemctl reload apache2
```