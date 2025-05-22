---
title: 'Comment ça marche ?'
description:
draft: false
type: docs
---

Le Cloud du Coeur utilise une technologie Open Source qui se nomme [OpenStack](https://www.openstack.org/). Cette technologie vise à fournir "*as a service*" différents éléments d'infrastructure nécessitant autrefois, une dépendance à une équipe pour la mise à disposition de ressources d'infrastructure.

OpenStack, sous le capot, fournit un ensemble de micro-services exposant des APIs (ce que l'on appelle des ["contrats d'API"](/en-savoir-plus/comment-ca-marche/vocabulaire/)) pour rendre cette infrastructure accessible et consommable.

Voici une vue globale de ces micro-services et des interractions entres-eux :

![](./cdc-openstack-fonctionnement.png)

Tous ces services sont en finalité accessibles via :

- [Une console](https://console.aucoeurdu.cloud)
- [Une API](https://api.chartres.aucoeurdu.cloud), utilisable via `terraform`, `opentofu` ou `pulumi`.
- [Une CLI](/doc/cli/)
