Introduction au système de bundle
=================================

Un bundle est similaire à la notion de plugin, mais "en mieux". La différence est que dans Symfony _tout_ est un bundle, depuis le noyau du framework jusqu'à votre code d'application. Vous pouvez ainsi utiliser des bundles tiers ou distribuer les vôtres. Il est donc facile de choisir quelles fonctionnalités vous souhaitez activer dans votre application et de les régler selon vos besoins.

Un bundle est un ensemble de fichiers rassemblés dans un dossier et qui implémente une fonctionnalité, par exemple un BlogBundle, un ForumBundle, un bundle pour gérer les utilisateurs.

Les bundles utilisés par votre application doivent être activés dans la classe `AppKernel` :

```php
// app/AppKernel.php
public function registerBundles()
{
    $bundles = array(
        new Symfony\Bundle\FrameworkBundle\FrameworkBundle(),
        new Symfony\Bundle\SecurityBundle\SecurityBundle(),
        new Symfony\Bundle\TwigBundle\TwigBundle(),
        new Symfony\Bundle\MonologBundle\MonologBundle(),
        new Symfony\Bundle\SwiftmailerBundle\SwiftmailerBundle(),
        new Symfony\Bundle\DoctrineBundle\DoctrineBundle(),
        new Sensio\Bundle\FrameworkExtraBundle\SensioFrameworkExtraBundle(),
        new AppBundle\AppBundle(),
    );

    if (in_array($this->getEnvironment(), array('dev', 'test'))) {
        $bundles[] = new Symfony\Bundle\WebProfilerBundle\WebProfilerBundle();
        $bundles[] = new Sensio\Bundle\DistributionBundle\SensioDistributionBundle();
        $bundles[] = new Sensio\Bundle\GeneratorBundle\SensioGeneratorBundle();
    }

    return $bundles;
}
```
Vous pouvez ici contrôler quel bundle est utilisé, en l'activant ou le désactivant.

Créer un bundle
---------------

L'_Edition Standard de Symfony_ ou les projets créés par défaut avec l'éxécutable `symfony new my_project` vous fournit un bundle prêt-à-l'emploi, nommé `AppBundle`.

**Exemple de code minimal pour définir un bundle**

```php
// src/Acme/TestBundle/AcmeTestBundle.php
namespace Acme\TestBundle;

use Symfony\Component\HttpKernel\Bundle\Bundle;

class AcmeTestBundle extends Bundle
{
}
```

**Activation du bundle**

```php
// app/AppKernel.php
public function registerBundles()
{
    $bundles = array(
        // ...

        // register your bundle
        new Acme\TestBundle\AcmeTestBundle(),
    );
    // ...

    return $bundles;
}
```

**Créer un bundle avec la ligne de commaned Symfony**

`php bin/console generate:bundle --namespace=Acme/TestBundle`

Cette commande ajoute le bundle pour vous dans le ficher `AppKernel`.

Continuer sur Symfony.com
-------------------------

- [Le système de bundle](http://symfony.com/doc/current/bundles.html)
- [Bonnes pratiques avec les bundles](http://symfony.com/doc/current/bundles/best_practices.html)