# home-lab-asr
# Lab Semaine 1–2 · Linux & VM Setup

## Objectif
Installer Ubuntu Server sur VMware Workstation et maîtriser
les commandes Linux essentielles d'un administrateur réseau/système.

---

## Environnement technique

| Composant     | Détail                        |
|---------------|-------------------------------|
| OS hôte       | Windows 11                    |
| Hyperviseur   | VMware Workstation            |
| VM            | Ubuntu Server 22.04 LTS       |
| Kernel        | Linux 6.8.0-101-generic x86_64|
| RAM allouée   | 2.8 Go                        |
| Disque        | 9.8 Go                        |
| IP VM         | 172.29.78.195 (ens33)         |

---

## Ce que j'ai appris

### 1. Connexion SSH
Connexion à distance depuis Windows PowerShell vers la VM Ubuntu :
```bash
ssh samuel@172.29.78.195
```
Résultat : accès au terminal Linux depuis Windows, comme un admin en production.

### 2. Commandes système essentielles

| Commande     | Rôle                              | Résultat observé               |
|--------------|-----------------------------------|--------------------------------|
| `ip a`       | Voir les interfaces réseau        | ens33 → 172.29.78.195         |
| `ping 8.8.8.8` | Tester la connectivité internet | 4 paquets reçus, 0% perte     |
| `df -h`      | Espace disque disponible          | 4.8 Go libres sur 9.8 Go      |
| `free -h`    | RAM disponible                    | 2.4 Go libres sur 2.8 Go      |
| `top`        | Processus en cours                | 216 tâches, CPU idle à 99.5%  |
| `ss -tuln`   | Ports ouverts                     | Seul le port 22 (SSH) ouvert  |
| `who`        | Sessions actives                  | 2 sessions : tty1 + pts/0     |
| `last`       | Historique des connexions         | Historique depuis mars 2026   |
| `uname -a`   | Infos système                     | Linux 6.8.0, x86_64           |

### 3. Permissions Linux (chmod)
Comprendre et modifier les droits sur les fichiers :

```bash
touch rapport.txt        # créer un fichier
ls -l rapport.txt        # -rw-rw-r-- (644 par défaut)
chmod 755 rapport.txt    # -rwxr-xr-x
chmod 600 rapport.txt    # -rw------- (privé)
chmod 777 rapport.txt    # -rwxrwxrwx (tous les droits)
```

**Tableau de référence chmod :**

| Valeur | Permissions | Signification            |
|--------|-------------|--------------------------|
| 7      | rwx         | Lecture + Écriture + Exécution |
| 6      | rw-         | Lecture + Écriture       |
| 5      | r-x         | Lecture + Exécution      |
| 4      | r--         | Lecture seule            |
| 0      | ---         | Aucun droit              |

---

## Résultats obtenus

- [x] VM Ubuntu Server opérationnelle sur VMware Workstation
- [x] Connexion SSH fonctionnelle depuis Windows
- [x] Commandes système de base maîtrisées
- [x] Permissions Linux comprises et appliquées
- [x] Port 22 seul ouvert → bonne posture sécurité

---

## Prochaine étape
Semaine 3–4 : Subnetting & VLSM — préparation CCNA
