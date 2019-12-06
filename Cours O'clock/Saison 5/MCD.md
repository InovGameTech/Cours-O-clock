# MCD / Modèle Entité-Association

Cette modélisation des données permet de représenter de façon rigoureuse un système de données, ou système d'informations, sous forme d'entités et des relations qui les lient.

A partir des données présentes dans le dictionnaire nous pouvons :
- **Dessiner nos _entités_**.
- **Répartir leurs _attributs_** (les données qui les concernent).
- Définir un attribut qui identifie l'entité de manière unique : **L'identifiant ou la _clé primaire_**.
- **Identifier les _relations_** entre les entités et _les nommer_ par un verbe à l'infinitif.
- Définir les **_cardinalités_** : nous allons expliquer ce concept via un exemple.


## Exemple de MCD et définitions

Le MCD de l'exemple des livres nous donne :

![](./img/MCD-livres.png)

- L'**entité** est représentée par un **rectangle**. Elle est nommée **au singulier ou au pluriel** (ne mélangez pas les deux).
- Les **attributs sont listés** sous le nom de l'entité.
    - **La clé primaire** qui identifiera l'entité, est **soulignée** (premier champ).
- **Les associations** sont représentées par un **rectangle arrondi** et **nommées par un verbe**, ici *ECRIRE* entre *Auteur* et *Livre* puis *APPARTENIR* entre *Livre* et *Genre*.
    - Le verbe peut être :
        - à l'infinitif : ECRIRE,
        - à la forme passive : EST ECRIT,
        - accompagné d'un adverbe : AVOIR LIEU DANS.

### Cardinalités

- **Les cardinalités** sont :
    - Les **quantités minimum et maximum** qui peuvent exister **entre deux entités A et B**,
    - **de A vers B et de B vers A**,
    - cela implique donc **4 cardinalités par relation**, pour les trouver posons-nous ces questions :
        - L'entité A est "liée" à combien d'entités B au minimum ? => 0 ou 1
        - L'entité A est "liée" à combien d'entités B au maximum ? => 1 ou n
        - L'entité B est "liée" à combien d'entités A au minimum ? => 0 ou 1
        - L'entité B est "liée" à combien d'entités A au maximum ? => 1 ou n

Partant de là, **les valeurs possibles pour les cardinalités sont** : (0,1) (1,1) (0,n) (1,n).

### Raccourcis de langage

Les cardinalités maximum sont celles qui auront le plus d'impact sur notre implémentation physique, on les privilégiera souvent pour nommer la relation, on parlera alors :

- De relation **"un à plusieurs"** en cas de cardinalités max. 1 et n.
- De relation **"plusieurs à plusieurs"** en cas de cardinalités max. n et n.

#### Cas de notre MCD

> Relation Auteur-Livre :

- Combien de livres peut écrire un auteur au minimum ? 
    - => 0 (si l'auteur n'a pas terminé un seul livre).
- Combien de livres peut écrire un auteur au maximum ?
    - => n (plusieurs).
- Par combien d'auteurs un livre peut-il être écrit au minimum ?
    - => 1 (il faut au moins un auteur pour écrire un livre).
- Par combien d'auteurs un livre peut-il être écrit au maximum ?
    - => 1 (si on part du principe qu'il n'y a pas de co-auteurs).

> Relation Livre-Genre :

- A combien de livres correspond chaque genre au minimum ? 
    - => 0 (un genre peut n'avoir aucun livre associé).
- A combien de livres correspond chaque genre au maximum ?
    - => n (plusieurs).
- A combien de genres un livre peut-il être associé au minimum ?
    - => 0 (si un genre peut être "non spécifié" sur un livre, sinon 1).
- A combien de genres un livre peut-il être associé au maximum ?
    - => n (plusieurs).

On notera que pour la cardinalité *minimum*, le choix du 0 ou du 1 dépend énormément du fonctionnement attendu de notre application. En cas de doute, vous devez vous référez à vos spécifications ou être amené à les préciser le cas échéant. Rappelez-vous d'un des intérêts de la modélisation cité plus haut : *"se poser les bonnes questions"*.

## Autres cas d'association

### Association avec attributs

Parfois une information du dictionnaire de données se trouve _décrire, faire partie de la relation_. Par exemple le rôle d'une personne dans un film serait un attribut de la relation _Personne-Film_. Restons sur notre exemple et ajoutons la possibilité pour un livre d'être emprunté par une personne.

Nom|Description|Type|Commentaire|Entité|
-|-|-|-|-|
Nom|Nom de la personne|texte court|-|Personne|
Prénom|Prénom de la personne|texte court|-|Personne|
DateEmprunt|Date d'emprunt|date|attribut de la relation|Personne/Livre|

**La date d'emprunt est une propriété de la relation entre Personne et Livre**. On notera au passage le renommage de notre entité _Auteur_ en _Personne_ puisqu'une personne (pas forcément la même) pourra être auteur et/ou emprunteur d'un livre.

Notre schéma devient : 

![](./img/MCD-livres-asso-attributs.png)

### Association plurielles

**Les deux mêmes entités peuvent être plusieurs fois en association**, ce qui est le cas de *Personne* et *Livre* dans le schéma précédent.

### Association binaire, ternaire, n-aire

Quand le nombre d'entités _n_ en jeu dans un relation est de **n=2**, on parle de **relation binaire** (les relations vues jusqu'à présent). Il se trouve qu'une relation peut faire intervenir plus de 2 tables. On parlera de ternaire pour 3 tables mais plus généralement de relation **n-aire** dès qu'il y a plus de 2 tables en jeu.

Imaginons dans notre exemple, **la possibilité d'emprunter un livre depuis différents lieux** d'un même réseau : médiathèque, bibliothèque, bibliobus avec chacun ses propriétés (nom, adresse, type). Notre schéma deviendrait : 

![](./img/MCD-livres-asso-n-aire.png)

**Les cardinalités maximum** (ici n) nous indiquent que : plusieurs livres peuvent être empruntés par plusieurs personnes dans différents lieux à une date donnée.

**Les cardinalités minimum** (ici 0) nous indiquent qu'un livre peut ne pas être emprunté du tout, qu'une personne peut n'emprunter aucun livre et qu'un lieu peut ne jamais avoir à prêter un livre : encore une fois *les cardinalités minimum servent à préciser une réalité ou un fonctionnement attendu, défini par les contraintes du projet*.

### Association réflexive (réflexivité)

On parle d'**association réflexive lorsqu'une entité fait référence à elle-même** (des occurences d'une même entité se font référence entre elles). Par exemple *des Personnes dont le parent ou l'enfant seraient associés*, ou *des Catégories organisées entre elles selon une hiérarchie*. Exemple :

![](./img/MCD-reflexivite.png) => ![](./img/MCD-reflexivite-exemple.png)

- Une catégorie peut appartenir à 0 ou plusieurs catégories parentes.
- Une catégorie peut avoir de 0 à plusieurs catégories enfants.

---

> [Retour au sommaire](./README.md)