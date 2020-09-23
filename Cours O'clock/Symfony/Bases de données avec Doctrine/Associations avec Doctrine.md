# Symfo S2 J2 : associations avec Doctrine

## Ressources

### Symfony

- [Associations avec Doctrine](http://symfony.com/doc/current/doctrine/associations.html)

### Doctrine

- [Association Mapping (types de relations et notions d'unidirectionnelle et bidirectionelle)](https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/association-mapping.html)
- [Associations Update (Owning Side and Inverse Side)](https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/unitofwork-associations.html)
- [Référence des Annotations dont "@OrderBy" pour le classement des relations ArrayCollection](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/annotations-reference.html#orderby)

### Fiches récap' O'Clock

- [Relations](../../bdd/rdbms.md#relations)
- [Conception BDD générale](../../gestion-projet/conception-bd.md)

## Livecoding du jour

Objectif : réaliser l'association entre une table Product et une table Category.

Soit le MCD correspondant à notre besoin :

![](img/mcd-product-category.png)

### Make:entity

Depuis Symfony v4 nous utilisons la commande `php bin/console make:entity` sur `Category` nous permet de créer l'entité, puis sur `Product` de mettre à jour l'entité Product. L'assistant crée donc pour nous le code source adéquat.

### Mapping information

Nous avons une relation `ManyToOne` depuis `Product` vers `Category`

La relation peut-être **unidirectionnelle** ou **bidirectionnelle**. Tout d'abord créons la relation unidirectionnelle, à savoir que la relation sera décrite uniquement du côté du produit :

```php
// src/AppBundle/Entity/Product.php

// ...
class Product
{
    // ...

    /**
     * @ORM\ManyToOne(targetEntity="Category")
     * @ORM\JoinColumn(name="category_id", referencedColumnName="id")
     * (facultatif)
     */
    private $category;
}
```
Dans ce cas seuls les produits peuvent accéder à la catégorie, via `$product->getCategory()->getName()`.

Relation bidirectionnelle : si l'on souhaite également que les catégories accèdent aux produits liés, il faudra modifier la relation dans `Product` come suit :

```php
/* @ORM\ManyToOne(targetEntity="Category")
// devient
/* @ORM\ManyToOne(targetEntity="Category", inversedBy="products")
```

Et modifier la classe Category comme suit :

```php
// src/AppBundle/Entity/Category.php

// Ajout de la classe ArrayCollection de Doctrine
use Doctrine\Common\Collections\ArrayCollection;

class Category
{
    // ...

    /**
     * @ORM\OneToMany(targetEntity="Product", mappedBy="category")
     */
    private $products;

    public function __construct()
    {
        // Les produits liés seront stockés dans un ArrayCollection
        $this->products = new ArrayCollection();
    }
}
```
Dès lors, la catégorie pourra accéder aux produits via : `$products = $category->getProducts()`.

**ATTENTION, notion "Lazy loading"** : c'est uniquement lorsque nous souhaitons accéder aux objets liés que ceux-ci seront réellement récupérés par Doctrine, soit dans l'exemple 1 lorsque nous appellerons une propriété spécifique comme `$product->getCategory()->getName()`, dans l'exemple 2 quand nous bouclerons sur les produits issus de `$products = $category->getProducts()`.

### Sauvegarde des entités liées

Exemple :

```php
// Création d'un objet produit
$product = new Product();
$product->setName('Jean carotte');

// Création d'un objet catégorie
$category = new Category();
$category->setName('Pantalons');

// Associe l'objet catégorie à l'objet produit
$product->setCategory($category);

// Appel au Manager Doctrine
$em = $this->getDoctrine()->getManager();

// Demande à Doctrine de prendre en charge les objets
$em->persist($category);
$em->persist($product);

// Demande à Doctrine de stocker les données en bdd
$em->flush();
```

### Récupérer des objets liés

Exemple depuis un objet :

`$product->getCategory()->getName();`

Récupération d'une liste d'objet liés :

```php
$products = $category->getProducts();

foreach ($products as $product) {
    dump($product);
}
```

Pour classer par défaut les objets liés dans certains cas, voir [Référence des Annotations dont "@OrderBy" pour le classement des relations ArrayCollection](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/annotations-reference.html#orderby).

## Mini HowTo sur les _directions_

### mappedBy et inversedBy

Dans le doute il faut [se rapporter à la doc Doctrine](https://www.doctrine-project.org/projects/doctrine-orm/en/latest/reference/unitofwork-associations.html#bidirectional-associations).

**Ce qu'il faut retenir** pour notre exemple de Product et de Category c'est :

11 _"A bidirectional relationship has both an owning side and an inverse side"_ => ici on nous informe qu'il y'a une entité qui détient la relation, l'autre qui l'_"inverse"_.

11.1 (dans le désordre) :
- _"ManyToOne is always the owning side of a bidirectional association"_ => info importante ici, c'est la ManyToOne qui "détient" (own), donc dans notre exemple la Many(Product)ToOne(Category) est dans Product, c'est elle qui détient la relation.
- Puis : _"The **owning side** has to **use the inversedBy attribute** of the OneToOne, ManyToOne, or ManyToMany mapping declaration. The inversedBy attribute **contains the name of the association-field on the inverse-side**."_ => ici on nous indique quoi faire avec la _"owning side"_, donc Product dans notre exemple : `@ORM\ManyToOne(targetEntity="Category", inversedBy="products")`. Le champ indiqué dans inversedBy et mappedBy est le champ qui correspond à l'entité courante dans la targetEntity : ici  `products` correspond à la liste des produits contenues dans `Category`. Puis pour l'autre entité, c'est l'inverse.

**Pour résumer :**

1. Identifier qui est le "owning side".
2. Attribuer le `inversedBy` à l'Entité qui "own", et nommer dedans *le nom du champ (sans le $)* qui identifie cette Entité dans l'Entité cible (ici `products`)
3. Faire l'inverse avec l'autre Entité : `mappedBy` + nom du champ qui représente cette entité.

Le tout ça au niveau des relations OneToOne, OneToMany, et ManyToMany.

### Cascade, persist, remove, OnDelete...

A NOTER : **Doctrine will only check the owning side of an association for changes** : ici, cela indique qu'en cas d'associations d'objets, **seul l'objet qui détient la relation sera prise en compte pour persister l'objet**.

**OnDelete et cascade**

L'opération `cascade` permet à Doctrine de gérer la persistence (ajout, modification, suppression) des collections d'objets présents _dans la relation inverse_. Exemple avec User/Comment :

```php
<?php
class User
{
    //...
    /**
     * Bidirectional - One-To-Many (INVERSE SIDE)
     * @OneToMany(targetEntity="Comment", mappedBy="author", cascade={"persist", "remove"})
     */
    private $comments;
    //...
}
```
Cela ne vous empêche pas de devoir relier les 2 entités ensemble, par exemple `$newComment->setUser($this);`. Mais cela permet à Doctrine de persister tous les objets liés, sans que l'on ait besoin d'écrire : `$em->persist($newComment);`. Pensez à la cascade quand vous êtes face à une erreur du type : _An unknown entity has been found through a relation [...]_

- En savoir plus : [Documentation Doctrine](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/working-with-associations.html#transitive-persistence-cascade-operations)

Le cascade "remove" permet, de la même manière, de supprimer tous les Comment d'un User si on supprime un User donné.  
On peut également demander au SGBD (MySql) de faire cela à la place de l'ORM (Doctrine). Pour cela on indiquera au niveau de l'entité qui détient la relation, ici Comment, dans @JoinColumn :

```php
class Comment
    /**
     * @ORM\ManyToOne(targetEntity="User", inversedBy="comments")
     * @ORM\JoinColumn(onDelete="CASCADE")
     */
    private $author;
```

Ainsi quand on supprime User, les Comment associés sont supprimés par MySql. On choisira **soit** `cascade={"remove"}`, **soit** `JoinColumn(onDelete="CASCADE")`.

- Voir [la documentation Doctrine](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/working-with-objects.html#removing-entities)
- Et [cascade remove, orphanRemoval, onDelete, sur StackOverflow](https://stackoverflow.com/questions/27472538/cascade-remove-vs-orphanremoval-true-vs-ondelete-cascade)

### Associations ManyToMany

Comme indiqué dans [la documentation Doctrine _"Owning and Inverse Side on a ManyToMany Association"_](http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/association-mapping.html#owning-and-inverse-side-on-a-manytomany-association), vous pouvez choisir le côté qui "own" (et donc le _inversedBy_). Ensuite, il suffit d'ajouter la relation _inverse_ dans le `add` :
```php
<?php
class Article
{
    private $tags;

    public function addTag(Tag $tag)
    {
        $tag->addArticle($this); // synchronously updating inverse side
        $this->tags[] = $tag;
    }
}

class Tag
{
    private $articles;

    public function addArticle(Article $article)
    {
        $this->articles[] = $article;
    }
}
```
```php
<?php
$article = new Article();
$article->addTag($tagA);
$article->addTag($tagB);
```
## A savoir

- Commande pour créer une entité de façon interactive : `php bin/console doctrine:generate:entity`
- Debug Toolbar : icône des requêtes pour en savoir plus