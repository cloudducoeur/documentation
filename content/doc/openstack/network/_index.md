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

### Par où commencer ?

{{< cards >}}
  {{< card link="networks" title="Les réseaux" subtitle="Créez vos réseaux privés isolés." icon="globe" >}}
  {{< card link="routers" title="Les routeurs" subtitle="Connectez vos réseaux au monde extérieur." icon="switch-horizontal" >}}
  {{< card link="security-groups" title="Groupes de sécurité" subtitle="Gérez le pare-feu de vos instances." icon="shield-check" >}}
  {{< card link="public-ip-range" title="Nos IP publiques" subtitle="Gérez l'accès depuis Internet." icon="globe-alt" >}}
  {{< card link="load-balancers" title="Load Balancers" subtitle="Distribuez la charge sur vos instances." icon="scale" >}}
{{< /cards >}}
