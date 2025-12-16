# 🌐 Nginx/UFW Manager - Gestionnaire de Serveur Web

Ce script fournit un menu interactif pour la gestion complète des composants web essentiels : le serveur Nginx, le pare-feu UFW, et les opérations de déploiement et de sauvegarde.

## Configuration Principale

Le script utilise les chemins de configuration Debian/Ubuntu standards. Si votre installation utilise des chemins non conventionnels, ces variables devront être mises à jour directement dans le script :

| **Variable** | **Chemin Standard** | **Description** |
| :--- | :--- | :--- |
| `DIR_WEB` | `/var/www` | Racine des données web. |
| `DIR_NGINX` | `/etc/nginx` | Dossier principal de configuration Nginx. |
| `BACKUP_DIR` | `/var/backups/nginx-manager` | Dossier de destination des sauvegardes. |

## Prérequis et Dépendances

Ce manager nécessite les outils suivants pour fonctionner correctement :

| Dépendance | Description | Note |
| :--- | :--- | :--- |
| `nginx` | Le serveur web. | Obligatoire |
| `ufw` | Le pare-feu. | Obligatoire |
| `git` | Utilisé pour l'option de déploiement GitHub. | Requis pour le déploiement. |
| `composer` | Détecté et utilisé pour l'installation des dépendances PHP. | Requis pour les projets PHP. |
| `tar` | Utilisé pour la création des archives de sauvegarde. | Obligatoire |

## Exigences Sudoers (Requis)

Le Dashboard du manager vérifie l'état du service Nginx et du pare-feu UFW à chaque rafraîchissement. Pour garantir que le menu s'affiche instantanément sans bloquer l'utilisateur, les commandes d'état doivent être autorisées sans mot de passe.

### Règle NOPASSWD pour UFW

Ajoutez ces règles (en remplaçant `votre_utilisateur` ou `%votre_groupe`) à votre fichier Sudoers :

```sudoers
# Autoriser les commandes UFW d'information
votre_utilisateur ALL=(ALL) NOPASSWD: /usr/sbin/ufw status*, /usr/sbin/ufw status numbered
```

## Fonctionnalités Clés

* **Gestion VHosts (Sites Web) :** Création, activation, désactivation, édition et suppression de fichiers de configuration Nginx (`sites-available` / `sites-enabled`).
* **Déploiement GitHub :** Clonage rapide d'un dépôt dans `DIR_WEB` avec gestion des permissions et détection de Composer.
* **Pare-feu UFW :** Gestion interactive des règles, ouverture des ports standards (80, 443, 22), et activation/désactivation complète du pare-feu.
* **Sauvegardes :** Sauvegarde complète du serveur, des configurations Nginx ou des données web sélectionnées.
* **Shell Restreint :** Accès limité aux dossiers `/var/www`, `/etc/nginx` et `/etc/php` pour l'inspection manuelle.
