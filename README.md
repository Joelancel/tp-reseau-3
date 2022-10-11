# TP3 : On va router des trucs


➜ Pour ce TP, on va se servir de VMs Rocky Linux. 1Go RAM c'est large large. Vous pouvez redescendre la mémoire vidéo aussi.  

➜ Vous aurez besoin de deux réseaux host-only dans VirtualBox :

- un premier réseau `10.3.1.0/24`
- le second `10.3.2.0/24`
- **vous devrez désactiver le DHCP de votre hyperviseur (VirtualBox) et définir les IPs de vos VMs de façon statique**

➜ Les firewalls de vos VMs doivent **toujours** être actifs (et donc correctement configurés).

➜ **Si vous voyez le p'tit pote 🦈 c'est qu'il y a un PCAP à produire et à mettre dans votre dépôt git de rendu.**

## I. ARP

Première partie simple, on va avoir besoin de 2 VMs.

| Machine  | `10.3.1.0/24` |
|----------|---------------|
| `john`   | `10.3.1.11`   |
| `marcel` | `10.3.1.12`   |

```schema
   john               marcel
  ┌─────┐             ┌─────┐
  │     │    ┌───┐    │     │
  │     ├────┤ho1├────┤     │
  └─────┘    └───┘    └─────┘
```

> Référez-vous au [mémo Réseau Rocky](../../cours/memo/rocky_network.md) pour connaître les commandes nécessaire à la réalisation de cette partie.

### 1. Echange ARP

🌞**Générer des requêtes ARP**

