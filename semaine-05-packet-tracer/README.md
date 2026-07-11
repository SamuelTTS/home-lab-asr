# Lab Semaine 5–6 · Packet Tracer — Première topologie routée

## Objectif
Concevoir et configurer un réseau d'entreprise avec deux sous-réseaux
communiquant via un routeur Cisco — en appliquant le subnetting /27
calculé lors du lab précédent.

---

## Topologie

```
PC1 (192.168.10.2) ──┐
                      ├── Switch1 ── Gi0/0 [Routeur] Gi0/1 ── Switch2 ──┬── PC3 (192.168.10.34)
PC2 (192.168.10.3) ──┘                                                   └── PC4 (192.168.10.35)

LAN 1 : 192.168.10.0/27        LAN 2 : 192.168.10.32/27
```

---

## Équipements utilisés

| Équipement | Modèle        | Rôle                        |
|------------|---------------|-----------------------------|
| Routeur    | Cisco 2911    | Interconnexion des 2 LANs   |
| Switch 1   | Cisco 2960    | Commutation LAN 1           |
| Switch 2   | Cisco 2960    | Commutation LAN 2           |
| PC1 & PC2  | Generic PC    | Hôtes LAN 1                 |
| PC3 & PC4  | Generic PC    | Hôtes LAN 2                 |

---

## Plan d'adressage

| Équipement | Interface       | Adresse IP       | Masque            | Passerelle      |
|------------|-----------------|------------------|-------------------|-----------------|
| Routeur    | Gi0/0           | 192.168.10.1     | 255.255.255.224   | —               |
| Routeur    | Gi0/1           | 192.168.10.33    | 255.255.255.224   | —               |
| PC1        | FastEthernet    | 192.168.10.2     | 255.255.255.224   | 192.168.10.1    |
| PC2        | FastEthernet    | 192.168.10.3     | 255.255.255.224   | 192.168.10.1    |
| PC3        | FastEthernet    | 192.168.10.34    | 255.255.255.224   | 192.168.10.33   |
| PC4        | FastEthernet    | 192.168.10.35    | 255.255.255.224   | 192.168.10.33   |

---

## Configuration routeur (CLI Cisco)

```bash
enable
configure terminal

# Interface LAN 1
interface GigabitEthernet0/0
ip address 192.168.10.1 255.255.255.224
no shutdown
exit

# Interface LAN 2
interface GigabitEthernet0/1
ip address 192.168.10.33 255.255.255.224
no shutdown
exit
```

---

## Tests de connectivité

| Source | Destination    | Résultat |
|--------|----------------|----------|
| PC1    | PC2 (même LAN) | ✅ OK    |
| PC1    | PC3 (LAN 2)    | ✅ OK    |
| PC1    | PC4 (LAN 2)    | ✅ OK    |

Ping inter-VLAN fonctionnel → le routeur achemine correctement les paquets entre les deux sous-réseaux.

---

## Ce que j'ai appris

- Les interfaces du routeur Cisco sont **éteintes par défaut** → toujours faire `no shutdown`
- Le masque `/27` = `255.255.255.224` en notation décimale
- La **passerelle par défaut** d'un PC doit pointer vers l'interface du routeur dans son sous-réseau
- Un routeur connecte des sous-réseaux différents — sans lui, LAN1 et LAN2 ne peuvent pas communiquer

---

## Fichier Packet Tracer
`lab-topologie-01.pkt` — topologie complète sauvegardée

---

## Prochaine étape
Semaine 7–8 : Routage dynamique OSPF — configurer plusieurs routeurs
qui apprennent automatiquement les routes entre eux.
