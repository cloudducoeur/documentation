---
title: 'Les guides du Cloud du Coeur'
description:
draft: false
type: docs
---

A travers le ***Cloud du Coeur***, nous offrons 2 types d'hébergements :

- [Hébergement Web mutualisé](https://doc.aucoeurdu.cloud/guides/cloudpanel/) : Vous possèdez une console (CloudPanel) et vous êtes autonome sur cette dernière. Idéal pour les petits sites qui n'ont pas vocation à recevoir un très gros trafic.
- [Hébergement Cloud OpenStack](https://doc.aucoeurdu.cloud/guides/openstack/) : C'est la [console](https://console.aucoeurdu.cloud) fournie pour que vous puissiez créer et héberger vos applications "at-scale". Que ça soit en la déployant avec une base de données managée ou via un cluster **Kubernetes** tout frais.

Ainsi qu'une plateforme d'[observabilité](https://doc.aucoeurdu.cloud/guides/observabilite/) commune :

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
