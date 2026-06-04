---
title: "Les volumes"
description: "Gérez le stockage block persistant avec les volumes OpenStack (Cinder)."
draft: false
type: docs
---

Les **volumes** sont des espaces de stockage persistants que vous pouvez attacher à vos instances. Contrairement au disque système local (Ephemeral) de l'instance qui peut être perdu lors de la suppression de l'instance, les données sur un volume sont conservées indépendamment du cycle de vie des serveurs.

### Créer et attacher un volume via la console

{{% steps %}}

#### Créer un volume

1. Allez dans **Volumes** → **Volumes**.
2. Cliquez sur **Créer un volume**.
3. Donnez un **Nom** (ex: `data-vol-1`).
4. Spécifiez la **Taille** (en Go).
5. Validez avec **Créer un volume**.

#### Attacher le volume à une instance

1. Dans la liste des volumes, localisez votre volume.
2. Cliquez sur le menu déroulant à droite (flèche) et sélectionnez **Gérer les attachements**.
3. Sélectionnez l'instance à laquelle attacher le volume.
4. Cliquez sur **Attacher le volume**.

{{% /steps %}}

{{% callout type="info" %}}
Une fois attaché, le volume apparaît comme un disque supplémentaire dans votre instance (ex: `/dev/vdb` sous Linux). Vous devrez le formater et le monter pour l'utiliser.
{{% /callout %}}

### Formater et monter le volume (Linux)

Connectez-vous à votre instance et exécutez :

```bash
# Identifier le nouveau disque (souvent /dev/sdb ou /dev/vdb)
lsblk

# Créer un système de fichiers (formatage)
sudo mkfs.ext4 /dev/sdb

# Créer un point de montage
sudo mkdir /mnt/data

# Monter le volume
sudo mount /dev/sdb /mnt/data

# Vérifier
df -h
```

### Via la CLI OpenStack

```bash
# Créer un volume de 10 Go
openstack volume create --size 10 data-vol-1

# Lister les volumes
openstack volume list

# Attacher le volume à une instance
openstack server add volume <INSTANCE_NAME> data-vol-1

# Détacher un volume
openstack server remove volume <INSTANCE_NAME> data-vol-1

# Supprimer un volume (doit être détaché)
openstack volume delete data-vol-1
```
