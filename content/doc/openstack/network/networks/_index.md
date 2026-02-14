---
title: "Les réseaux"
description: "Créez vos réseaux privés isolés (VXLAN)."
draft: false
type: docs
---

Dans votre projet, vous pouvez créer autant de réseaux privés que nécessaire pour isoler vos environnements (ex: Prod, Preprod, Dev) ou vos tiers applicatifs (Front, Back, DB).

### Créer un réseau via la console

{{% steps %}}

#### Aller dans l'interface Réseau

Dans le menu principal, cliquez sur **Réseau** → **Réseaux**.

#### Créer le réseau

Cliquez sur **Créer un réseau**.
1.  **Réseau** : Donnez un nom (ex: `network-int`). Laissez "Case activée d'administration" coché.
2.  **Sous-réseau** : Donnez un nom (ex: `subnet-int`) et définissez l'adresse réseau en CIDR (ex: `192.168.10.0/24`).
3.  **Détails du sous-réseau** : Vous pouvez laisser les options par défaut (DHCP activé) et définir les serveurs DNS (ex: `1.1.1.1` ou `8.8.8.8`).
4.  Cliquez sur **Créer**.

{{% /steps %}}

### Via la CLI OpenStack

```bash
# Créer le réseau
openstack network create network-int

# Créer le sous-réseau associé
openstack subnet create --network network-int \
  --subnet-range 192.168.10.0/24 \
  --dns-nameserver 1.1.1.1 \
  subnet-int

# Lister les réseaux
openstack network list
```
