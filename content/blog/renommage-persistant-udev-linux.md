---
title: Renommer ses interfaces réseau pour isoler les usages
date: 2025-05-27
authors:
  - name: juhnny5
    link: https://github.com/juhnny5
    image: https://github.com/juhnny5.png
tags:
  - Network
  - Infrastructure
  - IaC
excludeSearch: true
---

<img src="/img/cdc-illustration-renommage-persistant-udev.png" alt="Serveurs physiques" style="width: 35%;">

La gestion des interfaces réseau sur Linux, notamment dans des environnements virtualisés ou à haute disponibilité, nécessite une identification claire et persistante des interfaces physiques. Cet article explique pourquoi et comment automatiser le renommage des interfaces réseau à l’aide d’**Ansible** et de règles `udev`, afin de garantir une administration simplifiée et fiable.

## Pourquoi renommer les interfaces réseau ?

Pour faciliter l'administration de nos machines, nous avons pris la décision de renommer les interfaces dites "[prédictibles](https://blog.devarieux.net/2015/08/comprendre-la-prediction-de-noms-des-interfaces-reseau-de-systemd.html)" des distributions Linux modernes. Pourquoi et comment ? Me direz-vous...

### Le contexte

En effet, à la place de `enoX` ou `enpXsX`, nous préférons utiliser des noms liés à l'usage de ces interfaces.

Sur nos serveurs qui fondent l'infrastructure du Cloud du Coeur (exemple : hyperviseurs OpenStack, noeuds réseau, etc), nous avons 4 interfaces physiques connectées pour la redondance.

| Interface physique      | Vitesse | Usage           | Nom souhaité |
|------------------------|---------|-----------------|--------------|
| 2x RJ45 on-board       | 1 Gbps  | Management      | mgt0, mgt1   |
| 2x QSFP (cartes dédiées)| 100 Gbps| Production      | prd0, prd1   |

Pour schématiser les interfaces d'un point de vue physique :

<img src="/img/renommage-persistant-udev-physical-server.png" alt="Serveurs physiques" style="width: 85%;">

Pour schématiser les interfaces d'un point de vue virtuel :

<img src="/img/renommage-persistant-udev-linux-bonds.png" alt="Linux bonds" style="width: 85%;">

### Quels sont les avantages ?

- **Clarté et maintenance facilitée** : Les noms `mgtX` et `prdX` permettent d’identifier immédiatement à quel usage correspond chaque interface physique.
- **Gestion simplifiée des bonds** : En regroupant les interfaces selon leur rôle, on peut facilement configurer et monitorer les bonds réseau dédiés à la gestion ou à la production.
- **Simplification en cas de remplacement d'une carte** : Il suffira de remplacer l'adresse MAC côté `udev` et la nouvelle interface récupèrera le même nom que l'ancienne et réintégrera automatiquement le bon agrégat.

## Passons à la technique

### Prérequis

- Accès root sur les machines cibles
- **Ansible** installé sur la machine de contrôle
- Facts Ansible collectés (`gather_facts: yes`)

### Comment appliquer (de manière automatisée) ?

Voici un bout de code `ansible`, outil utilisé chez nous pour le déploiement de configuration sur nos machines.

```yaml
---
- name: Rename network interfaces persistently using udev rules
  hosts: all
  become: true
  vars:
    udev_rules_file: /etc/udev/rules.d/10-network-interfaces.rules
    reboot_after: true
    disable_predictable_naming: true

  tasks:
    - name: Filter physical interfaces (exclude loopback, docker, veth, bridge, bond, virbr)
      set_fact:
        physical_ifaces: >-
          {{
            ansible_interfaces
            | reject('match', '^lo$')
            | reject('match', '^docker.*')
            | reject('match', '^veth.*')
            | reject('match', '^br.*')
            | reject('match', '^bond.*')
            | reject('match', '^virbr.*')
            | list
          }}

    - name: Collect MAC and speed data for each physical interface
      set_fact:
        iface_data: >-
          {{
            iface_data | default([]) + [{
              "name": item,
              "mac": hostvars[inventory_hostname]['ansible_' + item]['macaddress'] | default(''),
              "speed": hostvars[inventory_hostname]['ansible_' + item]['speed'] | default(0)
            }]
          }}
      loop: "{{ physical_ifaces }}"
      when: hostvars[inventory_hostname]['ansible_' + item] is defined and
            hostvars[inventory_hostname]['ansible_' + item]['macaddress'] is defined

    - name: Separate 1G (MGT) and 10G+ (PRD) interfaces
      set_fact:
        mgt_ifaces: "{{ iface_data | selectattr('speed', '==', 1000) | list }}"
        prd_ifaces: "{{ iface_data | selectattr('speed', '>=', 10000) | list }}"

    - name: Debug classified physical interfaces
      debug:
        msg:
          - "MGT interfaces (1G): {{ mgt_ifaces }}"
          - "PRD interfaces (10G+): {{ prd_ifaces }}"

    - name: Generate udev rules content
      set_fact:
        udev_rules: |
          {% for iface in mgt_ifaces %}
          SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="{{ iface.mac }}", NAME="mgt{{ loop.index0 }}"
          {% endfor %}
          {% for iface in prd_ifaces %}
          SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="{{ iface.mac }}", NAME="prd{{ loop.index0 }}"
          {% endfor %}

    - name: Show generated udev rules
      debug:
        var: udev_rules

    - name: Write udev rules to file
      copy:
        dest: "{{ udev_rules_file }}"
        content: "{{ udev_rules }}"
        owner: root
        group: root
        mode: '0644'

    - name: Disable predictable interface names (optional)
      file:
        path: /etc/udev/rules.d/80-net-setup-link.rules
        state: link
        src: /dev/null
      when: disable_predictable_naming

    - name: Reboot system if required
      reboot:
        msg: "Reboot required after applying udev rules"
        reboot_timeout: 300
      when: reboot_after and udev_rules | length > 0
```

{{< callout type="info" >}}
  Stockez le contenu dans un fichier *yaml* qui pourrait se nommer `rename-interfaces.yml` par exemple.
{{< /callout >}}

### Application

Pour appliquer le playbook :

```bash
ansible-playbook -i hosts rename-interfaces.yml
```

### Vérification

Après redémarrage, vérifiez que les interfaces portent bien les nouveaux noms :

```bash
ip link show
# ou
ls /sys/class/net
```

Vous devriez voir apparaître les interfaces `mgt0`, `mgt1`, `prd0`, `prd1`.

### Rollback

Pour revenir en arrière, il suffit de supprimer le fichier de règles udev :

```bash
rm /etc/udev/rules.d/10-network-interfaces.rules
reboot
```

## Liens complémentaires

- [Documentation officielle Ansible](https://docs.ansible.com/)
- [Documentation officielle udev](https://www.freedesktop.org/software/systemd/man/udev.html)
- [Comprendre la prédiction de noms des interfaces réseau de systemd](https://blog.devarieux.net/2015/08/comprendre-la-prediction-de-noms-des-interfaces-reseau-de-systemd.html)

---

Grâce à cette méthode, la gestion des interfaces réseau devient plus claire, plus fiable et plus facilement automatisable, même lors de changements matériels.
