---
title: "Les sauvegardes"
description: "Protégez vos données avec les instantanés (snapshots) de volumes."
draft: false
type: docs
---

Il est crucial de protéger vos données. OpenStack propose un mécanisme simple pour sauvegarder vos volumes : les **instantanés** (snapshots).

### Instantanés de volume (Snapshots)

Un instantané est une copie ponctuelle d'un volume. C'est utile pour sauvegarder l'état d'un disque avant une modification risquée (mise à jour, migration, etc.).

{{% steps %}}

#### Créer un instantané

1. Allez dans **Volumes** → **Volumes**.
2. Sur la ligne du volume concerné, cliquez sur le menu déroulant et choisissez **Créer un instantané**.
3. Nommez votre instantané (ex: `snap-data-pre-update`).
4. Validez.

#### Restaurer (Créer un volume depuis un instantané)

Pour restaurer des données, on crée un *nouveau* volume basé sur l'instantané.

1. Allez dans **Volumes** → **Instantanés**.
2. Sur l'instantané, cliquez sur **Créer un volume**.
3. Suivez la procédure de création de volume classique (Nom, Taille...).
4. Attachez ensuite ce nouveau volume à votre instance pour récupérer vos données.

{{% /steps %}}

{{% callout type="warning" %}}
Attention : Supprimer le volume original peut impacter l'instantané si celui-ci est dépendant (selon le backend de stockage). Par sécurité, considérez les instantanés comme des solutions de court terme.
{{% /callout %}}

### Via la CLI OpenStack

```bash
# Créer un instantané d'un volume
openstack volume snapshot create --volume data-vol-1 snap-data-1

# Lister les instantanés
openstack volume snapshot list

# Créer un nouveau volume à partir d'un instantané
# (nécessaire pour accéder aux données sauvegardées)
openstack volume create --snapshot snap-data-1 restored-data-vol
```
