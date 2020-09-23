Cookies, Session, FlashMessages
======================================

Lire et écrire dans un cookie
-----------------------------

D'après la doc : https://symfony.com/doc/current/components/http_foundation.html#setting-cookies

Ecrire dans un cookie, exemple depuis un contrôleur  :

```php
/**
 * @Route("/cookie/set", name="cookie_set")
 */
public function cookieSetAction(Request $request)
{
    $response = new Response();
    $response->headers->setCookie(new Cookie('dog', 'Rex');
    $response->send();
    
    return $this->redirectToRoute('homepage');
}
```

Lire depuis un contrôleur :
```php
$dog = $request->cookies->get('dog');
```
Lire depuis Twig :
```php
{{ app.request.cookies.get('dog') }}
```

Utiliser la session
-------------------

La session peut être utilisée de manière très simple depuis un contrôleur comme ceci :

```php
use Symfony\Component\HttpFoundation\Session\SessionInterface;

public function indexAction(SessionInterface $session)
{
    // Stocke un attribut pour utilisation lors d'une requête ultérieure
    $session->set('name', 'Charles');

    // Récupère un attribut définit dans un contrôleur d'une autre requête du même utilisateur
    $foobar = $session->get('name');

    // Utilisation d'une valeur par défaut (argument 2) si l'attribut 'name' n'existe pas
    $name = $session->get('name', 'Anonymous');
}
```

Messages Flash
--------------

Les messages Flash sont des messages qui sont stockés puis effacés au moment où vous les récupérer. Très pratique pour indiquer une notification d'une requête à l'autre, ici suite à une soumission de formulaire :

```php
use Symfony\Component\HttpFoundation\Request;

public function updateAction(Request $request)
{
    // ...

    if ($form->isSubmitted() && $form->isValid()) {
        // Traite le formulaire
        // ...

        $this->addFlash(
            'notice',
            'Your changes were saved!'
        );

        return $this->redirectToRoute(...);
    }

    return $this->render(...);
}
```
`$this->addFlash()` est équivalent à `$request->getSession()->getFlashBag()->add()`.

Les messages Flash sont dont stockés dans la session.

Affichage des messages
----------------------

```twig
{# app/Resources/views/base.html.twig #}

{# you can read and display just one flash message type... #}
{% for message in app.flashes('notice') %}
    <div class="flash-notice">
        {{ message }}
    </div>
{% endfor %}

{# ...or you can read and display every flash message available #}
{% for label, messages in app.flashes %}
    {% for message in messages %}
        <div class="flash-{{ label }}">
            {{ message }}
        </div>
    {% endfor %}
{% endfor %}
```

Voir [la documentation du contrôleur](https://symfony.com/doc/current/controller.html#managing-the-session).

Le composant Session complet
============================

Voir [la documentation du composant Session](https://symfony.com/doc/current/components/http_foundation/sessions.html).