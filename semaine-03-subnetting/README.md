# Lab Semaine 3–4 · Subnetting & VLSM

## Objectif
Maîtriser le découpage d'un réseau en sous-réseaux (subnetting)
et appliquer la méthode VLSM pour concevoir un plan d'adressage
d'entreprise — compétence clé pour l'examen CCNA.

---

## Concepts maîtrisés

### 1. Structure d'une adresse IP
Une adresse IP /préfixe se décompose en deux parties :
- **Partie réseau** : définie par le préfixe (ex: /24 = 24 bits réseau)
- **Partie hôte** : bits restants (ex: /24 = 8 bits hôtes)

Les 2 adresses réservées par sous-réseau :
- **Adresse réseau** : premier bloc (ex: 192.168.1.0)
- **Adresse broadcast** : dernier bloc (ex: 192.168.1.255)

### 2. Formules essentielles

| Préfixe | Taille bloc | Hôtes utilisables | Formule       |
|---------|-------------|-------------------|---------------|
| /24     | 256         | 254               | 2⁸ - 2        |
| /25     | 128         | 126               | 2⁷ - 2        |
| /26     | 64          | 62                | 2⁶ - 2        |
| /27     | 32          | 30                | 2⁵ - 2        |
| /28     | 16          | 14                | 2⁴ - 2        |
| /29     | 8           | 6                 | 2³ - 2        |
| /30     | 4           | 2                 | 2² - 2        |

**Formule universelle :** `2^(32 - préfixe) - 2`

### 3. Méthode de calcul (3 étapes)
1. Calculer la **taille du bloc** → `2^(32 - préfixe)`
2. Les sous-réseaux commencent aux **multiples du bloc** (0, 32, 64, 96...)
3. **Broadcast** = début du prochain sous-réseau - 1

---

## Exercices résolus

### Exercice 1 · /25
Réseau : `192.168.1.0/25` — taille bloc : 128

| | Adresse |
|---|---|
| Réseau | 192.168.1.0 |
| Hôtes utilisables | 192.168.1.1 → 192.168.1.126 |
| Broadcast | 192.168.1.127 |
| Hôtes | 126 |

### Exercice 2 · /26
Réseau : `192.168.1.0/24` découpé en /26 — 4 sous-réseaux de 62 hôtes

| Sous-réseau | Réseau        | Hôtes utilisables           | Broadcast      |
|-------------|---------------|-----------------------------|----------------|
| 1           | 192.168.1.0   | 192.168.1.1 → .62           | 192.168.1.63   |
| 2           | 192.168.1.64  | 192.168.1.65 → .126         | 192.168.1.127  |
| 3           | 192.168.1.128 | 192.168.1.129 → .190        | 192.168.1.191  |
| 4           | 192.168.1.192 | 192.168.1.193 → .254        | 192.168.1.255  |

### Exercice 3 · /27
Réseau : `172.16.0.0/27` — taille bloc : 32

| | Adresse |
|---|---|
| Réseau | 172.16.0.0 |
| Hôtes utilisables | 172.16.0.1 → 172.16.0.30 |
| Broadcast | 172.16.0.31 |
| Sous-réseau 2 | 172.16.0.32 |

### Exercice 4 · Cas réel entreprise (type CCNA)
**Besoin :** 5 sous-réseaux avec minimum 25 hôtes chacun
**Réseau disponible :** `192.168.10.0/24`
**Préfixe choisi :** `/27` → 30 hôtes utilisables ✅

| Sous-réseau | Réseau           | Hôtes utilisables                  | Broadcast        |
|-------------|------------------|------------------------------------|------------------|
| 1           | 192.168.10.0     | 192.168.10.1 → 192.168.10.30      | 192.168.10.31    |
| 2           | 192.168.10.32    | 192.168.10.33 → 192.168.10.62     | 192.168.10.63    |
| 3           | 192.168.10.64    | 192.168.10.65 → 192.168.10.94     | 192.168.10.95    |
| 4           | 192.168.10.96    | 192.168.10.97 → 192.168.10.126    | 192.168.10.127   |
| 5           | 192.168.10.128   | 192.168.10.129 → 192.168.10.158   | 192.168.10.159   |

---

## Résultats obtenus

- [x] Formule 2^(32-préfixe) - 2 maîtrisée
- [x] Calcul de blocs et plages de sous-réseaux
- [x] Résolution d'un cas réel type CCNA
- [x] Méthode des 3 étapes appliquée

---

## Prochaine étape
Semaine 5–6 : Packet Tracer — configurer une topologie réseau
avec les sous-réseaux calculés dans ce lab.
