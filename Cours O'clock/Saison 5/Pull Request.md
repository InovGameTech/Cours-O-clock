# Pull Request

Avec Git, lorsqu'une fonctionnalité est terminée, on peut vouloir que ses collègues viennent vérifier le code produit.  
Pour cela, il existe les _Pull Requests_ :tada:

## Procédure

- avant de coder sa fonctionnalité
    - créer une branche du nom de la fonctionnalité
    - se placer sur cette branche
    - coder dans cette branche
- après avoir codé la fonctionnalité
    - on ne merge pas dans la branche principale (`dev` ou `master`)
    - on push la branche sur _GitHub_ => `origin/mabranche`
- aller sur la page du dépôt sur le site _GitHub_
    - _GitHub_ a détecté qu'une nouvelle branche vient d'être envoyée (la branche s'appelle `ben` dans les screenshots)
    - on va donc utiliser le bouton pour créer notre _Pull Request_ (PR, pour les intimes :wink:)
![créer la PR](img/git-pull-request.PNG)
    - _GitHub_ effectue une comparaison entre la branche `master` et la branche envoyée
    - on peut changer la branche de comparaison si nécessaire
    - on écrit le titre de la PR et la description de ce qu'elle contient
    - on peut aussi mettre dans le message des informations à destination des reviewers
![PR en cours de création](img/git-pull-request-2.PNG)
    - à droite, on peut sélectionner les reviewers parmi les membres de la team
![PR sélection de reviewers](img/git-pull-request-3.PNG)
    - un _reviewer_ est une personne chargée de revoir votre code :
        - lire le code
        - chercher les bugs
        - vérifier la qualité du code (indentation, commentaires, etc.)
        - ajouter des messages dans le code review _GitHub_
    - dans ta promo, seuls les personnes ayant un accès en lecture à ton repo peut être reviewer
        - donc tu peux ajouter des personnes (ou la promo) en _Collaborator_
        - puis, ces personnes (ou la promo) sont dispo dans la liste des _reviewers_ possibles
![PR sélection de reviewers](img/git-pull-request-4.PNG)
    - pour faire le code review, le _reviewer_ a plusieurs onglets à disposition
        - la liste des commits
![PR sélection de reviewers](img/git-pull-request-5.PNG)
        - les fichiers modifiés et leurs lignes modifiées
![PR sélection de reviewers](img/git-pull-request-6.PNG)
- après quelques heures, (quelques jours pour jc :unamused:)
    - le ou les reviewer(s) ont validé le code
![PR sélection de reviewers](img/git-pull-request-7.PNG)
    - on peut lancer le merge dans la branche principale, ici `master`
![PR sélection de reviewers](img/git-pull-request-8.PNG)

## :champagne: :tada: