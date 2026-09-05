---
title: 'Comment ça marche ?'
description:
draft: false
type: docs
---

Parce que nous faisons les choses en toute transparence, il est important pour nous de vous partager comment ça marche.

[**VictoriaMetrics**](https://victoriametrics.com/) est la base de données qui stocke les métriques du Cloud du Coeur.

Une métrique est une valeur mesurée dans le temps. Par exemple :

- une machine est-elle disponible ?
- combien de mémoire est utilisée ?
- combien de requêtes reçoit une application ?
- combien de temps met un service à répondre ?

<img src="./cdc-howitworks-animation.gif" alt="Fonctionnement de VictoriaMetrics dans le Cloud du Coeur" style="width:80%;">

## Le chemin d'une métrique

Dans le contexte du *Cloud du Coeur*, le fonctionnement est le suivant :

1. Votre application ou votre serveur expose des métriques.
2. Un agent les collecte.
3. L'agent les envoie vers VictoriaMetrics.
4. VictoriaMetrics les stocke dans le tenant de votre projet.
5. Grafana lit ces métriques pour afficher des tableaux de bord.

En résumé :

```text
Application ou serveur -> Agent de collecte -> VictoriaMetrics -> Grafana
```

## Le tenant projet

Chaque projet dispose de son propre tenant VictoriaMetrics.

Le tenant sert à séparer les données : les métriques d'un projet ne sont pas mélangées avec celles des autres projets.

Avant d'envoyer ou de lire des métriques, il faut donc demander la création d'un tenant à l'équipe du Cloud du Coeur via [Tickoeur](https://tickoeur.restosducoeur.org/).

## À retenir

- VictoriaMetrics stocke les métriques.
- Grafana les affiche.
- Chaque projet a son propre tenant.
- Les métriques sont stockées dans la région **Chartres | CHA**.
- Pour commencer, il faut demander un tenant à l'équipe du Cloud du Coeur.
