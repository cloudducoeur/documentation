---
title: 'Métriques'
description:
draft: false
type: docs
weight: 1
aliases:
  - /doc/environnements/observabilite/utilisation/
---

Les métriques sont stockées dans la région **Chartres | CHA** du Cloud du Coeur
et conservées sur une durée glissante d'un an.

## Demander un tenant

Chaque nouveau projet doit disposer de son propre tenant VictoriaMetrics. Avant
d'utiliser les endpoints de lecture ou d'écriture, créez un ticket dans
[Tickoeur](https://tickoeur.restosducoeur.org/) à destination de l'équipe du
Cloud du Coeur afin qu'elle crée un tenant associé au projet.

## Documentation

{{< cards >}}
	{{< card link="comment-ca-marche" title="Comment ça marche ?" subtitle="Comprenez la collecte et le stockage des métriques." icon="document-text" >}}
	{{< card link="ecrire" title="Écrire la donnée" subtitle="Envoyez vos métriques vers la plateforme d'observabilité." icon="upload" >}}
	{{< card link="lire" title="Lire la donnée" subtitle="Interrogez les données collectées par la plateforme." icon="search" >}}
	{{< card link="visualiser" title="Visualiser la donnée" subtitle="Explorez vos métriques dans des tableaux de bord." icon="chart-bar" >}}
{{< /cards >}}
