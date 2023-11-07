README
======

Ce fichier README explique le fonctionnement du script 'pre-commit' utilisé dans les hooks Git pour automatiser la création d'un fichier de suivi pour chaque commit, à condition que l'utilisateur le demande.

Description du Hook 'pre-commit'
--------------------------------

Le script 'pre-commit' est un hook Git qui se déclenche avant que chaque 'commit' ne soit finalisé. Son rôle est de poser une question à l'utilisateur pour savoir si un fichier de suivi de commit doit être généré. Si l'utilisateur répond 'y' (oui), un fichier nommé 'commitInfo.txt' est créé dans le dossier 'suivi/', contenant la date et l'heure actuelles avec le texte « commit vérifié le ».

Emplacement du Hook
-------------------

Le script doit être placé dans le répertoire suivant de votre dépôt Git :

    .git/hooks/pre-commit

Assurez-vous de le rendre exécutable en utilisant la commande suivante dans le terminal :

    chmod +x .git/hooks/pre-commit

Comment fonctionne le script
-----------------------------

1. Lorsqu'un commit est déclenché, le script demande à l'utilisateur : "Stockage d'un fichier complémentaire pour ce commit (y/[n]) ? ".
2. L'utilisateur peut répondre avec 'y' pour oui ou 'n' pour non. S'il appuie simplement sur Entrée, la réponse par défaut est 'n'.
3. Si la réponse est 'y', le script crée un fichier 'commitInfo.txt' contenant la phrase avec la date et l'heure formatées comme suit : 'dd/mm/yyyy HH:MM:SS'.
4. Ce fichier est ensuite ajouté au staging area de Git avec `git add`, de sorte qu'il soit inclus dans le commit en cours.
5. Si la réponse est 'n' ou Entrée, le script n'effectue aucune action et permet au commit de se poursuivre sans ajouter de fichier de suivi.
6. En cas de réponse autre que 'y' ou 'n', le script affiche un message d'erreur et arrête le processus de commit avec un code d'erreur pour que l'utilisateur puisse répondre correctement.

Note Importante
---------------

Si le dossier 'suivi/' n'existe pas déjà, le script le créera. Aucune configuration supplémentaire n'est nécessaire de la part de l'utilisateur.

Conclusion
----------

Ce hook est un moyen simple de garder une trace des vérifications de commit avec un fichier de suivi qui contient l'horodatage de chaque commit. Il automatise une partie du processus de suivi sans intervention supplémentaire, à moins que l'utilisateur ne souhaite exclure le fichier de suivi du commit.
