---
title: 'Accéder à CloudPanel'
description:
draft: false
type: docs
---

CloudPanel est l'interface mise à disposition des hébergements Web pour les services internes des Restos (dans les antennes). Cette console permet d'administrer, de manière autonome, les sites exposés, les bases de données, l'envoie du code de l'application, etc.

Cette console est mise à disposition par antenne/service (exemple `ad75`). Pour y accéder, vous devez vous connecter sur l'URL mise à disposition et utiliser l'identifiant fournit par l'équipe du Cloud du Coeur. Si vous ne possèdez plus cet identifiant, rendez-vous [ici](/doc/aide/).

L'URL de la console est disponible sous le format :

- [https://console.adXX.rdcnet.org](https://console.adXX.rdcnet.org)

Maintenant, veuillez vous connecter avec votre identifiant fournit et votre mot de passe.

![](./cdc-cloudpanel-login-page-capture.png)

{{< callout type="info" >}}
  A noter que chaque console mise à disposition dispose de son tableau de bord de status pour visualiser rapidement l'état de l'ensemble des services qui vous sont mis à disposition.

  Exemple : [https://status.infra.rdcnet.org/status/adXX](https://status.infra.rdcnet.org/status/adXX)

{{< /callout >}}

Une fois connecté(e), vous accéderez à ce tableau de bord :

![](./cdc-cloudpanel-dashboard-capture.png)

Cette page est découpée comme suit :

- **Tableau de bord** : Visualiser rapidement les informations de la machine hébergeant mon site internet, pratique notamment dans un cas où le site est lent, ça évite ainsi de devoir contacter le support.
- **Sites** : Comme son nom l'indique, c'est ici que vous allez pouvoir gérer vos sites (gérer, créer, supprimer).
- **Accès administrateur-trice** : Permet d'agir sur les services faisant tourner votre site, par exemple : redémarrer le service `nginx` sans avoir à passer également par le support.
