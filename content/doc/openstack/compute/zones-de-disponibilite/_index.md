---
title: "Les zones de disponibilité"
description: "Comprenez le fonctionnement des zones de disponibilité sur le Cloud du Cœur."
draft: false
type: docs
---

<img src="./cdc-illustration-osk-az.gif" alt="OpenStack AZ" style="width: 25%;">

Les **zones de disponibilité** (Availability Zones) permettent de répartir vos instances sur des groupes de serveurs physiques distincts. Elles jouent un rôle clé dans la **haute disponibilité** et la **résilience** de vos services.

## Principe de fonctionnement

Chaque zone de disponibilité correspond à un ensemble isolé de ressources matérielles (serveurs, alimentation, réseau). Si une zone rencontre un problème, les autres zones continuent de fonctionner normalement.

```
┌──────────────────────────────────────────┐
│           Cloud du Cœur                  │
│                                          │
│  ┌──────────┐  ┌──────────┐  ┌────────┐  │
│  │  Zone A  │  │  Zone B  │  │ Zone C │  │
│  │  ─────   │  │  ─────   │  │ ─────  │  │
│  │ Serveurs │  │ Serveurs │  │Serveurs│  │
│  │ Stockage │  │ Stockage │  │Stockage│  │
│  └──────────┘  └──────────┘  └────────┘  │
└──────────────────────────────────────────┘
```

## Cas d'usage

### Haute disponibilité

Pour un service critique, déployez vos instances sur **plusieurs zones différentes**. Ainsi, en cas de défaillance d'une zone, vos autres instances restent opérationnelles.

### Service non critique

Pour des environnements de développement ou de test, une seule zone suffit. Vous pouvez laisser OpenStack choisir automatiquement la zone.

## Choisir une zone de disponibilité

### Depuis la console

Lors de la [création d'une instance](/doc/openstack/compute/premiere-instance/), sélectionnez la zone souhaitée dans le champ **Zone de disponibilité** du formulaire.

### Via le CLI

```bash
# Lister les zones de disponibilité
openstack availability zone list

# Créer une instance dans une zone spécifique
openstack server create \
  --image "Debian 12" \
  --flavor a1-ram1-disk10-perf1 \
  --key-name ma-cle-ssh \
  --availability-zone par1 \
  mon-instance
```

## Bonnes pratiques

- **Services critiques** : Répartissez vos instances sur au moins 2 zones de disponibilité.
- **Load balancer** : Placez un répartiteur de charge devant vos instances multi-zones.
- **Stockage** : Les volumes sont liés à une zone. Assurez-vous que vos instances et leurs volumes sont dans la même zone.

{{% callout type="info" %}}
La liste des zones de disponibilité peut évoluer au fil du temps selon l'infrastructure du Cloud du Cœur. Consultez la console pour connaître les zones actives.
{{% /callout %}}
