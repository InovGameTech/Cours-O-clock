## Données de test, données factices

### DoctrineFixturesBundle

Ce bundle vous permet de créer des entités depuis un fichier spécifique dans lequel le Manager de Doctrine est disponible. La fonction contenue dans ce fichier est éxécutée en ligne de commande, vous évitant ainsi de polluer votre code source avec l'ajout de données de test.

http://symfony.com/doc/current/bundles/DoctrineFixturesBundle/index.html

Dorénavant avec Symfony 4, la commande `make:fixtures` est disponible pour initialiser vos fichiers de fixtures.

### Faker

Faker est une libriaire qui permet de générer automatiquement des données factices, avec des possibilités de personnalisation poussées. Faker propose également un pont pour créer des données depuis des entités Doctrine.

https://github.com/fzaninotto/Faker

> A noter
> -------
> La relation ManyToMany n'est pas prise en charge, voir l'issue que nous avons posée ici : https://github.com/fzaninotto/Faker/issues/1201
>
> Solution si nécessaire : utiliser une table de jointure réelle OneToMany/ManyToOne (convertir la relation ManyToMany en une entité PHP).

### Astuce d'utilisation combinée DoctrineFixturesBundle + Faker

Faker propose [un "Populator" pour Doctrine, voir ici](https://github.com/fzaninotto/Faker#populating-entities-using-an-orm-or-an-odm).  
L'ajout de données via DoctrineFixturesBundle étant assez rébarbative, on peut très bien intégrer `Faker` dans le fichier `AppFixtures.php` :

```php
// src/DataFixtures/AppFixtures.php
namespace App\DataFixtures;

use Faker;
use Doctrine\Bundle\FixturesBundle\Fixture;
use Doctrine\Common\Persistence\ObjectManager;

class AppFixtures extends Fixture
{
    public function load(ObjectManager $manager)
    {
        // On crée une instance de Faker en français
        $generator = Faker\Factory::create('fr_FR');
        // On passe le Manager de Doctrine à Faker !
        $populator = new Faker\ORM\Doctrine\Populator($generator, $manager);
        $populator->addEntity('App\Entity\Movie', 10);
        // On peut passer en 3ème paramètre le générateur de notre choix, ici un "name" cohérent pour Person
        $populator->addEntity('App\Entity\Person', 20, array(
          'name' => function() use ($generator) { return $generator->name(); },
        ));
        // On demande à Faker d'éxécuter les ajouts
        $insertedEntities = $populator->execute();
        // Si besoin de manipuler les entités créées
        // dump($insertedEntities);
    }
}
```