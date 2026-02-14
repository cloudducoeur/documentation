---
title: "Les groupes de sécurité"
description: "Gérez le pare-feu de vos instances."
draft: false
type: docs
---

Les **groupes de sécurité** agissent comme un pare-feu virtuel au niveau de l'instance. Tout trafic entrant est bloqué par défaut, sauf si une règle l'autorise explicitement.

### Gérer les règles via la console

{{% steps %}}

#### Accéder aux groupes

Allez dans **Réseau** → **Groupes de sécurité**. Vous verrez un groupe `default` préexistant qui autorise tout le trafic sortant et le trafic entrant entre membres du même groupe.

#### Créer un nouveau groupe

1.  Cliquez sur **Créer un groupe de sécurité**.
2.  Nommez-le (ex: `web-server` ou `ssh-only`).
3.  Validez.

#### Ajouter des règles

1.  Cliquez sur le bouton **Gérer les règles** à droite de votre groupe.
2.  Cliquez sur **Ajouter une règle**.
3.  Exemple pour **SSH** :
    *   Règle: `SSH`
    *   CIDR distant: `0.0.0.0/0` (ou votre IP de bureau pour plus de sécurité).
4.  Exemple pour **HTTP/HTTPS** :
    *   Règle: `HTTP` / `HTTPS`
    *   CIDR distant: `0.0.0.0/0`.
5.  Cliquez sur **Ajouter**.

{{% /steps %}}

### Appliquer un groupe de sécurité à une instance

Vous pouvez assigner un ou plusieurs groupes de sécurité à une instance :
*   **Lors de la création** : Dans l'onglet "Groupes de sécurité".
*   **Après création** : Menu déroulant de l'instance → **Modifier les groupes de sécurité**.

### Via la CLI OpenStack

```bash
# Créer un groupe de sécurité
openstack security group create web-server

# Autoriser SSH (port 22)
openstack security group rule create --proto tcp --dst-port 22 web-server

# Autoriser HTTP (port 80)
openstack security group rule create --proto tcp --dst-port 80 web-server

# Autoriser HTTPS (port 443)
openstack security group rule create --proto tcp --dst-port 443 web-server

# Lister les groupes
openstack security group list
```
