---
title: "Database"
description: "Créez et gérez vos propres bases de données."
draft: false
type: docs
---

Le service Database d'OpenStack (Trove) permet de déployer des bases de donnees managées sans gerer vous-meme les machines virtuelles, le stockage et les operations de base.

Vous pouvez créer rapidement une instance de base de donnees (MySQL, PostgreSQL, etc. selon disponibilite) et l'utiliser depuis vos applications.

### Concepts

*   **Database Instance** : Instance managée de moteur de base de données.
*   **Datastore** : Type de moteur (ex: MySQL, PostgreSQL) et sa version.
*   **Flavor** : Taille de l'instance (vCPU, RAM).
*   **Volume** : Stockage persistant de la base.
*   **Utilisateur / Base** : Comptes et schemas applicatifs crees sur l'instance.

### Datastores disponibles (Trove)

| Datastore | Nom Trove (CLI) | Cas d'usage principal |
| --- | --- | --- |
| MariaDB / MySQL | `mysql` | Applications web, CMS, outils métier classiques |
| PostgreSQL | `postgresql` | Applications transactionnelles, analytics, besoins SQL avancés |

Les versions disponibles peuvent evoluer selon l'environnement OpenStack. Pour afficher la liste exacte des versions sur votre projet :

```bash
openstack database datastore version list <DATASTORE>
```

### Creer une base de donnees via la console

{{% steps %}}

#### Creer l'instance Trove

1.  Allez dans **Database** → **Instances**.
2.  Cliquez sur **Create Database Instance**.
3.  Renseignez :
		*   **Nom** (ex: `db-prod`).
		*   **Datastore** et **version**.
		*   **Flavor** adapte a la charge.
		*   **Taille du volume** (ex: `20` Go).
		*   **Reseau prive** autorise.
4.  Definissez l'utilisateur administrateur.
5.  Validez et attendez le statut `ACTIVE`.

#### Creer une base applicative

1.  Ouvrez votre instance.
2.  Allez dans l'onglet **Databases**.
3.  Cliquez sur **Create Database** (ex: `app_db`).
4.  Creez ensuite un utilisateur dedie (ex: `app_user`) avec les droits necessaires.

{{% /steps %}}

{{% callout type="info" %}}
Limitez l'acces à votre base via les groupes de sécurité et les réseaux prives. Evitez d'exposer directement votre instance de base de donnees sur Internet.
{{% /callout %}}

### Via la CLI OpenStack

```bash
# Lister les datastores et versions disponibles
openstack database datastore list
openstack database datastore version list <DATASTORE>

# Creer une instance Trove
openstack database instance create db-prod \
	--flavor db.small \
	--size 20 \
	--datastore mysql \
	--datastore-version 8.0

# Suivre l'etat de l'instance
openstack database instance list
openstack database instance show db-prod

# Creer une base
openstack database db create app_db --instance db-prod

# Creer un utilisateur
openstack database user create app_user <MOT_DE_PASSE> --instance db-prod --database app_db

# Supprimer une instance
openstack database instance delete db-prod
```

### Bonnes pratiques

*   Creez un utilisateur dedié par application (pas de compte partage).
*   Activez une strategie de sauvegarde regulière adaptée à vôtre RPO/RTO.
*   Surveillez CPU, RAM, IOPS et latence pour anticiper les changements de flavor.
*   Testez les procedures de restauration, pas uniquement les sauvegardes.
