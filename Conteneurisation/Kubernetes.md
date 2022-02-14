---
title: Kubernetes
description: 
published: true
date: 2022-02-14T17:44:15.322Z
tags: 
editor: markdown
dateCreated: 2022-02-14T10:33:28.625Z
---

# Présentation
Kubernetes ou k8s est un orchestrateur de conteneur gratuit et open source. Il est développé par Google et vous permet d'orchestrer des conteneurs sur plusieurs hôtes.

# Notions
Les **noeuds** sont des serveurs physiques ou virtuels.
Il existe les noeuds master (serveur maitre) et les worker (serveur d'éxécution)

Les **pods** sont un ensemble de conteneurs, il peux contenir un au plusieurs conteneurs.
  
Les **services** sont un moyen d'accéder à nos pods via (ip/port) c'est l'équivalent à l'exposition sur docker
  
- volumes : persistens ou non
	- leiux d"achanges entre pods
  - intérieur de pods = non persistent
  - extérieur = persistant
  
Les **deployments** sont une représentation logique de un ou plusieurs pod.
- deployments: objets de gestion des déploiments
	- création/supprission
  - scaling: gestion de paramètres pour la montée en charge (ou réduction)
  
- namespaces: cluster virtuel (ensemble de services)
	- sous ensemble pour cloisonner dans K8S
  
# Commandes
|     |     |
| --- | --- |
| `txt` | txt |
| `txt` | txt |


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
Si docker n'est pas démarrer, démarrer le :
```bash
systemctl start docker
```


j'ajoute mon serveur worker au cluster :
```bash
kubeadm join 192.168.20.10:6443 --token jw5fvt.9c51s6dp6qoixvqg \
        --discovery-token-ca-cert-hash sha256:c5b9c0fe465e71d3a56df4f1c8efe509afd1a7c1630670af5dd798a1e125978d
```

La commande soit vous retourner :
```bash
This node has joined the cluster:
* Certificate signing request was sent to apiserver and a response was received.
* The Kubelet was informed of the new secure connection details.

Run 'kubectl get nodes' on the control-plane to see this node join the cluster.
```

Vérifiez sur le serveur master, que le worker à bien été ajouté :
```bash
kubectl get nodes
```

Vous devriez voir vos deux serveurs :
```bash
NAME        STATUS     ROLES                  AGE   VERSION
k8smaster   NotReady   control-plane,master   69m   v1.23.3
k8snode     NotReady   <none>                 16m   v1.23.3
```

Toujours sur le serveur master, installer de module réseau Calico Pod :
```bash
kubectl apply -f https://docs.projectcalico.org/v3.16/manifests/calico.yaml
```
Vérifiez l'état des Pod avec cette commande :
```bash
kubectl get pods --all-namespaces

```
Elle devrait retourner :
```bash
NAMESPACE     NAME                                     READY   STATUS     RESTARTS      AGE
kube-system   calico-kube-controllers-cdbb46f6-wnlvl   0/1     Pending    0             54s
kube-system   calico-node-49gdj                        0/1     Init:1/3   0             54s
kube-system   calico-node-db6lq                        0/1     Init:0/3   0             54s
kube-system   coredns-64897985d-5h8w8                  0/1     Pending    0             94m
kube-system   coredns-64897985d-gh7td                  0/1     Pending    0             94m
kube-system   etcd-k8smaster                           1/1     Running    0             94m
kube-system   kube-apiserver-k8smaster                 1/1     Running    0             94m
kube-system   kube-controller-manager-k8smaster        1/1     Running    0             94m
kube-system   kube-proxy-gbkkp                         1/1     Running    2 (30m ago)   41m
kube-system   kube-proxy-vr7bc                         1/1     Running    0             94m
kube-system   kube-scheduler-k8smaster                 1/1     Running    0             94m
```

Enfin nous allons tester si notre cluster fonctionne. Pour ce faire nous allons déployer Nginx.
```bash
kubectl create deployment nginx-web --image=nginx --port=80
```

Vérifiez le déploiement :
```bash
kubectl get deployments.apps  -o wide
```

La commande doit vous afficher :
```bash
NAME        READY   UP-TO-DATE   AVAILABLE   AGE   CONTAINERS   IMAGES   SELECTOR
nginx-web   0/1     1            0           4s    nginx        nginx    app=nginx-web
```

Ensuite, on scale le deploiment à 3 :
```bash
kubectl scale --replicas=3 deployment nginx-web
```

On vérifie :
```bash
kubectl get deployments.apps nginx-web
```

La commande doit retourner : 
```bash
NAME        READY   UP-TO-DATE   AVAILABLE   AGE
nginx-web   3/3     3            3           40s
```

Ensuite on créer un service Nginx en exposant le port 80 :

```bash
kubectl run nginx-web --image=httpd --port=80
kubectl expose pod nginx-web --name=http-service --port=80 --type=NodePort
```

On peux vérifier le services avec :
```bash
kubectl get service http-service
```

La commande doit retourner :
```bash
NAME           TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
http-service   NodePort   10.100.217.87   <none>        80:30784/TCP   2s
```

Pour obtenir des informations sur le service "http-service" un éxécute la commande :
```bash
kubectl describe service http-service
```

Qui nous retourner :
```bash
NAME           TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)        AGE
http-service   NodePort   10.100.217.87   <none>        80:30784/TCP   2s
root@K8Smaster:/home/zatoufly# kubectl describe service http-service
Name:                     http-service
Namespace:                default
Labels:                   run=nginx-web
Annotations:              <none>
Selector:                 run=nginx-web
Type:                     NodePort
IP Family Policy:         SingleStack
IP Families:              IPv4
IP:                       10.100.217.87
IPs:                      10.100.217.87
Port:                     <unset>  80/TCP
TargetPort:               80/TCP
NodePort:                 <unset>  30784/TCP
Endpoints:                172.16.145.199:80
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>
```

On peux voir les pods actif via la commande :
```bash
kubectl get pods nginx-web -o wide
```

# Déploier un Pod

```bash
kubectl run myshell -it --image busybox -- sh
```
kubectl run est un équivalent à docker run. Avec kubectl run on lance un pod qui contient un ou plusieurs conteneurs (un conteneur de ce cas)

myshell est le nom du pod

-it permet de ce connecter sur le pod
--image busybox est l'image qui sera éxécuter
-- sh pour passer la commande sh au pod

pour voir les pods :
```bash
kubectl get pods
```

pour supprimer le pod :
```bash
kubectl delete pods myshell
```

pour voir les deployment :
```bash
kubectl get deploy
```

pour supprimer les deployment
```bash
kubectl delete deplay myshell
```

# Services

```bash
kubectl create deploy mynginx --image nginx
```

équivalent à docker docker inspect
```bash
kubectl describe pod mynginx
```

On vient de créer un pod nginx, mais comment y accéder ?

On va exposer les port comme pour docker sauf que dans k8s on utile les service pour remplir cette tâche.

```bash
kubectl create service nodeport mynginx --tcp=8080:80
```
nodeport est un type de service, il en existe plusieurs :
- nodeport = exposition de port : rendre public notre pod via un port
- Clusterip = exposition à l'interieur du clusteur uniquement (pas public)
- loadBalancerIP = pour exposer via controler ingress ou dans le cloud
- externalname = via une url

Pour voir nos service : kubectl get svc

Si on se rend sur l'ip de notre master suivi du port attribuer par kubernetes, on arrive sur nginx

# Scaling