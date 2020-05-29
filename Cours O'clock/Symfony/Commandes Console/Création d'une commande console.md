# Commande console

Issu de la doc : http://symfony.com/doc/current/console.html

## Introduction

Symfony permet la création de commandes depuis `bin/console` depuis le composant Console.

## Créer une commande

La commande doit être crée dans le namespace `Command` de votre bundle. Le nom de classe doit se terminer par le suffixe `Command`.

## Configurer une commande

```php
$this
->setName('app:create-user') // the name of the command (part after "bin/console")
->setDescription('Creates a new user.') // short description shown by "php bin/console list"
->setHelp('This command allows you to create a user...') // shown by the "--help" option
```

## Exécuter une commande

`php bin/console app:create-user`

**Ecrire dans la sortie terminal**

```php
protected function execute(InputInterface $input, OutputInterface $output)
{
    // Ligne unique avec retour à la ligne
    $output->writeln('Whoa!');

    // Lignes multiples avec retour à la ligne
    $output->writeln([
        'User Creator',
        '============',
        '',
    ]);

    // Message sans retour ligne
    $output->write('You are about to ');
    $output->write('create a user.');
}
```

## Options et arguments (console input)

```php
protected function configure()
{
    $this
    ->addArgument('name', InputArgument::REQUIRED, 'Who do you want to greet?')
    ->addArgument('last_name', InputArgument::OPTIONAL, 'Your last name?')
    ->addOption('dump', InputOption::VALUE_OPTIONAL);
    ;
}

protected function execute(InputInterface $input, OutputInterface $output)
{
    $name = $input->getArgument('name');
    $lastName = $input->getArgument('last_name');

    // Faire quelque chose avec $name et $lastname

    if($input->getOption('dump')) {
        // Si option --dump présente, affiche un log par ex.
    }
}

```

- **Aller plus loin avec les arguments et options :** http://symfony.com/doc/current/console/input.html  
- **Poser des questions à l'utilisateur :** http://symfony.com/doc/current/components/console/helpers/questionhelper.html

## Utiliser les services depuis la commande

Pour cela vous devez non plus étendre de `Command` mais de `ContainerAwareCommand`. Cela vous donne accès au container, donc à tous les services :

```php
use Symfony\Bundle\FrameworkBundle\Command\ContainerAwareCommand;

class CreateUserCommand extends ContainerAwareCommand
{
    // ...

    protected function execute(InputInterface $input, OutputInterface $output)
    {
        // access the container using getContainer()
        $doctrine = $this->getContainer()->get('doctrine');
        $repository = $doctrine->getRepository($input->getArgument('entity'));
        $rows = $repository->findAll();

        // Faire quelque chose avec $rows
    }
}
```

## Exécuter une commande depuis un contrôleur

Voir : http://symfony.com/doc/current/console/command_in_controller.html

## Aller plus loin

http://symfony.com/doc/current/console.html