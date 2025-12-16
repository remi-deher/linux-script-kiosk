# 💾 MariaDB Manager - Configuration Spécifique

Ce script permet l'administration complète du service MariaDB (Start/Stop, CRUD des bases, Sauvegardes) sur une base Debian.

## Prérequis Sudoers (Crucial)

Pour que le Dashboard puisse s'afficher instantanément sans demander de mot de passe à chaque rafraîchissement (mode Kiosk/Manager), vous devez autoriser l'exécution de commandes non destructrices sans mot de passe.

**Le blocage se produit lorsque le script essaie d'exécuter `sudo mysql -u root -e "..."` pour récupérer l'état de la base de données.**

**Le blocage se produit aussi lorsque le script essaie d'exécuter `sudo ufw status"` pour récupérer l'état du pare feu.**

Ajoutez ces règles (en remplaçant `%grp_utilisateur_linux-ssh` par votre groupe ou `votre_utilisateur`) à votre fichier `/etc/sudoers.d/`:

```bash
# 1. Autoriser les commandes UFW d'information
%grp_utilisateur_linux-ssh ALL=(ALL) NOPASSWD: /usr/sbin/ufw status*, /usr/sbin/ufw status numbered

# 2. Autoriser l'exécution du client MySQL avec les arguments de diagnostic
# Ceci est nécessaire pour que la boucle principale récupère Version et Port SANS BLOCAGE.
%grp_utilisateur_linux-ssh ALL=(ALL) NOPASSWD: /usr/bin/mysql -u root -e *
```

## Dépendances

* mariadb-server (ou mysql-server)
* ufw
