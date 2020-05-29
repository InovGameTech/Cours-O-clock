# Tests

Ajouter des lignes de code à votre application ajoute potentiellement de nouveaux bugs. Pour créer des applications plus fiables, il est recommandé de créer des tests unitaires et des tests fonctionnels.

[D'après la doc Symfony : Testing](https://symfony.com/doc/current/testing.html).

# Installer PHPUnit

Installation via composer du bundle PHPUnitBridge :

```
composer require --dev symfony/phpunit-bridge
```

On vérifie et/on installe les paquets manquants via :

`./bin/phpunit` ou `php bin/phpunit` sous Windows.

## Tests fonctionnels

### Principe d'un test fonctionnel :

- Exécuter une requête
- Optionnel : Cliquer sur un lien ou un formulaire
- Tester la réponse
- Recommencer

### Etude du test fourni avec `php bin.console make:functional-test`

```php
<?php

namespace App\Tests\Controller;

use Symfony\Bundle\FrameworkBundle\Test\WebTestCase;

/**
 * Classe de test du DefaultController
 */
class DefaultControllerTest extends WebTestCase
{
    public function testHomepage()
    {
        // Crée un client
        $client = static::createClient();
        // Exécute une requête vers la home
        $crawler = $client->request('GET', '/');
        
        // Affirme que le status code de la requête est entre 200 et 299
        $this->assertResponseIsSuccessful();
        // Affirme que le h1 du DOM reçu contient le texte 'Hello World'
        $this->assertSelectorTextContains('h1', 'Hello World');
    }
}
```

## Exécuter un test

Depuis la racine du projet, en ligne de commande :

```
// éxécute tous les tests de l'application
php bin/phpunit

// éxécute tous les tests du répertoire Utils
php bin/phpunit tests/Utils

// éxécute un test en particulier
php bin/phpunit tests/Utils/CalculatorTest.php
```

## Test minimal pour les routes accessibles

http://symfony.com/doc/current/best_practices/tests.html#functional-tests

## Simuler une authentification pour les tests

http://symfony.com/doc/current/testing/http_authentication.html

## Tests et recettes

Référence et philosophie des tests : http://www.test-recette.fr/