---
title: "Développer"
description:
draft: false
type: docs
---

<img src="./cdc-illustration-developper.png" alt="Développer" style="width: 35%;">

Pour automatiser la gestion de votre infrastructure sur le Cloud du Coeur avec OpenStack, vous pouvez utiliser des outils d’infrastructure as code comme [Terraform](https://developer.hashicorp.com/terraform), [OpenTofu](https://opentofu.org/) ou [Pulumi](https://www.pulumi.com/).

Voici comment initialiser un dépôt avec chacun de ces outils :

{{< tabs items="Terraform,OpenTofu,Pulumi" >}}

{{< tab >}}
### Initialiser un dépôt **Terraform** pour OpenStack

1. Créer un dossier pour votre projet :
   ```bash
   mkdir mon-projet-terraform && cd mon-projet-terraform
   ```

2. Créer un fichier `main.tf` avec le provider OpenStack :
   ```hcl
   terraform {
     required_providers {
       openstack = {
         source  = "terraform-provider-openstack/openstack"
         version = "~> 1.0"
       }
     }
   }

   provider "openstack" {
     auth_url    = var.auth_url
     tenant_name = var.tenant_name
     user_name   = var.user_name
     password    = var.password
     domain_name = var.domain_name
     region      = var.region
   }
   ```

3. Créer un fichier `variables.tf` pour vos variables d’authentification.

4. Initialiser le projet :
   ```bash
   terraform init
   ```

5. Configurer vos variables (via un fichier `.tfvars` ou des variables d’environnement).

Pour plus d’informations, voir la [doc officielle Terraform OpenStack](https://registry.terraform.io/providers/terraform-provider-openstack/openstack/latest/docs).
{{< /tab >}}

{{< tab >}}
### Initialiser un dépôt **OpenTofu** pour OpenStack

OpenTofu fonctionne comme Terraform, il suffit de remplacer la commande `terraform` par `tofu` :

1. Créer un dossier pour votre projet :
   ```bash
   mkdir mon-projet-tofu && cd mon-projet-tofu
   ```

2. **Créer un fichier `main.tf` avec le provider OpenStack** (voir exemple Terraform ci-dessus).

3. Initialiser le projet :
   ```bash
   tofu init
   ```

4. Configurer vos variables (via un fichier `.tfvars` ou des variables d’environnement).

Pour plus d’informations, voir la [doc OpenTofu](https://opentofu.org/docs/intro).
{{< /tab >}}

{{< tab >}}
### Initialiser un dépôt **Pulumi** pour OpenStack

1. Créer un dossier pour votre projet :
   ```bash
   mkdir mon-projet-pulumi && cd mon-projet-pulumi
   ```

2. Initialiser un projet Pulumi (ex : en TypeScript) :
   ```bash
   pulumi new openstack-typescript
   ```

3. Configurer vos variables d’authentification dans le fichier `Pulumi.<stack>.yaml` ou via variables d’environnement :
   - `OS_AUTH_URL`
   - `OS_USERNAME`
   - `OS_PASSWORD`
   - `OS_TENANT_NAME`
   - `OS_DOMAIN_NAME`
   - `OS_REGION_NAME`

4. Installer le provider OpenStack si besoin :
   ```bash
   npm install @pulumi/openstack
   ```

5. Développer votre infrastructure dans le fichier `index.ts` (ou équivalent).

Pour plus d’informations, voir la [doc Pulumi OpenStack](https://www.pulumi.com/registry/packages/openstack/).
{{< /tab >}}

{{< /tabs >}}