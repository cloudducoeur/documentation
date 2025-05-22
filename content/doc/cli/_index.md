---
title: "OpenStack CLI"
description:
draft: false
type: docs
---

Cette documentation concerne l'installation de la ligne de commande OpenStack, OpenStack étant le logiciel utilisé pour faire tourner le Cloud du Coeur.

<img src="./cdc-illustration-cli.png" alt="CLI OpenStack" style="width: 25%;">

{{% steps %}}

## L'installer

En fonction du système d'exploitation sur lequel vous êtes, vous trouver la documentation d'installation associée.

{{< tabs items="macOS,GNU/Linux,Windows" >}}

{{< tab >}}
Sur **macOS**, pour installer la CLI `openstack`, vous devez utiliser le gestionnaire de paquets **Homebrew**.

Pour installer la CLI :

```bash
brew install openstackclient
```

{{< /tab >}}

{{< tab >}}
Sur **GNU/Linux**, pour installer la CLI `openstack`, l'installation se fait via les packages `python3` associés.

Pour installer la CLI :

#### Sur Ubuntu (24.04, 22.04 ou 20.04)

```bash
sudo apt install python python3-dev python3-pip
sudo pip install python3-openstackclient
```

#### Sur CentOS (8, 9)

```bash
sudo dnf install python-openstackclient
```

{{< /tab >}}

{{< /tabs >}}

## S'authentifier

Une fois que la CLI est installée, vous devez configurer la CLI en fonction de votre système d'exploitation pour pouvoir vous connecter à la plateforme du *Cloud du Coeur*.

{{< tabs items="macOS,GNU/Linux,Windows" >}}

{{< tab >}}
Il faudra se connecter dans l'interface (console) et récupérer votre fichier `.<project name>-openrc.sh`. Ce fichier sera à ajouter dans `$HOME/.<project name>-openrc.sh`.

Une fois que c'est fait, pour utiliser la CLI et connecter cette dernière à la plateforme du *Cloud du Coeur*, il faut charger les informations :

```bash
source $HOME/.<project name>-openrc.sh
```

Vérifier que ça fonctionne en listant les images disponibles dans le catalogue :

```bash
openstack image list
```

{{< /tab >}}

{{< /tabs >}}

{{% /steps %}}