---
title: OpenSSL
description: 
published: true
date: 2022-10-07T07:06:47.659Z
tags: 
editor: markdown
dateCreated: 2022-02-14T08:55:36.353Z
---

# Générer le CA
Le CA ou "Certificate Authority" permet de signer nos certificats.
 
On peut générer la clé privée. Il vous sera demandé une passphrase, qui permettra plus tard de certifier notre certificat.
```bash
openssl genrsa -des3 -out zatouflyCA.key 4096
```
 
On génère le certificat racine au format .pem à partir de la clé précédemment créée.
Il vous sera demandé ces informations :

```bash
openssl req -x509 -new -nodes -key zatouflyCA.key -sha256 -days 10000 -out zatouflyCA.pem
```

Output:
```
Enter pass phrase for linuxtricksCA.key:
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) []:
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:ZatouflyCA
Email Address []:
```
Hormis le Common Name à renseigner, le reste n'a pas d'importance.

 
Puis on le génère maintenant pour avoir un format en .crt
```bash
openssl x509 -in zatouflyCA.pem -inform PEM -out zatouflyCA.crt
```
 
On a 3 fichiers :
- zatouflyCA.key : La clé privée
- zatouflyCA.pem : Certificat racine au format pem
- zatouflyCA.crt : Certificat racine au format crt
 
Il vous faudra dans le cas d'un poste Windows d'importer le fichier .crt dans le magasin.

# Créer un certificat pour un hôte
 
Pour des raisons de simplicité, nous allons créer un certificat "wildcard" qui pourra se greffer à n'importe quel sous-domaine. Cela nous évite de générer un certificat pour chaque sous-domaine.
 
Je génère la clé 
```bash
openssl genrsa -out wildcard.local.key 2048
```
 
générer le csr (Certificate Signing Request) :
```bash
openssl req -new -key wildcard.local.key -out wildcard.zatoufly.csr
```
 
Il vous sera demandé des informations, attention au paramètre "Common Name" c'est ici que l'on met nos sous domaine à certifier.
 
Dans notre cas on met un "*" à la place du sous domaine
```bash
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) [AU]:
State or Province Name (full name) [Some-State]:
Locality Name (eg, city) []:
Organization Name (eg, company) [Internet Widgits Pty Ltd]:
Organizational Unit Name (eg, section) []:
Common Name (e.g. server FQDN or YOUR name) []:*.zatoufly.local # <- ATTENTION, insérer votre nom de domaine
Email Address []:
Please enter the following 'extra' attributes
to be sent with your certificate request
A challenge password []:
An optional company name []:
```
 
Ensuite créer un fichier certifica.ini, 
```bash
nano certifica.ini
```
et copier le code ci-dessous :
```bash
authorityKeyIdentifier=keyid,issuer
basicConstraints=CA:FALSE
keyUsage = digitalSignature, nonRepudiation, keyEncipherment, dataEncipherment
subjectAltName = @alt_names
[alt_names]
DNS.2 = *.zatoufly.local # modifier avec votre nom de domaine local
```
Enregistrez-le.
 
Enfin signer votre certificat avec la clé CA crée au début du tuto :
```bash
openssl x509 -req -in wildcard.zatoufly.csr -CA zatouflyCA.pem -CAkey zatouflyCA.key -CAcreateserial -out wildcard.zatoufly.crt -days 10000 -sha256 -extfile certifica.ini
```
Nous avons ces fichiers : 
- wildcard.local.key => La clé privée du certificat du sous domaine
- wildcard.zatoufly.csr => La demande de signature du certificat
- wildcard.zatoufly.crt => Certificat du sous domaine au format crt
- certifica.ini => Fichier de configuration du sous domaine
 
Il vous reste qu'à configurer le certificat sur un serveur web ou un reverse proxy.

# Importer le CRT
# Tabs {.tabset}
## Windows
Sur votre machine Windows, créer un fichier du même nom que votre Certificat racine au format crt. Je crée zatouflyCA.crt
 
Sur votre machine linux où a été créer le certificat, afficher sont contenus via cat.
```bash
cat zatouflyCA.crt
```
 
Copier le contenu du fichier dans le fichier créé sur la machine Windows
 
Enregistrez le et ouvrez le fichier avec "Extensions noyau de chiffrement"
 
Installer le certificat
![openssl-windows01.jpg](/linux/openssl/openssl-windows01.jpg)
 
Installez-le dans l'ordinateur local
![openssl-windows02.jpg](/linux/openssl/openssl-windows02.jpg)
 
Placer le certificat manuellement  et cliquez sur "Parcourir..."
![openssl-windows03.jpg](/linux/openssl/openssl-windows03.jpg)
 
Séléctionnez le second dossier "Autorités de certication racines de confiance"
![openssl-windows04.jpg](/linux/openssl/openssl-windows04.jpg)
 
Suivez les étapes restantes, votre certificat devrait s'exporter dans le magasin 
 
