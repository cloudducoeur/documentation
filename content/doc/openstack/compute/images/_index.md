---
title: "Les images"
description: "Découvrez les images système disponibles pour créer vos instances sur le Cloud du Cœur."
draft: false
type: docs
---

<img src="./cdc-illustration-osk-images.gif" alt="OpenStack Images" style="width: 25%;">

Une **image** est un modèle de système d'exploitation utilisé pour démarrer une instance. Le Cloud du Cœur met à disposition un catalogue d'images prêtes à l'emploi.

### Images disponibles

Le catalogue d'images est accessible depuis la console Horizon :

1. Connectez-vous à la [console OpenStack](https://console.cloudducoeur.org).
2. Dans le menu latéral, rendez-vous dans **Compute** → **Images**.

Vous y trouverez des images publiques maintenues par l'équipe du Cloud du Cœur, notamment :

| Image | Version | Architecture | Utilisateur par défaut
|---|---|---|---| 
| Debian | 10 | x86_64 | `debian` |
| Debian | 11 | x86_64 | `debian` |
| Debian | 12 | x86_64 | `debian` |
| Debian | 13 | x86_64 | `debian` |


{{% callout type="info" %}}
Les images publiques sont mises à jour régulièrement par l'équipe du Cloud du Coeur. Elles incluent le package `cloud-init` nécessaire à l'injection de vos clés SSH et à la configuration réseau automatique. Votre clé SSH sera injectée sur l'utilisateur par défaut de la dite image.
{{% /callout %}}

### Importer votre propre image

Si vous avez besoin d'une image spécifique, vous pouvez l'importer via la console :

{{% steps %}}

#### Préparer votre image

Votre image doit être au format **QCOW2** ou **RAW**. Assurez-vous qu'elle inclut `cloud-init` et les drivers `virtio`.

#### Accéder au formulaire d'import

Dans la console Horizon, allez dans **Compute** → **Images**, puis cliquez sur **Créer une image**.

#### Renseigner les informations

- **Nom** : Un nom explicite pour votre image.
- **Source** : Sélectionnez le fichier image depuis votre poste ou renseignez une URL.
- **Format** : Choisissez le format correspondant (QCOW2, RAW…).
- **Visibilité** : Laissez sur **Privée** pour que seul votre projet y ait accès.

#### Valider

Cliquez sur **Créer une image**. L'import peut prendre quelques minutes selon la taille du fichier.

{{% /steps %}}

### Via la CLI OpenStack

Vous pouvez également gérer vos images en ligne de commande :

```bash
# Lister les images disponibles
openstack image list

# Téléverser une image
openstack image create "Mon image" \
  --file mon-image.qcow2 \
  --disk-format qcow2 \
  --container-format bare \
  --private

# Voir les détails d'une image
openstack image show "Mon image"

# Supprimer une image
openstack image delete "Mon image"
```

{{% callout type="info" %}}
Pour utiliser la CLI, consultez au préalable la page [CLI OpenStack](/doc/cli/) pour l'installation et la configuration.
{{% /callout %}}
