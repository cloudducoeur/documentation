---
title: "Le DNS"
description: "Créez et gérez vos propres noms de domaine."
draft: false
type: docs
---

<img src="./cdc-illustration-dns.png" alt="OpenStack DNS" style="width: 70%;">

Le service DNS d'OpenStack (Designate) vous permet de gérer vos zones et vos enregistrements directement depuis votre projet.

Vous pouvez, par exemple, publier une application avec un nom de domaine lisible (`api.example.tld`) plutôt qu'avec une adresse IP.

### Concepts

*   **Zone DNS** : Conteneur principal d'un domaine (ex: `example.tld.`).
*   **Recordset** : Ensemble d'enregistrements de même nom et même type.
*   **Types d'enregistrements** :
	*   **A / AAAA** : Associe un nom à une adresse IPv4/IPv6.
	*   **CNAME** : Alias vers un autre nom DNS.
	*   **MX** : Serveur de messagerie.
	*   **TXT** : Texte libre (SPF, vérifications, etc.).
*   **TTL** : Durée de cache DNS (en secondes).

### Créer une zone DNS via la console

{{% steps %}}

#### Créer la zone

1.  Allez dans **Réseau** → **DNS** → **Zones**.
2.  Cliquez sur **Créer une zone**.
3.  Renseignez :
	*   **Nom de zone** (ex: `example.tld.`).
	*   **Adresse e-mail administrateur** (format DNS, ex: `admin@example.tld`).
	*   **Description** (optionnel).
4.  Validez la création.

#### Ajouter un enregistrement

1.  Ouvrez votre zone puis allez dans l'onglet **Recordsets**.
2.  Cliquez sur **Créer un recordset**.
3.  Choisissez le type (ex: `A`) et le nom (ex: `www`).
4.  Saisissez la valeur (ex: IP flottante de votre service).
5.  Définissez un TTL (ex: `300`) et validez.

{{% /steps %}}

{{% callout type="info" %}}
Pensez a pointer vos enregistrements vers une IP stable (par exemple une IP flottante ou un load balancer) pour eviter de changer la zone DNS a chaque redeploiement d'instance.
{{% /callout %}}

### Via la CLI OpenStack

```bash
# Creer une zone
openstack zone create --email admin@example.tld example.tld.

# Lister les zones
openstack zone list

# Creer un enregistrement A (www.example.tld. -> 203.0.113.10)
openstack recordset create --type A --record 203.0.113.10 --ttl 300 example.tld. www

# Creer un enregistrement CNAME (api.example.tld. -> www.example.tld.)
openstack recordset create --type CNAME --record www.example.tld. --ttl 300 example.tld. api

# Lister les enregistrements d'une zone
openstack recordset list example.tld.

# Supprimer un enregistrement
openstack recordset delete example.tld. www
```

### Bonnes pratiques

*   Utilisez un **TTL court** (`300`) pendant les migrations, puis augmentez-le en regime stable.
*   Evitez de cibler directement une IP d'instance ephemere.
*   Nommez vos enregistrements de maniere explicite (`api`, `grafana`, `mail`, etc.).
*   Documentez les enregistrements critiques (MX, SPF, DKIM, DMARC).
