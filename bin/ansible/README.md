# 🐙 Ansible Manager - Gestionnaire du Contrôleur

Ce script fournit un menu interactif pour gérer les opérations et les fichiers d'un environnement Ansible. Il est conçu pour être la console principale pour les utilisateurs qui gèrent l'infrastructure depuis ce contrôleur.

## Configuration Principale

Le script utilise la variable d'environnement `ANSIBLE_ROOT` pour définir le répertoire de travail principal d'Ansible. Si cette variable n'est pas définie, elle utilise un chemin par défaut (généralement `$HOME/ansible`).

|**Variable**  | **Description** | **Chemin par Défaut (si non défini)**|
|--|--|-|
|`ANSIBLE_ROOT`|Répertoire racine de votre projet Ansible|`$HOME/ansible`
|`SCRIPTS_DIR`|Emplacement des scripts utilitaires |`$ANSIBLE_ROOT/scripts`|

Si vous déplacez votre installation Ansible, vous devez vous assurer que la variable `ANSIBLE_ROOT` est correctement défini.

## Exigences Sudoers (pour la Gestion Cron)

Le Manager Ansible a besoin de privilèges Sudo pour certaines opérations système, notamment pour la gestion des tâches Cron (`Option 2`).

Si vous souhaitez exécuter cette fonction **sans saisir de mot de passe** à chaque fois (mode NOPASSWD), vous devez ajouter une règle Sudoers.

## Fonctionnalités Clés

* **Launcher de Playbooks (Option 1) :** Exécute les playbooks définis.

* **Gestion des Tâches Cron (Option 2) :** Outil d'administration pour les tâches planifiées (nécessite Sudo).

* **Gestion des Secrets (Option 3) :** Gère les fichiers Vault.

* **Shell Restreint (Option 6) :** Ouvre un shell limité au répertoire `$ANSIBLE_ROOT` pour la manipulation de fichiers (Nano, Git, etc.).

* **Déverrouillage Admin (`[admin]`) :** Ouvre un shell Bash complet en demandant l'authentification de l'utilisateur.
"""
