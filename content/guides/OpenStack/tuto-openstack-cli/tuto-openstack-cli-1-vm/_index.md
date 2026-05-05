---
title: 'Création d'une VM'
description: 'Toutes les commandes...'
draft: false
type: docs
---

## Création d'une VM dans OpenStack

### Informations nécessaires

Information nécessaires pour créer une VM sur OpenStack:

- Création du réseau
- Création du subnet
- Création du security group


### Commandes à utiliser pour la création du réseaux, subnet et security group

```Shell
openstack network create <NOM_RESEAU>
openstack subnet create --network <NOM_RESEAU> --subnet-range 192.168.100.0/24 <NOM_SUBNET>
openstack security group create --stateful <SG_NAME>
openstack security group rule create --egress <SG_NAME>
openstack security group rule create --ingress --dst-port 22:22 --protocol tcp <SG_NAME>
openstack security group rule create --ingress --dst-port 5001:5002 --protocol tcp <SG_NAME>
openstack security group rule create --ingress --protocol icmp <SG_NAME>
```


### Exemple d'exécution des commandes

#### Notes

Dans les exemples suivants, nous allons utiliser les valeurs suivantes:

- <NOM_RESEAU> : dsh-net
- <NOM_SUBNET> : dsh-subnet
- <SG_NAME> :  dsh-sg

Ces valeurs sont arbitraires et ne sont là que pour illustrer ce tutoriel.
A ajuster par rapport à votre contexte.


#### Exemples

##### Création du réseau pour la future VM

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack network create dsh-net
+---------------------------+--------------------------------------+
| Field                     | Value                                |
+---------------------------+--------------------------------------+
| admin_state_up            | UP                                   |
| availability_zone_hints   | par1                                 |
| availability_zones        |                                      |
| created_at                | 2026-04-20T19:58:00Z                 |
| description               |                                      |
| dns_domain                | None                                 |
| id                        | fe0ac9c3-cc2d-42a5-85bc-c52df78e9fc8 |
| ipv4_address_scope        | None                                 |
| ipv6_address_scope        | None                                 |
| is_default                | False                                |
| is_vlan_qinq              | None                                 |
| is_vlan_transparent       | None                                 |
| l2_adjacency              | True                                 |
| mtu                       | 1450                                 |
| name                      | dsh-net                              |
| port_security_enabled     | True                                 |
| project_id                | 58ee6d9139d24a5287e9f81009fe22b8     |
| provider:network_type     | None                                 |
| provider:physical_network | None                                 |
| provider:segmentation_id  | None                                 |
| qos_policy_id             | None                                 |
| revision_number           | 1                                    |
| router:external           | Internal                             |
| segments                  | None                                 |
| shared                    | False                                |
| status                    | ACTIVE                               |
| subnets                   |                                      |
| tags                      |                                      |
| updated_at                | 2026-04-20T19:58:00Z                 |
+---------------------------+--------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$ 
```


##### Création du sous-réseau IP interne pour la VM

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack subnet create --network dsh-net --subnet-range 192.168.100.0/24 dsh-subnet
+----------------------+--------------------------------------+
| Field                | Value                                |
+----------------------+--------------------------------------+
| allocation_pools     | 192.168.100.2-192.168.100.254        |
| cidr                 | 192.168.100.0/24                     |
| created_at           | 2026-04-20T20:01:22Z                 |
| description          |                                      |
| dns_nameservers      |                                      |
| dns_publish_fixed_ip | None                                 |
| enable_dhcp          | True                                 |
| gateway_ip           | 192.168.100.1                        |
| host_routes          |                                      |
| id                   | 1fdb0da3-a51b-4b6a-9008-851cab8c0997 |
| ip_version           | 4                                    |
| ipv6_address_mode    | None                                 |
| ipv6_ra_mode         | None                                 |
| name                 | dsh-subnet                           |
| network_id           | fe0ac9c3-cc2d-42a5-85bc-c52df78e9fc8 |
| project_id           | 58ee6d9139d24a5287e9f81009fe22b8     |
| revision_number      | 0                                    |
| router:external      | False                                |
| segment_id           | None                                 |
| service_types        |                                      |
| subnetpool_id        | None                                 |
| tags                 |                                      |
| updated_at           | 2026-04-20T20:01:22Z                 |
+----------------------+--------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$
```


