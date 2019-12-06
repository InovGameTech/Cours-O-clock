# Architecture MVC : Model - View - Controller

* *Pattern* (modèle) de programmation objet, mais qui peut être implémenté en procédural (avec require...).

> * Séparation de l'application en *couches* (classes, ensemble de classes, composants), chaque couche logicielle assure un rôle distinct.

![mvc simple](img/mvc-simple.png)

* Avantages : meilleur code  
  * lisibilité du code   
  * prévention des erreurs   
  * DRY:   
    même contenu (model) présenté dans des vues différentes  
    utilisation de la même vue avec un contenu variable  
    ...

## Model
> Gère l'accès aux entités manipulées par l'application:  
> * protège l'intégrité des données en implémentant la logique métier  
> * s'occupe du stockage  

La définition des entités elles-mêmes (produit, utilisateur, employé) peut être séparée de l'accès aux données.  

La couche Model est l'ensemble des classes qui définissent les objets manipulés par l'application, qui contiennent les _données_ et réalisent les opérations de stockage.  

Plusieurs stratégies existent pour implémenter cette couche de l'application.


Pour aller plus loin sur le sujet :

<details>

#### ORM
La couche d'accès aux données peut être implémentée à l'aide d'un **ORM (Object Relational Mapping)** qui inclut des fonctions plus ou moins avancées:  
* validation des données
* connexion aux bases de données
* génération automatique de tables à partir des modèles   

*La plupart des frameworks utilisent un ORM, ou permettent d'en utiliser un:*
* *Symfony, Zend > Doctrine,*
* *Laravel > Eloquent*
* *CakePHP, CodeIgniter, Yii > built-in*

#### Active Record vs Data Mapper

##### Active Record
  *ex: Eloquent*  
  > Une classe <=> une table en base de données, une instance <=> une ligne.  

  La classe implémente les méthodes de validation des champs, sauvegarde et récupération des données.  
  - Plus simple à mettre en oeuvre,  
  - utile pour les opérations "CRUD",  
  - plus de *couplage* entre l'application et la base de données  

##### Data Mapper
  *ex: Doctrine*
  > 2 composants: l'Entité, objet manipulé par l'application, et le Manager, qui gère le mapping entre les entités et les données, et leur persistance.

  La structure de la BD peut être très différente de la structure des entités.
  - Plus flexible pour mettre en place des applications complexes,
  - demande plus de contrôle dans les interactions avec la BD,
  - moins de *couplage* application - base de données

</details>


## View

> Gère la présentation des données:  
> Les données sont "récupérées" par le Controller (via le Model) et "passées" à la View, qui est chargée de les présenter.

#### Systèmes de templates
* Plates : PHP natif   
  http://platesphp.com/  

* Smarty : langage dédié, templates compilés   
  https://github.com/smarty-php/smarty/  

* Twig (Symfony) : syntaxe dédiée, templates compilés   
  http://twig.sensiolabs.org/  


## Controller

> Gère l'aspect dynamique de l'application :  
> A partir de l'action demandée (requête utilisateur), il récupère les données (avec le Model) les injecte dans la vue adéquate, et envoie la réponse produite.  
> (selon l'implémentation, parfois c'est la vue qui renvoie elle-même la réponse)

#### Le Front Controller
> Objectif: centraliser les requêtes à l'application en un "Single Point of Entry", qui va analyser la requête et appeler l'action correspondante, du Controller correspondant.  

Le FrontController implémente 2 étapes de traitement:  
* le routage de la requête (recevoir la requête, identifier l'action à éxécuter et les paramètres)
* le dispatch (instancier le Controller et éxécuter l'action)


![mvc complet](img/MVC.png)


## Implémentation

### FrontController

##### Routage
Système minimaliste de routage:  
* le fichier `.htaccess`  
  ```
  RewriteEngine On
  RewriteBase /
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule ^(.*)$ index.php?params=$1 [L,QSA]
  ```

* le fichier `index.php`  
  ```php
  if(empty($_GET))
  {
      $params[0] = "default";
  }
  else
  {
      $params = explode('/', $_GET["params"]);
  }
  ```


## Stratégie / Structure de projet
Les stratégies d'implémentation du modèle MVC varient: il n'y a pas *une seule et unique* façon de structurer son application, ses classes, son système de fichiers.  

Quelques questions à se poser lors de la planification du développement:  
* Quelles actions pour mes utilisateurs?  
* Quelles routes correspondantes? Est ce que j'ai besoin d'un système de routage?  
* Quels controllers pour implémenter ces actions?
  * un controller par model? convient pour les applications CRUD (gestion...)
  * un controller par vue? convient pour les applications/vues complexes
  * un controller par domaine fonctionnel?
* Quelle stratégie pour mes modèles? Est ce que j'ai besoin d'un ORM?
* Quel système de templates?