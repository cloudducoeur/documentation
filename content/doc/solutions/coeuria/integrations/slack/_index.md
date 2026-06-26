---
title: 'Slack'
description:
draft: false
type: docs
---

![](./cdc-illustration-slack.png)

Ce tutoriel explique comment connecter votre compte Slack personnel à LibreChat. Une fois configuré, vous pourrez demander à l'assistant de lire vos canaux, chercher des messages, envoyer des messages, etc. — directement depuis le chat.

### Ce dont vous avez besoin

- Un compte Slack avec accès à votre workspace
- Un accès à CoeurIA - LibreChat (fourni par votre administrateur)
- Environ 10 minutes

### Le faire

{{% steps %}}

#### Créer une application Slack

1. Rendez-vous sur [api.slack.com/apps](api.slack.com/apps) et connectez-vous avec votre compte Slack.

2. Cliquez sur **Create New App**.

3. Choisissez **From scratch**.

4. Donnez un nom à votre app (par exemple : Slack CoeurIA) et sélectionnez votre workspace.

5. Cliquez sur **Create App**.

#### Activer le MCP Slack

1. Dans le menu de gauche, cliquez sur Agents & AI Apps.

2. Activez l'option Slack Model Context Protocol (MCP) Server (nécessaire pour que mcp.slack.com accepte votre token).

> Attention : Si cette section n'apparaît pas, contactez l'administrateur de votre workspace Slack — il peut être nécessaire qu'il active cette fonctionnalité au niveau de l'organisation.

#### Ajouter les permissions (User Token Scopes)

1. Dans le menu gauche, cliquez sur OAuth & Permissions.

2. Faites défiler jusqu'à la section Scopes.

3. Dans **User Token Scopes** (pas Bot Token Scopes), cliquez sur **Add an OAuth Scope** et ajoutez les scopes suivants un par un :

| Scope | Ce que ça permet |
|---------|------------------|
| `channels:read` | Lister les canaux publics |
| `channels:history` | Lire les messages des canaux publics |
| `groups:read` | Lister les canaux privés |
| `groups:history` | Lire les messages des canaux privés |
| `im:read` | Lister vos messages directs |
| `im:history` | Lire vos messages directs |
| `mpim:read` | Lister vos conversations de groupe |
| `mpim:history` | Lire vos conversations de groupe |
| `users:read` | Voir les informations des membres |
| `search:read` | Rechercher des messages dans le workspace |
| `chat:write` | Envoyer des messages |

Ajoutez au minimum les scopes dont vous avez besoin. Si vous n'avez pas besoin d'envoyer des messages, vous pouvez omettre chat:write.

#### Installer l'application dans votre workspace

1. Toujours dans **OAuth & Permissions**, remontez en haut de la page.

2. Cliquez sur **Install to Workspace**.

3. Slack vous affiche un écran de confirmation des permissions — cliquez sur **Allow**.

4. Vous êtes redirigé vers la page **OAuth & Permissions**. Vous verrez apparaître votre **User OAuth Token**, qui commence par `xoxp-`.

#### Copier votre User Token

Copiez le token `xoxp-...` affiché sous **OAuth Tokens for Your Workspace → User OAuth Token**.

> Attention : Traitez ce token comme un mot de passe. Il donne accès à votre compte Slack. Ne le partagez jamais.

#### Configurer CoeurIA (LibreChat)

1. Ouvrez LibreChat dans votre navigateur.

2. Dans le panneau de droite, cherchez la section **MCP Settings**. (Ou lors de la sélection d'un outil en conversation, cliquez sur l'icône ⚙️ à côté de "slack".)

3. Un dialogue s'affiche avec un champ **Slack User Token**.

4. Collez votre token `xoxp-...` et validez.

LibreChat stocke ce token de façon chiffrée, associé à votre compte uniquement.

#### Tester la connexion 

Dans une conversation CoeurIA (LibreChat), essayez par exemple :

```
"Liste mes canaux Slack les plus récents"
```

ou

```
"Cherche dans Slack les messages mentionnant 'réunion budget'"
```

Si l'assistant répond avec des données de votre workspace, la configuration est réussie. 🎉

{{% /steps %}}

### En cas de problème 

| Symptôme | Solution |
|-----------|----------|
| `missing_token` ou `invalid_token` | Vérifiez que vous avez bien copié le token `xoxp-` complet |
| `missing_scope` | Retournez sur `api.slack.com/apps`, ajoutez le scope manquant et réinstallez l'application |
| L'option **MCP Settings** est absente | Contactez votre administrateur LibreChat |
| `App not approved` | Votre administrateur Slack doit approuver l'activation MCP dans le workspace |

### Révoquer l'accès

Si vous souhaitez déconnecter LibreChat de Slack, rendez-vous sur [api.slack.com/apps](api.slack.com/apps), sélectionnez votre app, puis **OAuth & Permissions → Revoke Token**.
