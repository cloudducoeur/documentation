---
title: "Ma paire de clés"
description: "Créez et gérez vos clés SSH pour vous connecter à vos instances."
draft: false
type: docs
---

<img src="./cdc-illustration-osk-keys.gif" alt="OpenStack Keys" style="width: 25%;">

Une **paire de clés SSH** est indispensable pour vous connecter de manière sécurisée à vos instances. Elle se compose d'une **clé publique** (stockée sur l'instance) et d'une **clé privée** (conservée sur votre poste).

### Créer une paire de clés depuis la console

{{% steps %}}

#### Accéder à la gestion des clés

Connectez-vous à la [console OpenStack](https://console.aucoeurdu.cloud/auth/login?referer=/), puis rendez-vous dans **Compute** → **Paires de clés**.

#### Créer une nouvelle paire de clés

Cliquez sur **Créer une paire de clés**, puis renseignez un nom (par exemple `ma-cle-ssh`).

#### Télécharger la clé privée

La clé privée est automatiquement téléchargée par votre navigateur. **Conservez-la en lieu sûr**, elle ne pourra pas être re-téléchargée.

```bash
# Restreindre les permissions de la clé privée
chmod 600 ~/Downloads/ma-cle-ssh.pem
```

{{% /steps %}}

{{% callout type="warning" %}}
Si vous perdez votre clé privée, vous ne pourrez plus vous connecter aux instances qui l'utilisent. Il faudra alors créer une nouvelle paire de clés et recréer l'instance.
{{% /callout %}}

### Importer une clé publique existante

Si vous avez déjà une clé SSH sur votre poste, vous pouvez importer uniquement la clé publique :

{{% steps %}}

#### Récupérer votre clé publique

```bash
cat ~/.ssh/id_rsa.pub
```

Copiez le contenu affiché.

#### Importer dans la console

Dans **Compute** → **Paires de clés**, cliquez sur **Importer une clé publique**. Collez le contenu de votre clé publique et donnez-lui un nom.

{{% /steps %}}

### Générer une clé SSH sur votre poste

Si vous n'avez pas encore de clé SSH :

{{< tabs items="macOS / Linux,Windows" >}}
{{< tab >}}
```bash
ssh-keygen -t ed25519 -C "mon-email@restosducoeur.org"
```
Validez les options par défaut. Votre clé sera créée dans `~/.ssh/id_ed25519`.
{{< /tab >}}
{{< tab >}}
Ouvrez **PowerShell** et exécutez :
```powershell
ssh-keygen -t ed25519 -C "mon-email@restosducoeur.org"
```
La clé sera créée dans `C:\Users\<votre-utilisateur>\.ssh\id_ed25519`.
{{< /tab >}}
{{< /tabs >}}

### Via la CLI OpenStack

```bash
# Lister vos paires de clés
openstack keypair list

# Créer une paire de clés et sauvegarder la clé privée
openstack keypair create ma-cle-ssh > ma-cle-ssh.pem
chmod 600 ma-cle-ssh.pem

# Importer une clé publique existante
openstack keypair create --public-key ~/.ssh/id_ed25519.pub ma-cle-ssh

# Supprimer une paire de clés
openstack keypair delete ma-cle-ssh
```