- PING 10.3.1.12 (10.3.1.12) 56(84) bytes of data.
```
64 bytes from 10.3.1.12: icmp_seq=1 ttl=64 time=0.235 ms
64 bytes from 10.3.1.12: icmp_seq=2 ttl=64 time=0.282 ms
64 bytes from 10.3.1.12: icmp_seq=3 ttl=64 time=0.289 ms
64 bytes from 10.3.1.12: icmp_seq=4 ttl=64 time=0.250 ms
64 bytes from 10.3.1.12: icmp_seq=5 ttl=64 time=0.271 ms
64 bytes from 10.3.1.12: icmp_seq=6 ttl=64 time=0.280 ms
64 bytes from 10.3.1.12: icmp_seq=7 ttl=64 time=0.208 ms
64 bytes from 10.3.1.12: icmp_seq=8 ttl=64 time=0.297 ms
64 bytes from 10.3.1.12: icmp_seq=9 ttl=64 time=0.301 ms
64 bytes from 10.3.1.12: icmp_seq=10 ttl=64 time=0.271 ms
64 bytes from 10.3.1.12: icmp_seq=11 ttl=64 time=0.275 ms
64 bytes from 10.3.1.12: icmp_seq=12 ttl=64 time=0.240 ms
64 bytes from 10.3.1.12: icmp_seq=13 ttl=64 time=0.285 ms
64 bytes from 10.3.1.12: icmp_seq=14 ttl=64 time=0.283 ms
64 bytes from 10.3.1.12: icmp_seq=15 ttl=64 time=0.256 ms
64 bytes from 10.3.1.12: icmp_seq=16 ttl=64 time=0.266 ms
64 bytes from 10.3.1.12: icmp_seq=17 ttl=64 time=0.234 ms
64 bytes from 10.3.1.12: icmp_seq=18 ttl=64 time=0.280 ms
64 bytes from 10.3.1.12: icmp_seq=19 ttl=64 time=0.378 ms
64 bytes from 10.3.1.12: icmp_seq=20 ttl=64 time=0.288 ms
64 bytes from 10.3.1.12: icmp_seq=21 ttl=64 time=0.279 ms
64 bytes from 10.3.1.12: icmp_seq=22 ttl=64 time=0.452 ms
64 bytes from 10.3.1.12: icmp_seq=23 ttl=64 time=0.273 ms
64 bytes from 10.3.1.12: icmp_seq=24 ttl=64 time=0.342 ms
64 bytes from 10.3.1.12: icmp_seq=25 ttl=64 time=0.283 ms
64 bytes from 10.3.1.12: icmp_seq=26 ttl=64 time=0.237 ms
64 bytes from 10.3.1.12: icmp_seq=27 ttl=64 time=0.252 ms
64 bytes from 10.3.1.12: icmp_seq=28 ttl=64 time=0.291 ms
64 bytes from 10.3.1.12: icmp_seq=29 ttl=64 time=0.294 ms
64 bytes from 10.3.1.12: icmp_seq=30 ttl=64 time=0.270 ms
64 bytes from 10.3.1.12: icmp_seq=31 ttl=64 time=0.308 ms
64 bytes from 10.3.1.12: icmp_seq=32 ttl=64 time=0.278 ms
64 bytes from 10.3.1.12: icmp_seq=33 ttl=64 time=0.256 ms
64 bytes from 10.3.1.12: icmp_seq=34 ttl=64 time=0.270 ms
64 bytes from 10.3.1.12: icmp_seq=35 ttl=64 time=0.248 ms
64 bytes from 10.3.1.12: icmp_seq=36 ttl=64 time=0.291 ms
64 bytes from 10.3.1.12: icmp_seq=37 ttl=64 time=0.263 ms
64 bytes from 10.3.1.12: icmp_seq=38 ttl=64 time=0.230 ms
64 bytes from 10.3.1.12: icmp_seq=39 ttl=64 time=0.346 ms
64 bytes from 10.3.1.12: icmp_seq=40 ttl=64 time=0.318 ms
64 bytes from 10.3.1.12: icmp_seq=41 ttl=64 time=0.236 ms
64 bytes from 10.3.1.12: icmp_seq=42 ttl=64 time=0.235 ms
64 bytes from 10.3.1.12: icmp_seq=43 ttl=64 time=0.285 ms
64 bytes from 10.3.1.12: icmp_seq=44 ttl=64 time=0.286 ms
64 bytes from 10.3.1.12: icmp_seq=45 ttl=64 time=0.278 ms
64 bytes from 10.3.1.12: icmp_seq=46 ttl=64 time=0.367 ms
64 bytes from 10.3.1.12: icmp_seq=47 ttl=64 time=0.282 ms
64 bytes from 10.3.1.12: icmp_seq=48 ttl=64 time=0.230 ms
64 bytes from 10.3.1.12: icmp_seq=49 ttl=64 time=0.314 ms
64 bytes from 10.3.1.12: icmp_seq=50 ttl=64 time=0.300 ms
64 bytes from 10.3.1.12: icmp_seq=51 ttl=64 time=0.303 ms
64 bytes from 10.3.1.12: icmp_seq=52 ttl=64 time=0.320 ms
64 bytes from 10.3.1.12: icmp_seq=53 ttl=64 time=0.257 ms
64 bytes from 10.3.1.12: icmp_seq=54 ttl=64 time=0.282 ms
64 bytes from 10.3.1.12: icmp_seq=55 ttl=64 time=0.254 ms
64 bytes from 10.3.1.12: icmp_seq=56 ttl=64 time=0.258 ms
64 bytes from 10.3.1.12: icmp_seq=57 ttl=64 time=0.276 ms
64 bytes from 10.3.1.12: icmp_seq=58 ttl=64 time=0.303 ms
64 bytes from 10.3.1.12: icmp_seq=59 ttl=64 time=0.284 ms
64 bytes from 10.3.1.12: icmp_seq=60 ttl=64 time=0.265 ms
64 bytes from 10.3.1.12: icmp_seq=61 ttl=64 time=0.268 ms
64 bytes from 10.3.1.12: icmp_seq=62 ttl=64 time=0.315 ms
^C
--- 10.3.1.12 ping statistics ---
62 packets transmitted, 62 received, 0% packet loss, time 62500ms
rtt min/avg/max/mdev = 0.208/0.281/0.452/0.038 ms
```
- ip neigh show (vm 1)
```
10.3.1.1 dev enp0s8 lladdr 0a:00:27:00:00:4f DELAY
10.3.1.12 dev enp0s8 lladdr 08:00:27:06:5f:d2 STALE
```
(vm2)
```
10.3.1.1 dev enp0s8 lladdr 0a:00:27:00:00:4f REACHABLE
10.3.1.11 dev enp0s8 lladdr 08:00:27:cb:79:63 STALE
```
- Adresse de marcel ` 10.3.1.12 dev enp0s8 lladdr 08:00:27:06:5f:d2 STALE

-  Adresse de john `10.3.1.11 dev enp0s8 lladdr 08:00:27:cb:79:63 STALE`
- prouvez que l'info est correcte (que l'adresse MAC que vous voyez dans la table est bien celle de la machine correspondante)
  - ip neigh show 
```
 
10.3.1.1 dev enp0s8 lladdr 0a:00:27:00:00:4f DELAY
10.3.1.12 dev enp0s8 lladdr 08:00:27:06:5f:d2 STALE
```
  -    (ip a) 
 
```
link/ether 08:00:27:06:5f:d2 brd ff:ff:ff:ff:ff:ff
    inet 10.3.2.11/24 brd 10.3.2.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet 10.3.1.12/24 brd 10.3.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe06:5fd2/64 scope link
       valid_lft forever preferred_lft forever
```
