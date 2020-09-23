# Twig, moteur de template recommandé

Quand le contrôleur a besoin de générer du HTML, du JSON ou n'importe quel autre contenu, il délègue ce travail au moteur de template (_template engine_). Avec Symfony il est recommandé d'utiliser Twig comme moteur de template, bien que PHP soit également une possibilité.

## Rappel : Rendre un template (contrôleur)

Depuis un contrôleur Symfony, la méthode `render()` nous permet de rendre un template et de le renvoyer dans un objet `Response` directement :

```php
// Rend la vue située dans app/Resources/views/lucky/number.html.twig
return $this->render('lucky/number.html.twig', array('name' => $name));
```

La méthode `render()` prend comme paramètres _le fichier de template_ et le cas échéant _un tableau de valeurs à transmettre au template_.

> A partir d'ici on résumera la documentation officielle ["Démarrer avec Twig"](https://symfony.com/doc/current/templating.html).

## Templates

Les 3 types de syntaxes spécifiques à Twig :

`{{ ... }}` : **affiche** une variable ou une expression.

`{% ... %}` : un **mot-clé (tag)** qui contrôle la logique du template (for, if, etc.).

`{# ... #}` : un **commentaire** Twig, ligne simple ou multi-ligne. Le commentaire ne sera pas visible dans la page rendue.

Twig contient également des filtres et des fonctions :

`{{ title|upper }}` : applique le filtre `upper` à la variable `title`.

Fonction qui affiche la classe `odd` ou `even` en cyclant sur la valeur de `i`.

```twig
{% for i in 1..10 %}
    <div class="{{ cycle(['even', 'odd'], i) }}">
      <!-- some HTML here -->
    </div>
{% endfor %}
```

## Héritage de template et gabarits (layouts)

A l'instar d'une classe PHP et de ses propriétés, l'héritage permet de définir un gabarit (layout) de base qui contient des éléments de votre page ou site, appelés **blocks**. L'enfant qui étend d'un tel gabarit peut donc redéfinir chacun de ces blocks (tout ou partie).

Exemple de layout :

```twig
{# app/Resources/views/base.html.twig #}
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>{% block title %}Test Application{% endblock %}</title>
    </head>
    <body>
        <div id="sidebar">
            {% block sidebar %}
                <ul>
                    <li><a href="/">Home</a></li>
                    <li><a href="/blog">Blog</a></li>
                </ul>
            {% endblock %}
        </div>

        <div id="content">
            {% block body %}{% endblock %}
        </div>
    </body>
</html>
```

Ce template définit un squelette HTML de base. Trois zones `{% block %}` sont définies et peuvent être surchargées. Le template peut être rendu tel quel. Si le block contient déjà un contenu par défaut (ici `title` et `sidebar`) ce contenu sera conservé.

Exemple de template enfant :

```twig
{# app/Resources/views/blog/index.html.twig #}
{% extends 'base.html.twig' %}

{% block title %}My cool blog posts{% endblock %}

{% block body %}
    {% for entry in blog_entries %}
        <h2>{{ entry.title }}</h2>
        <p>{{ entry.body }}</p>
    {% endfor %}
{% endblock %}
```

Le mot-clé `extends` indique d'évaluer d'abord le template de base, qui contient les différents blocks, puis le template enfant est rendu et les blocks du parent sont remplacés par ceux de l'enfant.

Dans notre exemple seuls les blocks `title` et `body` sont remplacés.

## Tags et helpers

Quelques tags et fonctions utiles (helper) livrées ave Twig pour Symfony.

### Inclure des templates

Imaginons un article présent sur différentes pages, nous pourrions le définir tel que :

```twig
{# app/Resources/views/article/article_details.html.twig #}
<h2>{{ article.title }}</h2>
<h3 class="byline">by {{ article.authorName }}</h3>

<p>
    {{ article.body }}
</p>
```

Et l'utiliser ainsi via `include()` :

```twig
{# app/Resources/views/article/list.html.twig #}
{% extends 'layout.html.twig' %}

{% block body %}
    <h1>Recent Articles<h1>

    {% for article in articles %}
        {{ include('article/article_details.html.twig', { 'article': article }) }}
    {% endfor %}
{% endblock %}
```
La variable `article` est passée en paramètre de la fonction via la syntaxe de la forme `{ 'article': article, 'key2': value2, 'key3': value3 }`.

### Liens vers des pages
Fonction `path()` :

```twig
<a href="{{ path('welcome') }}">Home</a>`
```
`welcome` étant la route nommée dans votre routing (annotation, YML, XML ou PHP).

Si la route contient des paramètres, on doit les ajouter à la fonction `path()` de la même manière pour `include()`:

```php
/**
 * @Route("/article/{slug}", name="article_show")
 */
```
Puis dans le template :
```twig
{# app/Resources/views/article/recent_list.html.twig #}
{% for article in articles %}
    <a href="{{ path('article_show', {'slug': article.slug}) }}">
        {{ article.title }}
    </a>
{% endfor %}
```

### Liens vers des Assets

Assets = images, fichiers JS, CSS etc. Symfony fournit une fonction qui crée le chemin vers ces fichiers pour vous :

```twig
<img src="{{ asset('images/logo.png') }}" alt="Symfony!" />
<link href="{{ asset('css/blog.css') }}" rel="stylesheet" />
```

Le chamin de votre asset est basé sur le dossier `web` de votre application, qui est la racine de votre site web depuis un navigateur.

### Inclure CSS et JS

La meilleure façon est d'utiliser l'héritage, afin de permettre d'inclure les JS et CSS par défaut dans le layout global puis d'ajuster selon les pages, comme suit :

```twig
{# app/Resources/views/base.html.twig #}
<html>
    <head>
        {# ... #}

        {% block stylesheets %}
            <link href="{{ asset('css/main.css') }}" rel="stylesheet" />
        {% endblock %}
    </head>
    <body>
        {# ... #}

        {% block javascripts %}
            <script src="{{ asset('js/main.js') }}"></script>
        {% endblock %}
    </body>
</html>
```
Puis dans la page enfant :

```twig
{# app/Resources/views/contact/contact.html.twig #}
{% extends 'base.html.twig' %}

{% block stylesheets %}
    {{ parent() }}

    <link href="{{ asset('css/contact.css') }}" rel="stylesheet" />
{% endblock %}

{# ... #}
```

## Aller plus loin

- [Twig Reference](https://twig.symfony.com/doc/2.x/#reference)
- [Accéder à Request, User ou Session](https://symfony.com/doc/current/templating/app_variable.html)
- [Echappement (output escaping) - Sécurisation des données affichées](https://symfony.com/doc/current/templating/escaping.html)
- [Symfony Twig Extensions Reference](http://symfony.com/doc/current/reference/twig_reference.html)
- [Injecter des variables globales accessible via Twig](http://symfony.com/doc/current/templating/global_variables.html)
- [Utiliser PHP comme moteur de template](http://symfony.com/doc/current/templating/PHP.html)

A consulter absolument au moins une fois :
- [Plein de recettes pratiques avec Twig !](https://symfony.com/doc/current/templating.html#learn-more)