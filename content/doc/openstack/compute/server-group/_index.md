---
title: "Les groupes de serveurs"
description: "Gérez le placement de vos instances avec les groupes de serveurs (affinité/anti-affinité)."
draft: false
type: docs
---

Les **groupes de serveurs** (Server Groups) vous permettent de contrôler la répartition de vos instances sur les hyperviseurs physiques. C'est un outil essentiel pour garantir la **haute disponibilité** ou maximiser les **performances** de vos applications.

### Les politiques de placement

Il existe principalement deux types de politiques :

*   **Anti-affinité (anti-affinity)** : Les instances du groupe doivent être hébergées sur des **hôtes physiques différents**.
    *   *Usage recommandé :* Pour la redondance et la haute disponibilité (ex: cluster de base de données, serveurs web load-balancés). Si un hyperviseur tombe en panne, seule une partie de votre service est impactée.

*   **Affinité (affinity)** : Les instances du groupe doivent être hébergées sur le **même hôte physique**.
    *   *Usage recommandé :* Pour optimiser les performances réseau entre les instances (baisser la latence). Attention, si l'hôte physique tombe en panne, toutes les instances du groupe seront indisponibles.

### Créer un groupe de serveurs via la console

{{% steps %}}

#### Accéder aux groupes de serveurs

Connectez-vous à la [console OpenStack](https://console.aucoeurdu.cloud/auth/login?referer=/). Dans le menu principal, allez dans **Compute** → **Groupes de serveurs**.

#### Créer un nouveau groupe

Cliquez sur le bouton **Créer un groupe de serveurs**.
1.  Donnez un **Nom** à votre groupe (ex: `web-ha`).
2.  Choisissez la **Politique** (ex: `anti-affinity`).
3.  Validez en cliquant sur **Envoyer**.

#### Lancer une instance dans le groupe

Lors de la création d'une instance (via le bouton **Lancer une instance**) :
1.  Configurez votre instance comme d'habitude (source, gabarit, réseaux...).
2.  Allez dans l'onglet **Groupes de serveurs**.
3.  Sélectionnez votre groupe dans la liste **Sélectionner un groupe de serveurs**.
4.  Lancez l'instance.

{{% /steps %}}

{{% callout type="info" %}}
Il existe généralement une limite sur le nombre de membres (instances) que l'on peut ajouter dans un groupe de serveurs (souvent liée à la taille du cluster physique pour l'anti-affinité).
{{% /callout %}}

### Via la CLI OpenStack

Voici les commandes pour gérer vos groupes de serveurs en ligne de commande.

```bash
# Lister les groupes de serveurs existants
openstack server group list

# Créer un groupe avec une politique d'anti-affinité
openstack server group create --policy anti-affinity web-ha

# Créer un groupe avec une politique d'affinité
openstack server group create --policy affinity backend-perf

# Afficher les détails d'un groupe (pour récupérer son ID par exemple)
openstack server group show web-ha

# Lancer une instance dans un groupe spécifique
# Remplacez <GROUP_ID> par l'ID ou le nom du groupe
openstack server create --flavor m1.small --image rocky-9 \
  --network private --hint group=web-ha \
  mon-serveur-web-1
  
# Supprimer un groupe de serveurs (il doit être vide)
openstack server group delete web-ha
```
