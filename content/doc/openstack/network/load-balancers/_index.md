---
title: "Les répartiteurs de charges"
description: "Distribuez le trafic réseau sur plusieurs instances avec Octavia."
draft: false
type: docs
---

Le service d'équilibrage de charge (Load Balancer as a Service - Octavia) permet de distribuer les requêtes entrantes vers un pool d'instances, améliorant ainsi la performance et la fiabilité de vos applications.

### Concepts

*   **Load Balancer** : L'entité principale, qui porte l'adresse IP virtuelle (VIP).
*   **Listener** : Écoute sur un port spécifique (ex: 80 ou 443).
*   **Pool** : Groupe de serveurs backend qui vont traiter les requêtes.
*   **Member** : Les instances (serveurs) membres du pool.
*   **Health Monitor** : Vérifie la santé des membres pour ne pas envoyer de trafic vers une instance en panne.

### Créer un Load Balancer via la console

{{% steps %}}

#### Créer le Load Balancer

1.  Allez dans **Réseau** → **Répartiteurs de charge**.
2.  Cliquez sur **Créer un répartiteur de charge**.
3.  **Détails** : Nommez-le (ex: `lb-web`). Choisissez le sous-réseau privé où il sera déployé.
4.  **Auditeur (Listener)** : Ajoutez un écouteur (ex: Port 80, Protocole HTTP ou TCP).
5.  **Pool** : Créez un pool (ex: `pool-web`) associé à l'écouteur. Choisissez l'algorithme (ex: `ROUND_ROBIN` ou `LEAST_CONNECTIONS`).
6.  **Membres** : Ajoutez vos instances existantes au pool, en spécifiant le port sur lequel elles écoutent (ex: 80).
7.  **Moniteur** : Configurez le health check (ex: Type `HTTP`, Url `/healthing`).

#### Attacher une IP Flottante (Optionnel)

Si votre Load Balancer doit être accessible depuis Internet :
1.  Dans la liste des répartiteurs de charge, cliquez sur le menu à droite de votre LB.
2.  Choisissez **Associer une IP flottante**.

{{% /steps %}}

### Via la CLI OpenStack

La configuration complète d'un LB est plus complexe en CLI, voici les étapes principales :

```bash
# 1. Créer le Load Balancer
openstack loadbalancer create --name lb-web --vip-subnet-id <SUBNET_ID>

# 2. Créer un Listener (ex: HTTP 80)
openstack loadbalancer listener create --name listener-http --protocol HTTP --protocol-port 80 lb-web

# 3. Créer un Pool
openstack loadbalancer pool create --name pool-web --lb-algorithm ROUND_ROBIN --listener listener-http --protocol HTTP

# 4. Ajouter des membres (instances)
openstack loadbalancer member create --subnet-id <SUBNET_ID> --address <INSTANCE_IP_1> --protocol-port 80 pool-web
openstack loadbalancer member create --subnet-id <SUBNET_ID> --address <INSTANCE_IP_2> --protocol-port 80 pool-web

# 5. Créer un Health Monitor
openstack loadbalancer healthmonitor create --delay 5 --max-retries 4 --timeout 10 --type HTTP --url-path / pool-web
```
