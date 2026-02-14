---
title: "Les routeurs"
description: "Connectez vos réseaux privés au monde extérieur."
draft: false
type: docs
---

Les routeurs virtuels permettent à vos instances de communiquer avec Internet (via SNAT ou Floating IP) et interconnectent différents réseaux privés entre eux.

### Créer et configurer un routeur via la console

{{% steps %}}

#### Créer le routeur

1.  Allez dans **Réseau** → **Routeurs**.
2.  Cliquez sur **Créer un routeur**.
3.  Nommez-le (ex: `router-gateway`).
4.  Dans **Réseau externe**, sélectionnez le réseau public disponible (généralement `public` ou `ext-net`).
5.  Validez.

#### Connecter un réseau privé

1.  Cliquez sur le nom de votre routeur nouvellement créé.
2.  Allez dans l'onglet **Interfaces**.
3.  Cliquez sur **Ajouter une interface**.
4.  Sélectionnez votre sous-réseau privé (ex: `subnet-int`).
5.  Cliquez sur **Envoyer**.

{{% /steps %}}

{{% callout type="info" %}}
Dès que le routeur est connecté à la fois au réseau externe et à votre sous-réseau privé, les instances de ce sous-réseau disposent automatiquement d'un accès sortant vers Internet (grâce au SNAT).
{{% /callout %}}

### Via la CLI OpenStack

```bash
# Créer le routeur
openstack router create router-gateway

# Définir la passerelle externe (le réseau public)
openstack router set --external-gateway public router-gateway

# Ajouter une interface vers votre sous-réseau privé
openstack router add subnet router-gateway subnet-int

# Lister les routeurs
openstack router list
```
