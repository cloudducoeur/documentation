---
title: 'Les guides du Cloud du Coeur'
description:
draft: false
type: docs
---

A travers le ***Cloud du Coeur***, nous offrons 2 types d'hébergements :

- **Hébergement mutualisé** : Vous possèdez une console (CloudPanel) et vous êtes autonome sur cette dernière. Idéal pour les petits sites qui n'ont pas vocation à recevoir un très gros trafic.
- **Hébergement Cloud OpenStack** : C'est la [console](https://console.aucoeurdu.cloud) fournie pour que vous puissiez créer et héberger vos applications "at-scale". Que ça soit en la déployant avec une base de données managée ou via un cluster **Kubernetes** tout frais.

Ainsi qu'une plateforme d'**observabilité** commune :

- Une [console unique](https://observabilite.aucoeurdu.cloud/login) permettant d'accéder aux différentes données applicatives avec la possibilité de créer vos propres tableaux de bord.

<img src="./cdc-guides.png" alt="Guides du Cloud du Coeur" style="width: 85%;">

## Technologies

Suivez étape par étape pour déployer différents types de services déjà documentés et utilisés sur la plateforme.

{{< cards >}}
  {{< card link="hebergement-web-wordpress" title="Wordpress" subtitle="Vous avez besoin d'héberger un service Wordpress" icon="wordpress" >}}
  {{< card link="hebergement-php" title="PHP 7 ou 8" subtitle="Vous avez besoin d'héberger un service PHP 7 ou 8" icon="php" >}}
  {{< card link="hebergement-python" title="Python 3" subtitle="Vous avez besoin d'héberger un service Python 3" icon="python" >}}
  {{< card link="hebergement-posgresql" title="PosgreSQL" subtitle="Vous avez besoin d'une base de données PosgreSQL" icon="pg" >}}
  {{< card link="hebergement-mariadb" title="MariaDB" subtitle="Vous avez besoin d'une base de données MariaDB/MySQL" icon="mysql" >}}
  {{< card link="hebergement-kubernetes" title="Kubernetes" subtitle="Vous avez besoin d'un cluster Kubernetes" icon="kubernetes" >}}
{{< /cards >}}

## Tutoriels

Vous cherchez de l'aide précise sur un sujet, il existe déjà peut-être un tutoriel pour vous aider.

### Hébergement Web mutualisé (CloudPanel)

{{< cards >}}
  {{< card link="tuto-hebergement-web-cloudpanel" title="Accéder à CloudPanel" subtitle="Vous chercher à accéder à la console d'hébergement de votre application" icon="user" >}}
  {{< card link="tuto-hebergement-creer-un-site" title="Créer un site" subtitle="Comment créer mon site sur CloudPanel ?" icon="code" >}}
  {{< card link="tuto-hebergement-creer-une-base-de-données" title="Créer une base de données" subtitle="Et pour stocker les données de mon application ?" icon="code" >}}
  {{< card link="tuto-hebergement-importer-une-base-de-données" title="Importer une base de données (migration)" subtitle="Pour migrer mon application..." icon="code" >}}
  {{< card link="tuto-hebergement-web-pousser-code" title="Pousser son code" subtitle="Pousser mon code en ligne? Facile!" icon="upload" >}}
  {{< card link="tuto-hebergement-web-consulter-les-logs" title="Consulter les logs" subtitle="Mon app ne va pas très bien, heureusement que j'ai mes logs!" icon="pencil-alt" >}}
{{< /cards >}}

### Observabilité (Grafana)

{{< cards >}}
  {{< card link="tuto-observabilite-account" title="Accéder à Grafana" subtitle="Vous chercher à accéder à la visualisation des données d'observabilité" icon="user" >}}
{{< /cards >}}

### Hébergement Cloud (OpenStack)

{{< cards >}}
  {{< card link="tuto-openstack-account" title="Accéder à la console OpenStack" subtitle="Vous chercher à vous connecter à la console ?" icon="user" >}}
  {{< card link="tuto-openstack-nouveau-projet" title="Créer un nouveau projet" subtitle="Une nouvelle idée ? Un nouveau projet ? :)" icon="pencil-alt" >}}
{{< /cards >}}
