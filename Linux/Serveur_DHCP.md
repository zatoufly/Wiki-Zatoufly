---
title: Serveur DHCP
description: 
published: 1
date: 2022-01-02T10:56:23.883Z
tags: 
editor: markdown
dateCreated: 2022-01-02T10:56:23.883Z
---

# Prérequis
- Machine sous Redhat (ou dérivés)
- Adresse IP fixe
# Installation
### Installation du paquet requis
```bash
dnf update
dnf dhcp-server -y
```

### Modifier le fichier de configuration
```bash
vim /etc/dhcp/dhcpd.conf
```

### ajoutez une étendu :
```bash
default-lease-time 86400; # Définie la durée du bail (24h)
max-lease-time 172800; # Définie le bail maximum (48h)

subnet 192.168.1.0 netmask 255.255.255.0 { # Indique le réseau et son masque
				range 192.168.1.10 192.168.1.253; # Définie la plage du DHCP
        option routers 192.168.1.1; # Définie l'ip du routeur
        option domain-name-servers 192.168.1.2; # Définie le serveur DNS
}
```

### Démarrer le service
```bash
systemctl enable --now dhcpd
systemctl start dhcpd
```

# Allez plus loin

## Réserver une addresse
```bash
default-lease-time 86400; 
max-lease-time 172800; 
subnet 192.168.1.0 netmask 255.255.255.0 { 
				range 192.168.1.10 192.168.1.253; 
        option routers 192.168.1.1; 
        option domain-name-servers 192.168.1.2;
        
        host ubuntu {
        		hardware ethernet 00:0c:29:8e:12:33; # Renseignez l'address MAC 
            fixed-address 192.168.1.150; # l'adresse qui sera réverser
        }
}
```

## Refuser un client
```bash
default-lease-time 86400; 
max-lease-time 172800; 
subnet 192.168.1.0 netmask 255.255.255.0 { 
				range 192.168.1.10 192.168.1.253; 
        option routers 192.168.1.1; 
        option domain-name-servers 192.168.1.2;
        
        host ubuntu {
        		hardware ethernet 00:0c:29:8e:12:33; # Renseignez l'address MAC 
            deny booting; # permet de refuser de distribuer une IP
        }
}
```

## Ajoutez plusieurs plages
```bash
# première plage
default-lease-time 86400;
max-lease-time 172800;

subnet 192.168.1.0 netmask 255.255.255.0 { 
				range 192.168.1.10 192.168.1.253;
        option routers 192.168.1.1; 
        option domain-name-servers 192.168.1.2; 
}

# deuxième plage 
default-lease-time 86400; 
max-lease-time 172800; 

subnet 192.168.2.0 netmask 255.255.255.0 { 
				range 192.168.2.10 192.168.2.253; 
        option routers 192.168.2.1; 
        option domain-name-servers 192.168.2.2;
}
```

## option communes aux plages
```bash
option routers 192.168.2.1; 
option domain-name-servers 192.168.2.2;

# première plage
default-lease-time 86400;
max-lease-time 172800;

subnet 192.168.1.0 netmask 255.255.255.0 { 
				range 192.168.1.100 192.168.1.150;
}

# deuxième plage 
default-lease-time 86400; 
max-lease-time 172800; 

subnet 192.168.1.0 netmask 255.255.255.0 { 
				range 192.168.1.200 192.168.1.253;   
}
```