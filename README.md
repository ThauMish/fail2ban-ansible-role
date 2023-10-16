---

# Ansible Role pour Fail2Ban

Ce rôle Ansible est spécifiquement conçu pour automatiser la configuration de Fail2Ban pour des services divers, en mettant l'accent sur les environnements Docker.

## Table des matières

- [Ansible Role pour Fail2Ban](#ansible-role-pour-fail2ban)
  - [Table des matières](#table-des-matières)
  - [Description](#description)
  - [Prérequis](#prérequis)
  - [Installation](#installation)
  - [Configuration](#configuration)
  - [Adaptation à votre stack](#adaptation-à-votre-stack)
  - [Contribution](#contribution)
  - [Licence](#licence)

## Description

Le rôle permet:

- L'ajout automatique de filtres, jails et actions pour chaque service.
- Une configuration flexible via des variables, permettant une adaptation facile à différents services sans avoir à modifier le code du rôle.
- Une action personnalisée pour bannir les adresses IP dans la chaîne `DOCKER-USER` d'iptables.

## Prérequis

- Un serveur Ubuntu avec Fail2Ban préinstallé.
- Ansible version 2.9 ou ultérieure.

## Installation

1. **Cloner le dépôt**:

   ```bash
   git clone https://github.com/thaumishansible-fail2ban-role.git
   cd ansible-fail2ban-role
   ```

## Configuration

1. **Configurer votre playbook**:

   Dans votre playbook, définissez les services que vous souhaitez configurer pour Fail2Ban sous la variable `fail2ban_services`. Par exemple:

   ```yaml
   vars:
     fail2ban_services:
       - name: nextcloud
         enabled: true
         port: "80,443"
         logpath: /chemin/vers/le/log
         # ... autres paramètres
   ```

   Les paramètres disponibles incluent:
   - `name`: Nom du service.
   - `enabled`: Si le service est activé ou non.
   - `port`: Les ports à surveiller.
   - `logpath`: Chemin vers le fichier de log du service.
   - `filter`: Détails du filtre, y compris le nom et la définition.
   - `action`: Détails de l'action, y compris le nom, l'action de bannissement et de débannissement.
   - `maxretry`: Nombre de tentatives avant bannissement.
   - `findtime`: Durée pendant laquelle les tentatives sont comptées.
   - `bantime`: Durée du bannissement.

2. **Exécuter le playbook**:

   ```bash
   ansible-playbook -i votre_inventaire votre_playbook.yml
   ```

## Adaptation à votre stack

Pour ajouter un nouveau service:

1. Ajoutez une nouvelle entrée à la variable `fail2ban_services` dans votre playbook.
2. Définissez les paramètres nécessaires pour ce service, comme indiqué dans la section [Configuration](#configuration).
3. Exécutez votre playbook pour appliquer les changements.

## Contribution

1. Forkez le dépôt.
2. Clonez votre fork localement.
3. Créez une nouvelle branche pour votre fonctionnalité ou correction.
4. Faites vos modifications.
5. Poussez vos modifications vers votre fork sur GitHub.
6. Créez une pull request vers le dépôt original.

## Licence

Ce projet est sous licence MIT. Voir le fichier [LICENCE](LICENCE) pour plus de détails.
