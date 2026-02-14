---
title: "Nos IP publiques"
description: "Rendez vos instances accessibles depuis Internet avec les IP flottantes."
draft: false
type: docs
---

Pour qu'une instance soit joignable depuis l'extérieur (Internet), vous devez lui associer une **IP Flottante** (Floating IP). C'est une adresse IP publique routable qui est mappée (NAT 1:1) vers l'adresse IP privée de votre instance.

### Gérer les IP flottantes via la console

{{% steps %}}

#### Allouer une IP

1.  Allez dans **Réseau** → **IP flottantes**.
2.  Cliquez sur **Allouer une IP au projet**.
3.  Choisissez le pool (généralement `public`).
4.  Cliquez sur **Allouer une IP**.

#### Associer à une instance

1.  Dans la liste des IP flottantes, repérez celle que vous venez d'allouer.
2.  Cliquez sur **Associer**.
3.  Sélectionnez le **Port à associer** (correspondant à votre instance et son adresse IP privée).
4.  Cliquez sur **Associer**.

{{% /steps %}}

{{% callout type="info" %}}
L'instance ne "voit" pas cette IP publique directement sur son interface réseau (elle ne voit que son IP privée). La translation d'adresse est gérée par le routeur virtuel.
{{% /callout %}}

### Via la CLI OpenStack

```bash
# Créer une IP flottante
openstack floating ip create public

# Lister les IP flottantes (pour récupérer l'adresse ou l'ID)
openstack floating ip list

# Associer une IP à une instance
openstack server add floating ip <INSTANCE_NAME> <FLOATING_IP_ADDRESS>

# Dissocier une IP
openstack server remove floating ip <INSTANCE_NAME> <FLOATING_IP_ADDRESS>

# Libérer une IP (la rendre au pool)
openstack floating ip delete <FLOATING_IP_ADDRESS>
```