##### Création du groupe de sécurité

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack security group create --stateful dsh-sg
+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
| Field           | Value                                                                                                                                            |
+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
| created_at      | 2026-04-20T20:04:55Z                                                                                                                             |
| description     | dsh-sg                                                                                                                                           |
| id              | 4962eaec-4238-45b6-99e6-036d5d34b6cd                                                                                                             |
| is_shared       | False                                                                                                                                            |
| name            | dsh-sg                                                                                                                                           |
| project_id      | 58ee6d9139d24a5287e9f81009fe22b8                                                                                                                 |
| revision_number | 1                                                                                                                                                |
| rules           | created_at='2026-04-20T20:04:55Z', direction='egress', ethertype='IPv4', id='1c347cc8-3be0-409b-ad57-708ccf64d678', standard_attr_id='1006',     |
|                 | updated_at='2026-04-20T20:04:55Z'                                                                                                                |
|                 | created_at='2026-04-20T20:04:55Z', direction='egress', ethertype='IPv6', id='48c531ef-34ce-4b65-a166-d25b86787c04', standard_attr_id='1007',     |
|                 | updated_at='2026-04-20T20:04:55Z'                                                                                                                |
| stateful        | True                                                                                                                                             |
| tags            | []                                                                                                                                               |
| updated_at      | 2026-04-20T20:04:55Z                                                                                                                             |
+-----------------+--------------------------------------------------------------------------------------------------------------------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$ 
```


##### Création des régles de sécurité associées au groupe de sécurité

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack security group rule create --egress dsh-sg
Error while executing command: ConflictException: 409, Security group rule already exists. Rule id is 1c347cc8-3be0-409b-ad57-708ccf64d678.
(oskclient) ko@cdc:~/restos/openstack$ 
```


###### Accepte les connexions SSH en TCP sur le port IP 22

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack security group rule create --ingress --dst-port 22:22 --protocol tcp dsh-sg
+-------------------------+--------------------------------------+
| Field                   | Value                                |
+-------------------------+--------------------------------------+
| belongs_to_default_sg   | False                                |
| created_at              | 2026-04-20T20:08:42Z                 |
| description             |                                      |
| direction               | ingress                              |
| ether_type              | IPv4                                 |
| id                      | 16e44dd4-6f22-45ab-8ca0-3e956ae30d30 |
| normalized_cidr         | 0.0.0.0/0                            |
| port_range_max          | 22                                   |
| port_range_min          | 22                                   |
| project_id              | 58ee6d9139d24a5287e9f81009fe22b8     |
| protocol                | tcp                                  |
| remote_address_group_id | None                                 |
| remote_group_id         | None                                 |
| remote_ip_prefix        | 0.0.0.0/0                            |
| revision_number         | 0                                    |
| security_group_id       | 4962eaec-4238-45b6-99e6-036d5d34b6cd |
| updated_at              | 2026-04-20T20:08:42Z                 |
+-------------------------+--------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$ 
```


###### Accepte les pings en entrée

 ```
(oskclient) ko@cdc:~/restos/openstack$ openstack security group rule create --ingress --protocol icmp dsh-sg
+-------------------------+--------------------------------------+
| Field                   | Value                                |
+-------------------------+--------------------------------------+
| belongs_to_default_sg   | False                                |
| created_at              | 2026-04-20T20:10:15Z                 |
| description             |                                      |
| direction               | ingress                              |
| ether_type              | IPv4                                 |
| id                      | d88423ef-0273-46f3-a80f-f1bbe3f12c0d |
| normalized_cidr         | 0.0.0.0/0                            |
| port_range_max          | None                                 |
| port_range_min          | None                                 |
| project_id              | 58ee6d9139d24a5287e9f81009fe22b8     |
| protocol                | icmp                                 |
| remote_address_group_id | None                                 |
| remote_group_id         | None                                 |
| remote_ip_prefix        | 0.0.0.0/0                            |
| revision_number         | 0                                    |
| security_group_id       | 4962eaec-4238-45b6-99e6-036d5d34b6cd |
| updated_at              | 2026-04-20T20:10:15Z                 |
+-------------------------+--------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$
```


## Création de VMs

### Commandes à exécuter

```Shell
openstack server create --flavor a1-ram2-disk10-perf1 --image debian-13 --network <NOM_RESEAU> --key <KEY> --security-group <SG_NAME> <VM_NAME>

