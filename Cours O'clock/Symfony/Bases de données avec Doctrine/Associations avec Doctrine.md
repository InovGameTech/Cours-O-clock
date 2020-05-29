## Symfony : Les bases de données et l'ORM Doctrine

Une des tâches les plus courantes pour toute application est la lecture et l'écriture en base de données.
Symfony fournit une intégration d'une librairie tierce appelée Doctrine, dont le seul objectif est de
vous donner des outils simples et puissants pour interagir avec la base de données.

[Site du projet Doctrine](http://www.doctrine-project.org/)

Principe de l'ORM Doctrine :

![](img/doctrine-orm.png)

Exercice inspiré de la doc : http://symfony.com/doc/current/doctrine.html

## Un produit

Afin de comprendre le fonctionnement de Doctrine nous allons créer un produit, le sauvegarder
et le récupérer.

### Configurer la base de données

**Les paramètres sont à configurer dans un nouveau fichier** `.env.local` _(puis seront utilisés par Doctrine dans `config/packages/doctrine.yaml`)_. Ce fichier reste sur votre dépôt local car ignoré par git.

Une fois la configuration faite, on éxécute la commande de création de bdd depuis la racine de notre projet via la console Symfony : `php bin/console doctrine:database:create`

## Création de la classe Entité _(phase de création)_

Cela correspond aux modèles que nous avons déjà créés depuis le début de la formation en MVC :
TodoModel, WeatherModel etc.
Nous créons une class Product via la ligne de commande `php bin/console make:entity` et nous renseignons le informations voulues.

### Ajout des informations de mapping

Les informations ont été ajoutées directement par `make` dans le fichier d'entité.

Rappel du principe ORM et schéma Doctrine.

![](http://symfony.com/doc/current/_images/mapping_single_entity.png)

Les infos de mapping, les "metadata", sont un ensemble de règles qui indique à Doctrine comment
notre classe Post doit être mappée vers telle table de la base de donnée. Ici encore les formats
YAML ou XML sont possibles pour décrire les metadatas, mais nous utiliserons à nouveau les annotations
déjà vues précédemment, pour leur efficacité :

```php
// src/Entity/Product.php
namespace App\Entity;

use Doctrine\ORM\Mapping as ORM;

/**
 * @ORM\Entity(repositoryClass="App\Repository\ProductRepository")
 */
class Product
{
    /**
     * @ORM\Id
     * @ORM\GeneratedValue
     * @ORM\Column(type="integer")
     */
    private $id;

    /**
     * @ORM\Column(type="string", length=255)
     */
    private $name;

    /**
     * @ORM\Column(type="integer")
     */
    private $price;

    public function getId()
    {
        return $this->id;
    }

    // ... getter and setter methods
}
```

**Types de champs Doctrine** : http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/basic-mapping.html

Suite à quoi vous pouvez demander à Doctrine de valider la sémantique de votre mapping via :

`php bin/console doctrine:schema:validate`

### Générer les getters et les setters

Ils ont été ajoutées directement par `make` dans le fichier d'entité.

Vous pouvez égaelement utiliser votre IDE ou via Atom avec le plug-in _"PHP Getters and Setters"_. Mais également utiliser la commande `php bin/console make:entity --regenerate` si vous avez fait des modifications manuelles.

### Mettre à jour le schéma de la base de données

Créer le code SQL de migration : `php bin/console make:migration`

L'éxécuter : `php bin/console doctrine:migrations:migrate`

### Modifier des champs de l'entité par la suite

Vous pouvez répéter les opérations ci-dessus autant de fois que nécessaire.

## Persister les objets vers la base de données _(Entity Manager)_

Créons un contrôleur pour expérimenter : `php bin/console make:controller ProductController`

```php
// src/Controller/ProductController.php
namespace App\Controller;

// ...
use App\Entity\Product;

class ProductController extends Controller
{
    /**
     * @Route("/product", name="product")
     */
    public function index()
    {
        // you can fetch the EntityManager via $this->getDoctrine()
        // or you can add an argument to your action: index(EntityManagerInterface $entityManager)
        $entityManager = $this->getDoctrine()->getManager();

        $product = new Product();
        $product->setName('Keyboard');
        $product->setPrice(1999);
        $product->setDescription('Ergonomic and stylish!');

        // tell Doctrine you want to (eventually) save the Product (no queries yet)
        $entityManager->persist($product);

        // actually executes the queries (i.e. the INSERT query)
        $entityManager->flush();

        return new Response('Saved new product with id '.$product->getId());
    }
}
```

## Récupérer des objets depuis la base de données _(entity repository)_

Supposons que nous ayons une route qui affiche notre `Post` basé sur son `id` :

```php
// src/Controller/ProductController.php
// ...

/**
 * @Route("/product/{id}", name="product_show")
 */
public function show($id)
{
    $product = $this->getDoctrine()
        ->getRepository(Product::class)
        ->find($id);

    if (!$product) {
        throw $this->createNotFoundException(
            'No product found for id '.$id
        );
    }

    return new Response('Check out this great product: '.$product->getName());

    // or render a template
    // in the template, print things with {{ product.name }}
    // return $this->render('product/show.html.twig', ['product' => $product]);
}
```

_Raccourci avec la **signature automatique**_

En passant un `id` en paramètre, Symfony est capable de fournir l'objet correspondant (ici `$product`) sans avoir à le récupérer avec `find()`. Le _type hinting_ (suggestion de type) et l'injection de dépendance sont utilisés :

```php
// src/Controller/ProductController.php

use App\Entity\Product;
// ...

/**
 * Conversion automatique via la signature de la méthode (injection)
 * @Route("/product/{id}", name="product_show")
 */
public function show(Product $product)
{
    // use the Product!
    // ...
}
```

### Objet Repository

Pour récupérer des objets on passe par le "Repository", une classe dont c'est la fonction :

```php
$repository = $this->getDoctrine()->getRepository(Product::class); // Raccourci vers 'AppBundle\Entity\Product'
```

**Liste des méthodes fournies par défaut (récupérer des objets uniques ou multiples) :**

```php
$repository = $this->getDoctrine()->getRepository(Product::class);

// query for a single product by its primary key (usually "id")
$product = $repository->find($productId);

// dynamic method names to find a single product based on a column value
$product = $repository->findOneById($productId);
$product = $repository->findOneByName('Keyboard');

// dynamic method names to find a group of products based on a column value
$products = $repository->findByPrice(1999);

// find *all* products
$products = $repository->findAll();
```
De plus, les méthodes `findBy` et `findOneBy` acceptent un tableau de paramètres
pour des conditions multiples :

```php
$repository = $this->getDoctrine()->getRepository(Product::class);

// query for a single product matching the given name and price
$product = $repository->findOneBy(
    array('name' => 'Keyboard', 'price' => 1999)
);

// query for multiple products matching the given name, ordered by price
$products = $repository->findBy(
    array('name' => 'Keyboard'),
    array('price' => 'ASC')
);
```

### Mettre à jour un objet

```php
// Après avoir récupéré l'objet
$product->setName('New product name!');
$em->flush();
// A noter : $em->persist() pas utile ici car récupéré via Doctrine
```

### Supprimer un objet

De la même manière mais depuis l'entity manager :

```php
// Après avoir récupéré l'objet
$em->remove($post); // en mémoire (intention)
$em->flush(); // en bdd ! (execute DELETE)
```
## D'autres façons d'accéder aux données

### Doctrine Query language (DQL)

http://symfony.com/doc/current/doctrine.html#querying-for-objects-with-dql

### Doctrine Query Builder

http://symfony.com/doc/current/doctrine.html#querying-for-objects-using-doctrine-s-query-builder

QueryBuilder documentation (http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/query-builder.html)

### Organiser vos requêtes spécifiques dans une classe Repository

Afin de laisser des requêtes plus complexes hors du contrôleur, Doctrine prévoit une classe Repository permettant de conserver la logique de recherche en un endroit :

http://symfony.com/doc/current/doctrine/repository.html

### SQL pur via DBAL
- Voir : https://symfony.com/doc/current/doctrine/dbal.html

### Native SQL
- Voir : http://docs.doctrine-project.org/projects/doctrine-orm/en/latest/reference/native-sql.html

### Extensions DQL MySql
- Voir : https://stackoverflow.com/questions/26298175/doctrine-querybuilder-date-format-not-working

=> Pour activer certaines fonctions SQL non disponibles dans Doctrine.

## Schéma récapitulatif Doctrine dans Symfony

![](img/doctrine-symfony.png)