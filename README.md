# 🐧 Kiosk Scripts Linux - Outils de Gestion de Serveur

Bienvenue dans le dépôt **Kiosk Scripts Linux**. Ce projet fournit un ensemble de managers shell interactifs conçus pour simplifier l'administration de services spécifiques (Nginx, MariaDB, Ansible, Zoraxy) sur des systèmes basés sur Debian/Ubuntu.

Ces scripts sont optimisés pour fonctionner en **mode Kiosk** (lancement automatique du menu au login) tout en gérant les permissions nécessaires via Sudoers (NOPASSWD) pour une expérience fluide et sécurisée.

---

## 🏗️ Structure du Dépôt

Le dépôt est organisé pour séparer les exécutables (les managers) de la documentation et des outils d'installation

### Index des Managers

Chaque manager est un script exécutable (sans extension `.sh`) placé dans son propre dossier pour une documentation et une gestion des dépendances claires.

| Dossier | Outil Géré | Script Exécutable | Notes Spécifiques |
| :--- | :--- | :--- | :--- |
| `ansible/` | Contrôleur Ansible | `ansible-manager` | Gestion de playbooks, inventaire, et shell restreint. |
| `mariadb/` | Base de données MariaDB | `mariadb-manager` | CRUD, Sauvegardes, et diagnostic de statut du service. |
| `nginx/` | Nginx & Pare-feu UFW | `nginx-fw-manager` | Gestion des VHosts, logs et déploiement via Git. |
| `zoraxy/` | Reverse Proxy Zoraxy | `zoraxy-manager` | Configuration de proxy, SSL et gestion d'API. |

---

## 🚀 Guide d'Installation Rapide

### 1. Installation des Managers

Pour que les scripts fonctionnent comme des commandes systèmes, ils doivent être placés dans un répertoire inclus dans votre `$PATH` (par exemple, `/usr/local/bin/`).

1.  Copiez tous les fichiers exécutables (les fichiers nommés `*-manager`) vers `/usr/local/bin/` :

    ```bash
    # Exemple pour les managers
    sudo cp bin/mariadb/mariadb-manager /usr/local/bin/
    # Répétez pour les autres managers...
    ```

2.  Assurez-vous qu'ils sont exécutables :

    ```bash
    sudo chmod +x /usr/local/bin/*-manager
    ```

### 2. Configuration des Permissions Sudoers (Essentiel)

Chaque manager nécessite des permissions Sudo `NOPASSWD` pour les commandes d'état (ex: `ufw status`, `mysql -u root -e "..."`) afin d'éviter les blocages dans la boucle principale.

* **ACTION REQUISE :** Lisez impérativement le `README.md` de chaque sous-dossier (en particulier `mariadb/README.md`) pour connaître les règles `NOPASSWD` exactes à ajouter à votre configuration Sudoers.

### 3. Configuration du Mode Kiosk

Note a venir
