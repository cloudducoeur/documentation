---
title: "Kubernetes"
description: "Créez et gérez vos propres cluster Kubernetes."
draft: false
type: docs
---

Le service Kubernetes d'OpenStack (Magnum) permet de déployer des clusters Kubernetes managés directement depuis votre projet.

Vous obtenez un cluster pret à l'emploi, avec un plan de controle et des noeuds workers, sans gerer vous-meme toute l'infrastructure de base.

### Concepts

*   **Cluster Template** : Modèle qui definit la version de Kubernetes, l'image, le reseau et les options du cluster.
*   **Cluster** : Ressource créee à partir d'un template, avec son endpoint API.
*   **Node Group** : Groupe de noeuds workers (utile pour dimensionner votre cluster).
*   **Kubeconfig** : Fichier de connexion pour administrer le cluster avec `kubectl`.

### Creer un cluster Kubernetes via la console

{{% steps %}}

#### Creer ou choisir un template

1.  Allez dans **Container Infrastructure** → **Cluster Templates**.
2.  Vérifiez qu'un template Kubernetes est disponible (ou créez-en un si votre projet y est autorise).
3.  Contrôlez les parametres principaux : version Kubernetes, flavour des noeuds, image et reseau.

#### Creer le cluster

1.  Allez dans **Container Infrastructure** → **Clusters**.
2.  Cliquez sur **Create Cluster**.
3.  Donnez un nom (ex: `k8s-prod`).
4.  Selectionnez le **Cluster Template**.
5.  Definissez le nombre de noeuds (ex: 3) et les options de disponibilite.
6.  Lancez la creation et attendez le statut `CREATE_COMPLETE`.

#### Recuperer le kubeconfig

1.  Ouvrez votre cluster.
2.  Cliquez sur **Download Config** (ou equivalent).
3.  Testez l'acces avec `kubectl get nodes`.

{{% /steps %}}

### Via la CLI OpenStack

```bash
# Lister les templates disponibles
openstack coe cluster template list

# Creer un cluster depuis un template
openstack coe cluster create k8s-prod \
	--cluster-template k8s-template \
	--node-count 3 \
	--master-count 1

# Suivre l'etat des clusters
openstack coe cluster list
openstack coe cluster show k8s-prod

# Recuperer le kubeconfig
openstack coe cluster config k8s-prod

# Redimensionner le nombre de noeuds
openstack coe cluster resize k8s-prod 5

# Supprimer un cluster
openstack coe cluster delete k8s-prod
```

### Bonnes pratiques

*   Démarrez avec au moins **3 workers** pour les workloads critiques.
*   Utilisez des **node groups** pour separer vos charges (systeme, applicatif, batch).
*   Sauvegardez vos manifestes et vos secrets dans un processus de CI/CD.
*   Exposez vos applications avec un **load balancer** et des noms DNS stables.
