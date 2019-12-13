

# CONFIGURATION ANSIBLE

### Modification des fichiers de configuration
Pour que notre configuration Ansible fonctionne correctement avec nos serveurs, il faut modifier quelques fichiers de conf qui se trouve à la racine du projet.

**`ansible.cfg`**
La configuration de ce fichier est simple, il faut simplement modifier 2 lignes:

    become_user = utilisateurSSH
    remote_user= utilisateurSSH
    
Remplacer **utilisateurSSH** par l'utilisateur de nos serveurs à configurer

**`inventory.ini`**
Pour identifier nos serveurs, il faut indiqué nos adresses IP dans ce fichier.
Pour notre serveur WEB, modifier cette ligne:
`SRV-WEB01 ansible_host=AdresseIP`
Pour notre serveur MYSQL, modifier cette ligne:
`SRV-MYSQL01 ansible_host=AdresseIP`

Si l'on souhaite rajouter un serveur WEB ou MYSQL supplémentaire, rajouter les lignes de configuration qui sont nécessaires.
Exemple pour un serveur MYSQL supplémentaire:

    SRV-MYSQL01 ansible_host=AdresseIPduServeur1
    SRV- MYSQL02 ansible_host=AdresseIPduServeur2
    
    [database]
    SRV-MYSQL01
    SRV-MYSQL02

**`vars.yml`**
Par défaut, les valeurs sont:
 - **database** pour notre base de données qui sera celle utilisée par WordPress
 - **user** pour notre utilisateur WordPress sur MYSQL
 - **password** pour le mot de passe de notre utilisateur

On peut simplement modifier ces valeurs par celle que l'on souhaite. 

### Lancement du playbook
Pour maintenant lancer notre configuration, il suffit juste de taper la commande suivante:
`ansible-playbook playbook.yml -i inventory.ini -u UtilisateurSSH -K`

`-i inventory` : définit notre fichier inventory.ini où sont stockés les adresses IP de nos serveurs.
`-u UtilisateurSSH` : définit l'utilisateur SSH qui est utilisé sur par nos serveurs. (**A Modifier**)
`-K` : permet de demander le mot de passe de notre utilisateur **become_user** indiqué dans le fichier **ansible.cfg** au lancement de la commande.
