---
title: "Le manifeste"
linkTitle: "Le manifest"
description:
draft: false
type: docs
---

<img src="./cdc-illustration-manifesto.png" alt="Illustration du manifeste" width="35%" />

## Objectif principal

Réduire drastiquement les coûts d'hébergement tout en fournissant une infrastructure cloud privée fiable, durable, ouverte et mutualisée, au service des associations départementales et de l'association nationale des Restos du Cœur.

## Les points fondateurs

### Maîtrise des coûts

#### Priorité absolue : L'argent

L’infrastructure a pour vocation première de réduire les coûts globaux liés à l’hébergement. Chaque décision technique est guidée par la maîtrise budgétaire.

<img src="./cdc-illustration-argent.png" alt="Illustration de l'argent" width="35%" />

#### Dons & réutilisation

99% de l’infrastructure repose sur du matériel issu de dons. L’acquisition de matériel doit prioritairement passer par la récupération, sauf pour les consommables. Une stratégie active de recherche de dons doit être mise en place.

### Fiabilité et performances

#### Disponibilité

La plateforme doit répondre aux besoins métiers avec des garanties minimales de disponibilité.

<img src="./cdc-illustration-server.png" alt="Illustration des serveurs" width="45%" />

#### Contrôle de la consommation

Les machines ne doivent être allumées qu’en cas de besoin. La consommation énergétique doit être monitorée et optimisée, car elle représente le seul coût variable direct.

### Une plateforme ouverte

Fourniture d’une infrastructure mutualisée inspirée des standards AWS, Azure, GCP. Abstraction de l’infrastructure pour simplifier l’usage par les utilisateurs internes. Chaque association ou acteur peut accéder à la plateforme selon ses besoins de manière sécurisée.

### Valeurs et culture

#### Collaboration & communication

Approche DevOps : équipes développement et exploitation travaillent ensemble dès la conception. Responsabilité partagée du cycle de vie complet des applications.

#### Automatisation

CI/CD systématique pour les déploiements (via Git, Ansible, etc.). Infrastructure as Code (IaC) pour tout ce qui peut être automatisé.

#### Culture du Feedback

Systèmes de monitoring et d’alerting en place. Pratique des blameless postmortems après incidents.

#### Documentation & transparence

Chaque brique doit être documentée, y compris :

- Son architecture

- Les alertes associées (runbook)

- Le dépôt Git contenant son code et README à jour

### Technologies et innovations

#### Open Source d’abord

Aucune licence commerciale coûteuse ne peut être envisagée. Le choix se porte sur des solutions libres et pérennes (Proxmox, OpenStack, Linux, Ceph, etc.).

#### Innovation libre

La plateforme sert aussi de bac à sable pour expérimenter des solutions bénéfiques pour l’association. Toute proposition d’innovation est encouragée, tant qu’elle respecte les principes de sobriété, de simplicité et de partage.

### Expertise et agilité

Les déploiements doivent suivre les principes Agile pour favoriser l'amélioration continue. L'équipe infrastructure agit en support et conseil technique auprès des autres associations.

L’ensemble du projet repose sur une approche communautaire et solidaire :

- Pas de savoir ou d’outil "privatisé"

- Toute contribution doit être partagée, documentée, et accessible

## Conclusion

Ce manifeste est un engagement collectif à maintenir une infrastructure éthique, ouverte, sobre, partagée, et orientée vers l’intérêt général.
Il constitue une boussole pour les choix technologiques et organisationnels à venir. Toute initiative doit s’y référer.
