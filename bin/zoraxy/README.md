# 🌐 Zoraxy Manager - Gestionnaire de Reverse Proxy

Ce script fournit une interface complète pour gérer le service Zoraxy, les sites web (VHosts), les certificats SSL via l'API Zoraxy, ainsi que le pare-feu UFW.

## Prérequis et Dépendances

Ce manager dépend de plusieurs outils pour interagir avec l'API, le système de fichiers et le réseau :

| Dépendance | Description | Note |
| :--- | :--- | :--- |
| `jq` | Outil de ligne de commande pour parser le JSON (crucial pour l'API Zoraxy). | **Obligatoire** |
| `curl`, `wget` | Communications réseau pour l'API et les mises à jour. | Obligatoire |
| `ufw` | Gestion du pare-feu. | Obligatoire |
| `openssl` | Lecture des dates d'expiration des certificats SSL locaux. | Obligatoire |

## Configuration des Permissions Sudoers (Requis)

Le manager nécessite des privilèges Sudo pour gérer le service systemd, les chemins de configuration (`/etc/zoraxy`), les fichiers de certificats SSL, et le pare-feu UFW.

### 1. Règle NOPASSWD pour UFW

Pour que la détection du statut UFW ne bloque pas la boucle principale, autorisez l'exécution sans mot de passe :

```sudoers
# Autoriser les commandes UFW d'information (Chemin le plus courant sur Debian/Ubuntu)
votre_utilisateur ALL=(ALL) NOPASSWD: /usr/sbin/ufw status*, /usr/sbin/ufw status numbered
```

### 2. Accès aux Fichiers Zoraxy

Étant donné que le script doit lire et écrire dans `/etc/zoraxy` (pour les configurations de service et les sauvegardes), vous devrez vous assurer que l'utilisateur qui exécute le script a les permissions nécessaires, soit en étant dans le groupe `zoraxy` (si vous avez configuré un tel groupe), soit en autorisant l'accès complet NOPASSWD aux commandes `tar`, `cp`, `rm`, `nano`, etc., pour le répertoire `/etc/zoraxy` via Sudoers.

## Fonctionnalités Clés

* **Gestion du Service (Start/Stop/Restart) :** Contrôle via `systemctl`.
* **Gestion VHosts & SSL :** Utilisation des appels API Zoraxy pour ajouter, modifier ou supprimer des hôtes et générer des certificats ACME (Let's Encrypt).
* **Mise à Jour Applicative :** Vérification de la dernière version disponible sur GitHub et installation.
* **Changement de Port :** Workflow complet pour modifier le port du service Zoraxy (nécessite l'accès au fichier de service `systemd`).
* **Shell Restreint :** Accès limité au répertoire de configuration Zoraxy pour l'inspection manuelle.
