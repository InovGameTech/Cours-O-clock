### Les Rôles

Condensé de [la doc Symfony sur les rôles](https://symfony.com/doc/3.4/security.html#denying-access-roles-and-other-authorization).

#### Restriction, rôles, autorisation

L'autorisation permet de définir comment un utilisateur accède à quelle ressource (URL, modèle, méthode).

1. Le User reçoit un jeu de rôles, par ex. ROLE_ADMIN, ROLE_USER.
2. Vous ajoutez du code de manière à ce qu'une ressource soit accédée via ce rôle.

#### Rôles

En bdd, ils peuvent être liés un un champ du User (champ texte ou table liée).
Les rôles doivent contenir le préfixe `ROLE_` et libre à vous de définir la suite
par ex. ROLE_BLOG_ADMIN, ROLE_TEACHER etc.
Assurez-vous que par défaut un utilisateur ait un rôle minimum, par convention
il s'agit de ROLE_USER.

**Les différentes façons de sécuriser votre code :**

- via security.yml, par un motif d'URL (en regexp), attention la première route qui correspond sera prise en compte (donc mettre les routes les plus "profondes" ou les routes à protéger en priorité d'abord) :
```yml
security:
    access_control:
        # Restreint à ROLE_SUPER_ADMIN
        - { path: ^/admin/users, roles: ROLE_SUPER_ADMIN }
        # require ROLE_ADMIN for /admin*
        - { path: ^/admin, roles: ROLE_ADMIN }
        # Si on avait inversé les 2 routes, ROLE_ADMIN aurait pu accéder à la route /admin/users, puisque /admin aurait "matchée" en premier
```

- depuis l'intérieur d'un contrôleur
```php
public function helloAction($name)
{
    // The second parameter is used to specify on what object the role is tested.
    $this->denyAccessUnlessGranted('ROLE_ADMIN', null, 'Unable to access this page!');
```

- idem via annotation (possible d'annoter aussi la classe contrôleur tout en haut) :

```php
use Sensio\Bundle\FrameworkExtraBundle\Configuration\Security;

/**
 * @Security("has_role('ROLE_ADMIN')")
 */
public function helloAction($name)
{
```

- dans les templates, si on souhaite conditionner un affichage :

```twig
{% if is_granted('ROLE_ADMIN') %}
    <a href="...">Delete</a>
{% endif %}
```
#### Get User

Récupérer l'objet User connecté et ses propriétés.

- depuis un contrôleur SEULEMENT si le user est authentifié(*):
    - `$user = $this->getUser();`
    - `$user->getUsername();`

(*) A lire : http://symfony.com/doc/current/security.html#always-check-if-the-user-is-logged-in

- depuis un template, si on souhaite savoir si un utilisateur s'est connecté avec succès (donc n'est PAS anonyme) :
```twig
{% if is_granted('IS_AUTHENTICATED_FULLY') %}
    <p>Username: {{ app.user.username }}</p>
{% endif %}
```

#### Hiérarchie des rôles

Si vous souhaitez attribuer les rôles en cascade :

```twig
# app/config/security.yml
security:

    role_hierarchy:
        ROLE_ADMIN:       ROLE_USER
```

Voir : http://symfony.com/doc/3.4/security.html#hierarchical-roles