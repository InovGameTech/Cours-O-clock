# Routing et Controllers

## Les fondamentaux HTTP avec Symfony

Nous vous conseillont la lecture de cette page issue du site de Symfony :  
[Symfony : les fondamentaux HTTP](http://symfony.com/doc/current/introduction/http_fundamentals.html)

## Classes Request et Response

Dans Symfony, les classes Request et Response sont des représentations objet de ces requêtes, et contiennent les informations relatives à la requête HTTP, et des méthodes qui facilitent leur manipulation.

**Le composant HttpFoundation en détail :** https://symfony.com/doc/current/components/http_foundation.html

**L'API de Request et Response :**
On voit ici le code source de ces deux classes, il permettra de connaitre les méthodes et propriétés disponibles !

* Définition de la classe Request (https://github.com/symfony/symfony/blob/4.3/src/Symfony/Component/HttpFoundation/Request.php)
* Définition de la classe Response (https://github.com/symfony/symfony/blob/4.3/src/Symfony/Component/HttpFoundation/Response.php)

## FrontController et Router

### Front Controller

Le FrontController sert de point d'entrée unique d'une application MVC, il permet d'organiser le routage et d'éxécuter la méthode de controller attendue, en fonction de la requête du visiteur.  
[En savoir plus sur le FrontController et le AppKernel](http://symfony.com/doc/current/configuration/front_controllers_and_kernel.html)  

![Request / Response](https://symfony.com/doc/current/_images/http/request-flow.svg)

[En savoir plus (doc symfony)](http://symfony.com/doc/current/introduction/http_fundamentals.html)

### Routage

Le routage consiste à déterminer l'action à éxécuter en fonction de la requête reçue.
Le Composant *Router* de Symfony permet de :  
* définir les routes de votre application et les mapper avec les méthodes correspondantes. La configuration des routes se fait dans le fichier de config `routing.yml`,
* générer l'url correspondante à une route donnée,
* il peut être accessible en tant que *service* dans les controllers ou d'autres composants de l'application,
* et il met à disposition des [commandes console](http://symfony.com/doc/current/routing/debug.html) permettant de débugger les routes de votre application.

[Pour aller plus loin, Composant Router (avancé)](http://symfony.com/doc/current/components/routing.html)

### Définition des routes

* définir une route :
  ```
  # app/config/routing.yml
  shop_list:
      path:     /shop
      defaults: { _controller: AppBundle:Shop:list }
  ```
* définir une route avec des paramètres variables ("wildcards")
  ```
  shop_show:
    path:     /shop/{slug}
    defaults: { _controller: AppBundle:Shop:show }
  ```
* définir des contraintes [("requirements")](http://symfony.com/doc/current/routing/requirements.html)
  ```
  shop_list:
    path:      /shop/{page}
    defaults:  { _controller: AppBundle:Shop:list }
    requirements:
        page: '\d+'
  ```
  Ces contraintes sont définies grâce aux expressions régulières.
* définir des valeurs par défaut pour les paramètres
  ```
  shop_list:
    path:      /shop/{page}
    defaults:  { _controller: AppBundle:Shop:list, page: 1 }
    requirements:
        page: '\d+'
  ```

### Routes avec annotations

_Méthode recommandée_

```php
/**
 * Correspond à /blog/*
 *
 * @Route("/blog/{slug}", name="blog_show")
 */
public function showAction($slug)
{
    // $slug sera égal à la partie dynamique de l'URL
    // soit à l'URL /blog/super-routing, then $slug='super-routing'

    // ...
}
```

## Préciser la méthode

Avec l'annotation `@Route` vous pouvez spécifier quelle(s) méthode(s) sont autorisées pour une route en ajoutant un attribut `methods`.  
Exemple :

```php
/**
 * @Route("/edit/{id}", methods={"GET","POST"})
 */
public function editAction($id)
{
}
```

## Aller plus loin

- [Pour aller plus loin, _"Guide du Routeur"_](https://symfony.com/doc/current/routing.html)
- Expressions régulières : [Cheat sheet](https://i.stack.imgur.com/S5b87.jpg) et [Online tester](https://regex101.com/)

## Controller

### Méthodes de Controller

Une méthode de controller (sauf celles qui ne sont jamais appelées directement par une route) prend toujours un objet *Request* comme paramètre, et renvoie toujours un objet *Response*.  

Voir [la liste des méthodes ici](https://github.com/symfony/framework-bundle/blob/master/Controller/ControllerTrait.php).

### AbstractController

Le framework Symfony comprend notamment un "contrôleur de base" qui propose des méthodes utiles "prêtes à utiliser". Il vous suffit de faire hériter les controllers de votre application de cette classe.
Ces méthodes permettent notamment de :

* render, renderView : appeler un template
* createNotFoundException, createAccessDeniedException: renvoyer un [statut HTTP](https://fr.wikipedia.org/wiki/Liste_des_codes_HTTP) particulier (erreurs 404, 403, 500...)
* generateUrl: générer une url pour une route donnée
* rediriger le visiteur
* récupérer les services disponibles dans l'application (router, session...)
* Déclencher [une redirection interne vers une autre action](https://symfony.com/doc/current/controller/forwarding.html) (forward)
* Pour récupérer un paramètre depuis `parameters.yml` ou `config.yml > parameters:`, il suffit d'utiliser la méthode `$this->getParameter('secret');`