openstack router create <RT_NAME>
openstack router add subnet <RT_NAME> <NOM_SUBNET>
openstack router set --external-gateway public_interco <RT_NAME>

openstack floating ip create public_interco
openstack server add floating ip <VM_NAME> 151.242.68.XXX
```


### Exemple d'exécution des commandes

#### Notes

Dans les exemples suivants, nous allons utiliser les valeurs suivantes:

<NOM_RESEAU>, <NOM_SUBNET> et <SG_NAME> comme pour l'exemple précédent.

Plus les nouveaux éléments suivants :
- <KEY> : dsh-admin
  nom de la clé SSH asymétrique que vous avez ajouté pour ce projet? #TODO
- <VM_NAME> : test-say-1
  nom du futur objet VM
- <RT_NAME> : dsh-rt
  nom du futur objet routeur


Ces valeurs sont arbitraires et ne sont là que pour illustrer ce tutoriel.
A ajuster par rapport à votre contexte.


#### Exemples


##### Création de la VM

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack server create --flavor a1-ram2-disk10-perf1 --image debian-13 --network dsh-net --key dsh-admin --security-group dsh-sg test-say-1
+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
| Field                               | Value                                                                                                                        |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
| OS-DCF:diskConfig                   | MANUAL                                                                                                                       |
| OS-EXT-AZ:availability_zone         | None                                                                                                                         |
| OS-EXT-SRV-ATTR:host                | None                                                                                                                         |
| OS-EXT-SRV-ATTR:hostname            | test-say-1                                                                                                                   |
| OS-EXT-SRV-ATTR:hypervisor_hostname | None                                                                                                                         |
| OS-EXT-SRV-ATTR:instance_name       | None                                                                                                                         |
| OS-EXT-SRV-ATTR:kernel_id           | None                                                                                                                         |
| OS-EXT-SRV-ATTR:launch_index        | None                                                                                                                         |
| OS-EXT-SRV-ATTR:ramdisk_id          | None                                                                                                                         |
| OS-EXT-SRV-ATTR:reservation_id      | None                                                                                                                         |
| OS-EXT-SRV-ATTR:root_device_name    | None                                                                                                                         |
| OS-EXT-SRV-ATTR:user_data           | None                                                                                                                         |
| OS-EXT-STS:power_state              | N/A                                                                                                                          |
| OS-EXT-STS:task_state               | scheduling                                                                                                                   |
| OS-EXT-STS:vm_state                 | building                                                                                                                     |
| OS-SRV-USG:launched_at              | None                                                                                                                         |
| OS-SRV-USG:terminated_at            | None                                                                                                                         |
| accessIPv4                          | None                                                                                                                         |
| accessIPv6                          | None                                                                                                                         |
| addresses                           | N/A                                                                                                                          |
| adminPass                           | szuF3TEDLK48                                                                                                                 |
| config_drive                        | None                                                                                                                         |
| created                             | 2026-04-20T20:19:49Z                                                                                                         |
| description                         | None                                                                                                                         |
| flavor                              | description=, disk='10', ephemeral='0', extra_specs.gabarit='hv', id='a1-ram2-disk10-perf1', is_disabled=, is_public='True', |
|                                     | location=, name='a1-ram2-disk10-perf1', original_name='a1-ram2-disk10-perf1', ram='2048', rxtx_factor=, swap='0', vcpus='1'  |
| hostId                              | None                                                                                                                         |
| host_status                         | None                                                                                                                         |
| id                                  | d9017229-fe0e-4199-b31c-8606e80e7031                                                                                         |
| image                               | debian-13 (ae6f6a83-c61f-4968-8151-f5a344449c28)                                                                             |
| key_name                            | dsh-admin                                                                                                                    |
| locked                              | None                                                                                                                         |
| locked_reason                       | None                                                                                                                         |
| name                                | test-say-1                                                                                                                   |
| pinned_availability_zone            | None                                                                                                                         |
| progress                            | None                                                                                                                         |
| project_id                          | 58ee6d9139d24a5287e9f81009fe22b8                                                                                             |
| properties                          | None                                                                                                                         |
| scheduler_hints                     |                                                                                                                              |
| security_groups                     | name='4962eaec-4238-45b6-99e6-036d5d34b6cd'                                                                                  |
| server_groups                       | None                                                                                                                         |
| status                              | BUILD                                                                                                                        |
| tags                                |                                                                                                                              |
| trusted_image_certificates          | None                                                                                                                         |
| updated                             | 2026-04-20T20:19:49Z                                                                                                         |
| user_id                             | 7c948f20d95d2752af68e3326c44966baeec8bc2e50580291a7b8e7eaacb3c25                                                             |
| volumes_attached                    |                                                                                                                              |
+-------------------------------------+------------------------------------------------------------------------------------------------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$ 
```


