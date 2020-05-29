# Les événements

## Préambule

La notion d'événement est assez vaste dans Symfony, cette fiche synthétise une partie de la documentation officielle disponible dans [Documentation > Guides > Event Dispatcher](http://symfony.com/doc/current/event_dispatcher.html).

## Aperçu

Dans Symfony, des événements sont émis depuis différents composants, notamment HTTP_Kernel et Form. Doctrine dispose également d'événements qui lui sont propres.

![](img/events.png)

Liens vers les _Documentations_ du schéma :

1. [Composant HTTP_Kernel](http://symfony.com/doc/current/components/http_kernel.html)
    - [Liste des events du Kernel](http://symfony.com/doc/current/reference/events.html)
2. [Composant Form](http://symfony.com/doc/current/form/events.html)
    - [Comment identifier le bon événement de formulaire ?](https://github.com/O-clock-Alumni/fiches-recap/blob/master/symfony/themes/form-events.md)
3. [Doctrine](http://symfony.com/doc/current/doctrine/lifecycle_callbacks.html)

=> Créer des listeners ou subscribers : [Event Dispatcher](http://symfony.com/doc/current/event_dispatcher.html)


## Principe

Pour intercepter un type d'événement, le principe est toujours le même ou presque :

- Identifier l'évenement qui va nous permettre de faire ce que l'on souhaite (en gros, où mettre un "hook" dans le processus d'éxécution de l'appli).
- On crée un listener ou un subscriber, qui réagit à tel ou tel événement (ou depuis une fonction anonyme pour les Forms).
    - Le listener doit être ajouté à `services.yml`, le subscriber est automatiquement reconnu.
- On récupère l'événement depuis la méthode appelée.
- On accède depuis l'événement reçu aux données qui nous intéressent.
- On code notre logique métier (business logic) => le but de la création de cet écouteur, en utilisant tout ou partie des données reçues de l'événement (modification de la requête, de la réponse, etc.).
- Puis l'éxécution de l'application reprend son cours normal.

Accessoirement, on peut :
- [Injecter d'autres services](http://symfony.com/doc/current/service_container.html#injecting-services-config-into-a-service) dans le constructeur du listener ou subscriber (voir `php bin/console debug:container --types`).
- Debugger les listeners et subscribers enregistrés, via :
    - `php bin/console debug:event-dispatcher` (tous events)
    - `php bin/console debug:event-dispatcher kernel.controller` (event particulier)

## Cas particuliers

### Forms

- Les événements peuvent être interceptés directement à la création du formulaire (fonction anonyme) ou dans des classes séparées (listener ou subscriber).

### Doctrine

- Doctrine dispose des `Lifecycles`, utilisables directement sur l'entité via les annotations.
- Si ça ne suffit pas, Doctrine permet également [l'usage des listeners et subscribers](http://symfony.com/doc/current/doctrine/event_listeners_subscribers.html).