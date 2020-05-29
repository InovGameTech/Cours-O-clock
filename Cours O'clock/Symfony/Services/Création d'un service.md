# Utilisation et création de services avec Symfony

D'après la doc officielle : https://symfony.com/doc/current/service_container.html

## Introduction

Un service est objet qui remplit une fonction associée à une configuration.

Ce concept permet d'éviter de dupliquer du code au comportement identique au sein d'une même application (contrôleur ou autre) et en le factorisant dans une classe dédiée.

Voici quelques exemples de besoins courants :

- Upload d'une image: 
    - _Un utilisateur doit pouvoir modifier sa photo de profil_
    - _Un utilisateur doit pouvoir inclure des images dans un contenu_
    - ... 

- Création d'un fichier PDF: 
    - _Un client doit pouvoir récupérer sa facture au format PDF_
    - _Un marchand doit pouvoir obtenir un recapitulif mensuel de ses ventes au format PDF_
    - ... 

- Envoyer un mail:
    - _Un client doit pouvoir recevoir le recapitulatif de sa commande par email_
    - _Un utilisateur doit pouvoir envoyer un email à l'administrateur du site via le formulaire de contact_
    - ...

Symfony est donc plein de services utiles tels que Mailer, Twig , Doctrine, Session et plein d'autres encore.

## Le conteneur de services

Pour pouvoir gérer l'orchestration de cet ensemble d'objets aux fonctionnalités diverses, chaque service est associé à un objet spécial appelé le **service container**.

Le conteneur de services permet d'organiser et d'instancier nos services à la demande :
   - en utilisant l'[injection de dépendance](https://putaindecode.io/articles/injection-de-dependances-en-php/) 
   - en appelant directement le service par son nom directement sur l'objet `container` (possible mais ce n'est pas une bonne pratique en règle générale)

> Note: Le fait de pouvoir injecter directement un service dans une methode de contrôleur est spécifique aux contrôleurs de chez Symfony. Dans tout les autres cas les services s'injectent directement dans le constructeur de la classe concernée.

### Fonctionnement

Le schéma suivant montre un exemple d'actions effectuées par le conteneur de service.

![](https://github.com/O-clock-Alumni/fiches-recap/blob/master/symfony/themes/img/service.png)


## Accéder et utiliser les services

Les services sont accessibles à tout moment depuis un contrôleur, en utilisant la suggestion de type et l'injection de dépendance :

```php
// src/AppBundle/Controller/ProductController.php
// ...

use Psr\Log\LoggerInterface;

/**
 * @Route("/products")
 */
public function list(LoggerInterface $logger)
{
    $logger->info('Look! I just used a service');

    // ...
}
```

Le nom des services disponibles dans votre application Symfony sont accessibles via :

- Liste des services avec alias: `php bin/console debug:autowiring`

- Liste tout les services sans alias compris: `php bin/console debug:autowiring --all`

- Liste tout les services du container (ancienne version fonctionnelle): `php bin/console debug:container`

Si vous connaissez le nom de ce service, vous pouvez l'appeler depuis un contrôleur via :

```php
$logger = $this->container->get('logger');
$mailer = $this->container->get('mailer');
$session = $this->container->get('session');
// Autre façon d'appeler $this->getDoctrine()->getManager();
$entityManager = $this->container->get('doctrine.entity_manager');
```

> Note: Cette methode n'est pas préconisée par Symfony 4 mais peux être utile dans certain cas notamment sur une version < 3.4

## Créer et configurer des services

Créez votre service dans le dossier `App\Service` :

```php
// src/App/Service/MessageGenerator.php
namespace App\Service;

class MessageGenerator
{
```
Note: Il est aussi proposé de gérer la création de vos services dans `App\Utils` (cf best practices). Auquel cas, il faut adapter la création de votre dossier & namespace en conséquence. 

Puis dans votre contrôleur :

```php
use App\Service\MessageGenerator;

public function new(MessageGenerator $messageGenerator)
{
    // thanks to the type-hint, the container will instantiate a
    // new MessageGenerator and pass it to you!
    // ...

    $message = $messageGenerator->getHappyMessage();
    $this->addFlash('success', $message);
```

Depuis Symfony 3.3, le service est configuré automatiquement.

On peut accéder au service via son `id` qui dans ce cas est son nom de classe :

```php
// only works if your service is public
$messageGenerator = $this->get(MessageGenerator::class);
```

## Injecter d'autres services ou une configuration dans un service

Dans le service :

### Sans paramètre

```php
use Psr\Log\LoggerInterface;

class MessageGenerator
{
    private $logger;

    public function __construct(LoggerInterface $logger)
    {
        $this->logger = $logger;
    }

    public function getHappyMessage()
    {
        $this->logger->info('Message generated!');
        // ...
    }
}
```

### Avec paramètres

```php
use Psr\Log\LoggerInterface;

class MessageGenerator
{
    private $logger;
    private $loggingEnabled;

    public function __construct(LoggerInterface $logger, $loggingEnabled)
    {
        $this->logger = $logger;
        $this->loggingEnabled = $loggingEnabled;
    }

    public function getHappyMessage()
    {
        if ($this->loggingEnabled) {
            $this->logger->info('Message generated!');
        }
        // ...
    }
}
```

Dans la config du service :

```yml
# app/config/services.yml
parameters:
    enable_message_logging:  true

services:
    App\Service\MessageGenerator:
        arguments:
            $loggingEnabled: '%enable_message_logging%'
```

On peut aussi récupérer ce paramètre directment depuis le contrôleur :
```php
// this ONLY works if you extend Controller
$adminEmail = $this->container->getParameter('admin_email');

// or a shorter way!
// $adminEmail = $this->getParameter('admin_email');
```

## Public Versus Private Services

```php
// but accessing directly from the container does NOT Work if private (default)
$this->container->get(MessageGenerator::class);
```

```yml
# app/config/services.yml
services:
    # ... same code as before

    # explicitly configure the service
    App\Service\MessageGenerator:
        public: true
```

https://symfony.com/doc/current/service_container.html#public-versus-private-services