##### Création du routeur

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack router create dsh-rt
+-------------------------+--------------------------------------+
| Field                   | Value                                |
+-------------------------+--------------------------------------+
| admin_state_up          | UP                                   |
| availability_zone_hints | par1                                 |
| availability_zones      |                                      |
| created_at              | 2026-04-20T20:21:14Z                 |
| description             |                                      |
| enable_ndp_proxy        | None                                 |
| external_gateway_info   | null                                 |
| flavor_id               | None                                 |
| id                      | 01f7deab-4473-4b9b-b4aa-a425d60717c2 |
| name                    | dsh-rt                               |
| project_id              | 58ee6d9139d24a5287e9f81009fe22b8     |
| revision_number         | 1                                    |
| routes                  |                                      |
| status                  | ACTIVE                               |
| tags                    |                                      |
| updated_at              | 2026-04-20T20:21:14Z                 |
+-------------------------+--------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$ 
```


##### Ajout du sous-réseau et de la passerelle Internet au routeur

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack router add subnet dsh-rt dsh-subnet
```


##### Ajout de la passerelle par défaut Internet au routeur

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack router set --external-gateway public_interco dsh-rt
```


##### Demande de réservation d'une adresse IP publique

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack floating ip create public_interco
+---------------------+--------------------------------------+
| Field               | Value                                |
+---------------------+--------------------------------------+
| created_at          | 2026-04-20T20:24:16Z                 |
| description         |                                      |
| dns_domain          | None                                 |
| dns_name            | None                                 |
| fixed_ip_address    | None                                 |
| floating_ip_address | 151.242.68.227                       |
| floating_network_id | 123a8d91-9a1c-40c7-8cbb-535e2ddc939d |
| id                  | dd8685fd-80e8-4e8c-a30c-abc04e4a80f9 |
| name                | 151.242.68.227                       |
| port_details        | None                                 |
| port_forwardings    | []                                   |
| port_id             | None                                 |
| project_id          | 58ee6d9139d24a5287e9f81009fe22b8     |
| qos_policy_id       | None                                 |
| revision_number     | 0                                    |
| router_id           | None                                 |
| status              | DOWN                                 |
| subnet_id           | None                                 |
| tags                | []                                   |
| updated_at          | 2026-04-20T20:24:16Z                 |
+---------------------+--------------------------------------+
(oskclient) ko@cdc:~/restos/openstack$ 
```


##### Affectation de l'adresse IP publique à la VM

```Shell
(oskclient) ko@cdc:~/restos/openstack$ openstack server add floating ip test-say-1 151.242.68.227
(oskclient) ko@cdc:~/restos/openstack$
```


## Connection à la VM

### Ping

```Shell
(oskclient) ko@cdc:~/restos/openstack$ ping 151.242.68.227
PING 151.242.68.227 (151.242.68.227) 56(84) bytes of data.
64 bytes from 151.242.68.227: icmp_seq=1 ttl=52 time=6.79 ms
^C
--- 151.242.68.227 ping statistics ---
1 packets transmitted, 1 received, 0% packet loss, time 0ms
rtt min/avg/max/mdev = 6.788/6.788/6.788/0.000 ms
(oskclient) ko@cdc:~/restos/openstack$
```


### SSH

```Shell
(oskclient) ko@cdc:~/restos/openstack$ ssh debian@151.242.68.227
The authenticity of host '151.242.68.227 (151.242.68.227)' can't be established.
ED25519 key fingerprint is SHA256:4AR4T3PoP1ywI+nvlbV4vKabGtHEGrVdHQ/Y0j314Cg.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '151.242.68.227' (ED25519) to the list of known hosts.
Enter passphrase for key '/home/ko/.ssh/id_ed25519':
Linux test-say-1 6.12.69+deb13-cloud-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.12.69-1 (2026-02-08) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
debian@test-say-1:~$ 
```


