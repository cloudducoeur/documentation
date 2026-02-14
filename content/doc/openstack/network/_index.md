---
title: "Network"
description: "Comprendre et configurer le réseau dans votre projet OpenStack."
draft: false
type: docs
---

Le service réseau d'OpenStack (Neutron) vous permet de construire des architectures réseaux complètes et isolées dans le cloud.

### Concepts clés

*   **Réseaux (Networks)** : Segments de communication L2 isolés.
*   **Sous-réseaux (Subnets)** : Plages d'adresses IP (IPAM).
*   **Routeurs** : Assurent la connectivité entre vos réseaux privés et le réseau externe (Internet).
*   **Groupes de sécurité** : Pare-feu distribués appliqués directement aux instances.
*   **IP Flottantes (Floating IPs)** : Adresses IP publiques attachées dynamiquement à vos instances.
*   **Répartiteurs de charge (Load Balancers)** : Distribution du trafic vers plusieurs instances.

Dans cette section, nous détaillons comment configurer chacun de ces composants.
