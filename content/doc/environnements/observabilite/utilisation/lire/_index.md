---
title: 'Lire la donnée'
description:
draft: false
type: docs
---

<img src="./cdc-illustration-metrics.png" alt="Observabilité" style="width:80%;">

## Endpoint de lecture

Les métriques sont consultables via l'adresse suivante :

```text
https://metrics-read.cha.aucoeurdu.cloud
```

Chaque projet dispose de son propre tenant. Remplacez `<tenant>` par
l'identifiant associé à votre projet :

```text
https://metrics-read.cha.aucoeurdu.cloud/select/<tenant>/prometheus/api/v1/query
```

Pour exécuter une requête PromQL, utilisez par exemple l'API HTTP de
VictoriaMetrics :

```bash
curl --get \
	'https://metrics-read.cha.aucoeurdu.cloud/select/<tenant>/prometheus/api/v1/query' \
	--data-urlencode 'query=up'
```

Le tenant isole les métriques du projet. Une requête ne peut donc consulter
que les données du tenant utilisé dans l'URL.
