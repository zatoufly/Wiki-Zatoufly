---
title: Kubernetes
description: 
published: true
date: 2022-02-14T15:20:21.873Z
tags: 
editor: markdown
dateCreated: 2022-02-14T10:33:28.625Z
---

# Présentation
Kubernetes ou k8s est un orchestrateur de conteneur gratuit et open source. Il est développé par Google et vous permet d'orchestrer des conteneurs sur plusieurs hôtes.

# Notions
- noeuds (serveurs) : physiques ou virtuels
  - master ou simple noeud d'exécution 
  
- pods : pierre centrale de K8S
	- ensemble cohérent de conteneurs
  - un ou plusieurs conteneurs
  - une instace de K8S
  
- service : abstraction des pods
	- permet d'éviter la communication par ip
  - service > ip/port > pods
  - service = ip et port fixe
  
- volumes : persistens ou non
	- leiux d"achanges entre pods
  - intérieur de pods = non persistent
  - extérieur = persistant
  
- deployments: objets de gestion des déploiments
	- création/supprission
  - scaling: gestion de paramètres pour la montée en charge (ou réduction)
  
- namespaces: cluster virtuel (ensemble de services)
	- sous ensemble pour cloisonner dans K8S
  
# Installation

Ce tuto est effectuer sur une Debian 11 en utilisateur root

La machine éxécutant k8s devra posséder au minimum :
- 2 cores CPU
- 2Go de RAM


Désactiver le swap est nécessaire pour le bon fonctionnement de k8s.

éditez le fichier fstab :
```bash
vim /etc/fstab
```
Commentez les lignes concernant le swap :
```bash
# swap was on /dev/sda6 during installation
# UUID=18b43798-486f-499d-9edf-2c551b34b5a1 none            swap    sw              0       0
```

Enregistrez et fermer le fichier, puis désativez le Swap à l'aide de la commande :

```bash
swapoff -a
```

Ensuite vous devez également activer l'IP forwarding. Pour celà éditez le fichier /etc/sysctl.conf :

```bash
vim /etc/sysctl.conf
```

Décommenter la ligne suivante :

```bash
net.ipv4.ip_forward=1
```

Sauvegarder et fermer le fichier.

## Installer Docker

Ensuite vous devez installer docker sur le serveurs master et les serveur workers. Installer les dépendances :

```bash
apt install apt-transport-https ca-certificates curl gnupg2 software-properties-common
```

Installer les dépots de docker :
```bash
curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list
```

Ensuite mettez à jours vos dépots et installer docker :

```bash
apt update -y
apt install docker-ce docker-ce-cli containerd.io -y
```

Vous pouvez vérifier que docker est bien installer :

```bash
docker -v
```

## Installer Kubernetes

Installer les dépots d'installation de kubernetes :
```bash
apt-get update && apt-get install -y docker.io apt-transport-https curl sudo gnupg software-properties-common
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -
sudo add-apt-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
apt update
```

Mettez à jour vos dépots et installer kubernetes :
```bash
apt update
sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni
systemctl enable kubelet
```
- kubeadm : installation du cluster
- kubelet : service qui tourne sur les machines (lancement pods...)
- kubectl : permet la communication avec le cluster

# Installation du cluster

Sur le serveur master, initialiser le cluster via la commande :
```bash
kubeadm init
```

Après quelques minutes, la commande devrait sortir :
```bash
Your Kubernetes control-plane has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

Alternatively, if you are the root user, you can run:

  export KUBECONFIG=/etc/kubernetes/admin.conf

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

Then you can join any number of worker nodes by running the following on each as root:

kubeadm join 192.168.20.10:6443 --token jw5fvt.9c51s6dp6qoixvqg \
        --discovery-token-ca-cert-hash sha256:c5b9c0fe465e71d3a56df4f1c8efe509afd1a7c1630670af5dd798a1e125978d
```

Pour démarrer le cluster, éxécuter les commandes suivantes :

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(is -u):$(id -g) $HOME/.kube/config
```

Pour joindre un serveurs worker au cluster, utiliser la commande kubeadm join fournit après l'initialisation du cluster.

# Ajoutez un worker au cluster
