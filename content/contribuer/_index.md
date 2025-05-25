---
title: 'Comment contribuer ?'
description:
draft: false
type: docs
---

## Au projet ?

Si vous souhaitez nous aider sur ce projet, n'hésites pas à nous contacter par e-mail :

- [cloudducoeur@restosducoeur.org](cloudducoeur@restosducoeur.org)

## A cette documentation ?

Si vous souhaitez apporter votre contribution à cette documentation, suivez ce guide pour vous aider à bien commencer et à ajouter vos modifications !

<img src="./cdc-illustration-contribuer.png" alt="Contribuer" style="width: 30%;">

### Familiarisez-vous avec le guide de style

Il n'est pas obligatoire de lire le guide de style, mais il est important de s'y référer lors de vos contributions.

Prenez donc le temps de lire le guide une première fois pour vous assurer que la documentation est familière à toute personne qui la consulte.

{{< cards cols="1" >}}
  {{< card link="/guides" title="Documentation guide de style" icon="document-text" >}}
{{< /cards >}}

### Créer votre propre copie de la documentation

Commençons par forker et cloner le dépôt de documentation.

{{% steps %}}

#### Forking

Allez sur [cloudducoeur/documentation](https://github.com/cloudducoeur/documentation).

Cliquez sur le bouton **{{< icon "fork" >}} Fork** en haut à droite pour créer votre propre copie

#### Cloner le dépôt

Clonez votre fork fraîchement créé.

Cliquez sur l'onglet `Code` > `SSH`. Copiez l'adresse du dépôt.

Ouvrez un terminal à l'endroit désiré et clonez avec

```shell
git clone <URL copiée>
# exemple : git clone git@github.com:cloudducoeur/documentation.git
```

#### Démarrer l'environnement local

{{< callout type="info" >}}
Vous devez avoir installé [Docker](https://docs.docker.com/engine/install/) et [Docker Compose](https://docs.docker.com/compose/install/) pour continuer.
{{< /callout >}}

Entrez dans le nouveau répertoire créé (par défaut, `documentation`), et exécutez simplement :

```shell
docker compose up
```

Ceci téléchargera une image Docker et démarrera le serveur `hugo` en mode développement.

Vous pouvez consulter la documentation en visitant [localhost:1313](http://localhost:1313).

Toute modification de fichier sera rechargée à chaud et rafraîchira la page dans votre navigateur. Pratique !

#### Créer une nouvelle branche

Créez une branche pour ajouter votre contribution. Elle sera utilisée plus tard pour faire une **Pull Request**.
```Shell
git switch -c my-contrib
```

{{% /steps %}}

### Quel type de changement voulez-vous effectuer ?

{{< cards cols="1" >}}
  {{< card link="add-new-page" title="Ajouter une nouvelle page de documentation" icon="document-add" >}}
  {{< card link="update-page" title="Mettre à jour une page existante" icon="pencil-alt" >}}
  {{< card link="quick-fix" title="Corriger rapidement quelque chose" icon="lightning-bolt" >}}
{{< /cards >}}

### Commit, push et Pull Request !

Une fois que vous avez fini de faire vos changements, validez-les.

```shell
git add <fichier1> <fichier2>
git commit -m « <message pour les changements que j'ai effectués> »
```

Puis poussez-les :

```shell
git push origin my-contrib # utilise le nom de la branche défini précédemment
```

Utilisez le lien du résultat de `git push` pour créer la **Pull Request** !

#### Extensions recommandées

GoHugo [le site web maintient une liste](https://gohugo.io/tools/editors/) d'extensions sympas à avoir dans votre éditeur de choix lorsque vous utilisez GoHugo.

Si vous utilisez VSCode, utilisez au moins ces deux extensions :

- [Hugo Language and Syntax Support](https://marketplace.visualstudio.com/items?itemName=budparr.language-hugo-vscode)
- [Front Matter CMS](https://marketplace.visualstudio.com/items?itemName=eliostruyf.vscode-front-matter)