#### Volumes disques de la VM

```Shell
debian@test-say-1:~$ df -Thl
Filesystem     Type      Size  Used Avail Use% Mounted on
udev           devtmpfs  976M     0  976M   0% /dev
tmpfs          tmpfs     198M  468K  197M   1% /run
/dev/vda1      ext4      9.7G  594M  8.7G   7% /
tmpfs          tmpfs     988M     0  988M   0% /dev/shm
tmpfs          tmpfs     5.0M     0  5.0M   0% /run/lock
tmpfs          tmpfs     988M     0  988M   0% /tmp
tmpfs          tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-journald.service
tmpfs          tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-resolved.service
/dev/vda15     vfat      124M  8.7M  116M   8% /boot/efi
tmpfs          tmpfs     1.0M     0  1.0M   0% /run/credentials/systemd-networkd.service
tmpfs          tmpfs     1.0M     0  1.0M   0% /run/credentials/getty@tty1.service
tmpfs          tmpfs     1.0M     0  1.0M   0% /run/credentials/serial-getty@ttyS0.service
tmpfs          tmpfs     198M  4.0K  198M   1% /run/user/1000
debian@test-say-1:~$
```


#### Utilisation de mémoire de la VM

```Shell
debian@test-say-1:~$ free -h
               total        used        free      shared  buff/cache   available
Mem:           1.9Gi       208Mi       1.7Gi       472Ki       121Mi       1.7Gi
Swap:             0B          0B          0B
debian@test-say-1:~$
```


#### Identifica tion du processeur depuis la VM

```Shell
debian@test-say-1:~$ lscpu
Architecture:                x86_64
  CPU op-mode(s):            32-bit, 64-bit
  Address sizes:             40 bits physical, 48 bits virtual
  Byte Order:                Little Endian
CPU(s):                      1
  On-line CPU(s) list:       0
Vendor ID:                   GenuineIntel
  Model name:                Intel Core Processor (Haswell, no TSX, IBRS)
    CPU family:              6
    Model:                   60
    Thread(s) per core:      1
    Core(s) per socket:      1
    Socket(s):               1
    Stepping:                1
    BogoMIPS:                4799.99
    Flags:                   fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss syscall nx pdpe1gb rdtscp lm constan
                             t_tsc rep_good nopl xtopology cpuid tsc_known_freq pni pclmulqdq vmx ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_t
                             imer aes xsave avx f16c rdrand hypervisor lahf_lm abm cpuid_fault pti ssbd ibrs ibpb stibp tpr_shadow flexpriority ept vpid ept_ad fsgsba
                             se tsc_adjust bmi1 avx2 smep bmi2 erms invpcid xsaveopt arat vnmi umip md_clear arch_capabilities
Virtualization features:
  Virtualization:            VT-x
  Hypervisor vendor:         KVM
  Virtualization type:       full
Caches (sum of all):
  L1d:                       32 KiB (1 instance)
  L1i:                       32 KiB (1 instance)
  L2:                        4 MiB (1 instance)
  L3:                        16 MiB (1 instance)
NUMA:
  NUMA node(s):              1
  NUMA node0 CPU(s):         0
Vulnerabilities:
  Gather data sampling:      Not affected
  Indirect target selection: Mitigation; Aligned branch/return thunks
  Itlb multihit:             Not affected
  L1tf:                      Mitigation; PTE Inversion; VMX flush not necessary, SMT disabled
  Mds:                       Mitigation; Clear CPU buffers; SMT Host state unknown
  Meltdown:                  Mitigation; PTI
  Mmio stale data:           Unknown: No mitigations
  Reg file data sampling:    Not affected
  Retbleed:                  Not affected
  Spec rstack overflow:      Not affected
  Spec store bypass:         Mitigation; Speculative Store Bypass disabled via prctl
  Spectre v1:                Mitigation; usercopy/swapgs barriers and __user pointer sanitization
  Spectre v2:                Mitigation; Retpolines; IBPB conditional; IBRS_FW; STIBP disabled; RSB filling; PBRSB-eIBRS Not affected; BHI Retpoline
  Srbds:                     Unknown: Dependent on hypervisor status
  Tsa:                       Not affected
  Tsx async abort:           Not affected
  Vmscape:                   Not affected
debian@test-say-1:~$ 
```
