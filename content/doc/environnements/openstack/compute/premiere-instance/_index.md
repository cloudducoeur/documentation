---
title: "Ma première instance"
description: "Lancez votre première machine virtuelle sur le Cloud du Cœur, étape par étape."
draft: false
type: docs
---

<img src="./cdc-illustration-osk-instance.gif" alt="OpenStack Instance" style="width: 25%;">

Ce guide vous accompagne dans la création de votre première instance (machine virtuelle) sur la plateforme Cloud du Cœur.

### Prérequis

Avant de commencer, assurez-vous de :

- Disposer d'un compte actif sur la [console OpenStack](https://console.aucoeurdu.cloud/auth/login?referer=/).
- Avoir [créé ou importé une paire de clés SSH](/doc/openstack/compute/paire-de-cles/).

### Créer une instance depuis la console

{{% steps %}}

#### Se connecter à la console

Rendez-vous sur la [console OpenStack](https://console.aucoeurdu.cloud/auth/login?referer=/) et connectez-vous avec vos identifiants.

#### Accéder au formulaire de création

Dans le menu latéral, naviguez vers **Compute** → **Instances**, puis cliquez sur **Lancer une instance**.

#### Renseigner les détails

- **Nom de l'instance** : Donnez un nom explicite (par exemple `mon-serveur-web`).
- **Zone de disponibilité** : Choisissez une [zone de disponibilité](/doc/openstack/compute/zones-de-disponibilite/) ou laissez la valeur par défaut.

#### Choisir une source (image)

- **Sélectionner le type de source** : Image.
- **Créer un nouveau volume** : Oui (recommandé).
- **Taille du volume** : Ajustez selon vos besoins (minimum 10 Go).
- Sélectionnez l'image souhaitée (par exemple **Debian 13** ou **Ubuntu 24.04 LTS**).

#### Choisir un gabarit (flavor)

Le gabarit détermine les ressources allouées à votre instance. Sélectionnez le gabarit adapté à votre usage.

#### Configurer le réseau

Sélectionnez le réseau sur lequel votre instance sera connectée. Si vous n'avez pas encore de réseau, consultez la [documentation Réseau](/doc/openstack/network/).

#### Associer la paire de clés

Dans l'onglet **Paire de clés**, sélectionnez la clé SSH que vous avez créée précédemment.

#### Configurer les groupes de sécurité

Vérifiez que le groupe de sécurité sélectionné autorise :
- Le **SSH** (port 22) pour vous connecter à l'instance.
- Les ports nécessaires à votre application (80 pour HTTP, 443 pour HTTPS…).

#### Lancer l'instance

Cliquez sur **Lancer l'instance**. Après quelques secondes, votre instance apparaîtra dans la liste avec le statut **Active**.

{{% /steps %}}

### Se connecter à l'instance

Une fois l'instance active et une IP flottante associée :

```bash
ssh -i ~/.ssh/ma-cle-ssh.pem debian@<IP_FLOTTANTE>
```

{{% callout type="info" %}}
Le nom d'utilisateur par défaut dépend de l'image utilisée : `debian` pour Debian, `ubuntu` pour Ubuntu, `almalinux` pour AlmaLinux.
{{% /callout %}}

### Via la CLI OpenStack

```bash
# Créer une instance
openstack server create \
  --image "Debian 12" \
  --flavor a1-ram1-disk10-perf1 \
  --key-name ma-cle-ssh \
  --network mon-reseau \
  --security-group default \
  mon-serveur-web

# Vérifier le statut
openstack server show mon-serveur-web

# Lister les instances
openstack server list

# Arrêter / démarrer une instance
openstack server stop mon-serveur-web
openstack server start mon-serveur-web

# Supprimer une instance
openstack server delete mon-serveur-web
```

### Et ensuite ?

- Associez une [IP flottante](/doc/openstack/network/) à votre instance pour la rendre accessible depuis Internet.
- Ajoutez du [stockage supplémentaire](/doc/openstack/storage/volumes/) via les volumes.
