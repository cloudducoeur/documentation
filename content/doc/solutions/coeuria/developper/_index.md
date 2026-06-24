---
title: 'Développer'
description:
draft: false
type: docs
---

<img src="./cdc-illustration-developper.gif" alt="CoeurIA - Developper" style="width: 35%;">

Une des capacités de CoeurIA est d'aider au développement.

Cette page présente une base de configuration pour utiliser CoeurIA dans des outils orientés développement.

## Prérequis

Avant de commencer, vérifiez les éléments suivants :

- Vous disposez d'un compte `@restosducoeur.org`.
- Vous avez un accès CoeurIA opérationnel.
- Vous avez une clé d'API CoeurIA.
- Vous utilisez un éditeur compatible (VS Code recommandé).

{{< callout type="warning" >}}
Ne stockez jamais votre clé d'API dans un dépôt Git. Utilisez les variables d'environnement ou le gestionnaire de secrets de votre machine.
{{< /callout >}}

## OpenCode

[OpenCode](https://opencode.ai/) peut être branché sur CoeurIA pour assister l'écriture, la relecture et l'amélioration de code.

### Étapes d'intégration

{{% steps %}}

#### Installer OpenCode

Installez OpenCode sur votre poste.

#### Créer un profil CoeurIA

Créez un profil ou un provider dédié à CoeurIA.

#### Configurer l'endpoint

Configurez un endpoint compatible OpenAI.

#### Choisir le modèle

Sélectionnez un modèle disponible dans CoeurIA.

#### Valider l'intégration

Lancez un premier test (exemple : "explique cette fonction").

{{% /steps %}}

Exemple de paramètres à renseigner dans OpenCode :

```txt
Provider: OpenAI-compatible
Base URL: https://ai-gateway.par.aucoeurdu.cloud
API Key: <votre-cle-api>
Model: <modele-coeuria>
```

### Conseils d'usage

- Donnez du contexte métier dans vos prompts.
- Précisez le langage, le framework et la contrainte attendue.
- Demandez des modifications incrémentales plutôt qu'une réécriture complète.
- Validez systématiquement le code proposé avant commit.

## Continue.dev

[Continue.dev](https://github.com/continuedev/continue) s'intègre directement dans VS Code et peut utiliser CoeurIA comme fournisseur de modèle.

### Étapes d'intégration

{{% steps %}}

#### Installer l'extension Continue.dev

Installez l'extension Continue.dev dans VS Code.

#### Ouvrir la configuration

Ouvrez la configuration Continue.dev.

#### Ajouter le modèle CoeurIA

Ajoutez une entrée de modèle pointant vers CoeurIA.

#### Vérifier l'authentification

Vérifiez que l'authentification fonctionne.

#### Tester dans le projet

Testez avec une demande simple sur un fichier du projet.

{{% /steps %}}

Exemple de configuration Continue.dev (à adapter) :

```yaml
models:
	- name: CoeurIA
		provider: openai
		model: <modele-coeuria>
		apiBase: https://ai-gateway.par.aucoeurdu.cloud
		apiKey: $COEURIA_API_KEY
```

### Bonnes pratiques dans Continue.dev

- Ouvrez le bon dossier de projet pour fournir un contexte utile.
- Ajoutez des règles de style de code dans vos instructions.
- Utilisez la relecture ciblée (fonctions, fichiers, diff) avant fusion.
- Conservez un contrôle humain sur les changements sensibles.

## Recommandations générales

- Commencez par des demandes courtes et précises.
- Ajoutez progressivement les contraintes techniques.
- Exigez des explications sur les choix proposés.
- Faites toujours passer tests et linters avant déploiement.
