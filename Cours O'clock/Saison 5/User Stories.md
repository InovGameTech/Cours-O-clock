### Spécifications
Les spécifications contiennent toutes les informations nécessaires au développement.
C'est l'équipe de développement qui les rédige pendant la conception de l'application.

Spécifications fonctionnelles:
- description détaillée des scenarios d'utilisation: *user stories*.   
  "En tant que ... je veux ... pour ..."  
  *ex: En tant qu'employé de la librairie, je veux pouvoir consulter le stock de livres par référence, par auteur ou par titre, pour pouvoir renseigner les usagers qui viennent me demander un livre en particulier*  
  [exemple de fichier pour les user-stories](https://drive.google.com/open?id=1ShU5jhJhAvvccvfvbWg6Tb3YoBNNK7ZXS4RxGBhtDiI)

- fonctionnalités et autorisations : *use-cases*,  
  [exemple de fichier de spécification des autorisations](https://docs.google.com/a/oclock.io/spreadsheets/d/1QwfR0KfbBRm9xuFM7FFQUSNaPyzU00hsi-4cux8wCkI/edit?usp=sharing)   

  *exemple de use-cases sur la boutique:*
  ![use case front boutique](img/use_cases-boutique-pantoufland.png)
  ![use case account boutique](img/use_cases-account-pantoufland.png)

- la description de l'interface : *wireframes*,  
  *Outil: Balsamiq, Sketch*  

- les règles de gestion (*ex: un abonné ne peut emprunter plus de 2 DVD en même temps*)

Spécifications techniques:
- la description précises des données manipulées : *dictionnaire de données, MCD, MLD*
  [méthodologie/exemple pour concevoir une base de données relationnelle](conception-bd.md)

- architecture logicielle choisie : *outils/librairies, organisation des fichiers, ...*


### Méthodes/outils de modélisation
Modélisation: représentation graphique d'une situation ou d'un processus.

Référentiels de modélisation en programmation:  
Ces outils sont extrêment répandus et des références dans le domaine du développement logiciel en général.  
Ici ne sont listés que les schémas que nous utilisons en cours.

- MERISE : représentations séparée des données et des traitements, par niveaux
  - Modèle Conceptuel des Données: schéma Entité-Association, bien adapté à la modélisation de bases de données relationnelles

- UML : langage de modélisation, propose plusieurs types de visualisation, statiques ou dynamiques pour toutes les étapes de la conception à la réalisation d'un projet informatique.
  - diagramme de cas d'utilisation: à l'étape d'analyse des besoins, permet d'identifier les fonctionnalités et les acteurs du système
