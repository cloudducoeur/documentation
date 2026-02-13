---
title: 'Le vocabulaire'
description:
draft: false
type: docs
---

Pour bien comprendre le fonctionnement du Cloud du Coeur, il faut prendre en compte un certain vocabulaire.

| Notion   | Définition |
| --------  | -------- |
| **Contrat d'API** | C'est un document qui définit précisément comment une API fonctionne, en décrivant les données attendues en entrée, les réponses possibles, et les règles d’interaction entre le client et le serveur.|
| **CLI** | Interface en ligne de commande (*Command Line Interface*). Outil permettant d'interagir avec les services du Cloud du Cœur via un terminal, en tapant des commandes textuelles plutôt qu'en utilisant une interface graphique. |
| **OpenStack** | Plateforme open source de Cloud Computing utilisée par le Cloud du Cœur. Elle fournit les services de calcul (Nova), réseau (Neutron), stockage (Cinder) et gestion d'images (Glance). |
| **Flavors** | Gabarits qui définissent les ressources matérielles allouées à une instance : nombre de vCPU, quantité de RAM, taille du disque et niveau de performance I/O. |
| **Images** | Modèles de systèmes d'exploitation (Debian, Ubuntu, AlmaLinux…) utilisés pour démarrer une instance. Elles contiennent le système de base et le logiciel `cloud-init` pour la configuration automatique. |
| **Compute** | Service de calcul d'OpenStack (Nova) qui permet de créer, gérer et supprimer des machines virtuelles (instances). |
| **Gitlab** | Forge logicielle open source utilisée par le Cloud du Cœur pour héberger le code source, gérer les projets et faciliter la collaboration via Git. |
