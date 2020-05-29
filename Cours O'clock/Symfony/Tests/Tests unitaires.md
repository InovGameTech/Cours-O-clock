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

## Tests unitaires

Un test unitaire permet de tester une classe simple (comme un Service Symfony par exemple).

Exemple de test d'une classe "Calculatrice".

```php
// src/App/Util/Calculator.php
namespace App\Util;

class Calculator
{
    public function add($a, $b)
    {
        return $a + $b;
    }
}
```
Pour tester cela, créer le fichier suivant :

```php
// tests/App/Util/CalculatorTest.php
namespace Tests\App\Util;

use App\Util\Calculator;
use PHPUnit\Framework\TestCase;

class CalculatorTest extends TestCase
{
    public function testAdd()
    {
        $calc = new Calculator();
        $result = $calc->add(30, 12);

        // Affirme que votre Calculatrice ajoute les nombres correctement
        $this->assertEquals(42, $result);
    }
}
```

Pour lancer le test : `phpunit tests/App/Util/CalculatorTest.php`

[Continuer sur le site de Symfony](http://symfony.com/doc/current/testing.html)