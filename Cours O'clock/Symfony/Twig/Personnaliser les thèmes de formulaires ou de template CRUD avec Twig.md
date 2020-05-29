# Personnalisation des éléments Twig

La personnalisation avec Twig est détaillée dans ces trois pages de documentation, assez denses :

- [How to Customize Form Rendering](https://symfony.com/doc/current/form/form_customization.html)
- [How to Control the Rendering of a Form](https://symfony.com/doc/current/form/rendering.html)
- [How to Work with Form Themes](https://symfony.com/doc/current/form/form_themes.html)

## Exemple d'application du thème Bootstrap pour nos formulaires

### Installer Boostrap dans votre layout via :

```html
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
```

Cf : http://getbootstrap.com/

### Option 1 : Activer Bootstrap 3 intégré à Symfony

```yml
# app/config/config.yml
twig:
    form_themes:
        - bootstrap_3_layout.html.twig
```

Voir [Documentation > Reference > Configuration > twig](http://symfony.com/doc/current/reference/configuration/twig.html)

### Option 2 : Surcharger vos templates de formulaires

Depuis [cette page (que vous avez lue/parcourue)](https://symfony.com/doc/current/form/form_customization.html#what-are-form-themes) : utilisez par exemple le *built-in form theme* "bootstrap_3_layout.html.twig" :
- [afficher la page github](https://github.com/symfony/symfony/blob/master/src/Symfony/Bridge/Twig/Resources/views/Form/bootstrap_3_layout.html.twig),
- copier-coller tout le code Twig dans une page `app/Resources/views/form/boostrap.html.twig`, [comme indiqué ici](https://symfony.com/doc/current/form/form_customization.html#method-2-inside-a-separate-template).
- puis utiliser ce template depuis une page Twig de formulaire (`post/new.html.twig` par ex.), via `{% form_theme form 'form/bootstrap.html.twig' %}`
- vérifier que le thème Bootstrap est appliqué.

Pour plus de cohérence Bootstrap globale (marges notamment), dans votre layout `base.html.twig`, mettez ce snippet autour du `block body` ou quelque part dans votre layout, si pas déjà présent :

```twig
<div class="container">
    <div class="row">
        <div class="col-xs-12">

        {% block body %}{% endblock %}

        </div>
    </div>
</div>
```

Vous devriez obtenir un formulaire centré avec le style Boostrap. Sinon, vérifiez chaque étape ci-dessus.

### Surcharge globale

Pour appliquer ce thème dans tous vos formulaires sans utiliser `{% form_theme ... %}` il suffit de renseigner dans votre fichier `config.yml` (sous réserve d'avoir nommé votre fichier ainsi) :

```yml
twig:
    form_themes:
        - 'form/bootstrap.html.twig'
```

- [Source](https://symfony.com/doc/current/form/form_customization.html#making-application-wide-customizations!)

## Surcharger un template CRUD généré avec SensioGeneratorBundle

Lorsque vous utilisez la commande `php bin/console doctrine:generate:crud`, les squelettes qui servent de base à la création de cette page peuvent être modifiés. Ces squelettes se trouvent dans le generator-bundle, à cet emplacement :

- `vendor/sensio/generator-bundle/Resources/skeleton/crud/views/*.html.twig.twig` ces pages sont en fait des templates de templates.

Imaginons que l'on souhaite surcharger le squelette de la page _index_ nous allons copier-coller le template correspondant dans notre application à l'emplacement :

- `app/Resources/SensioGeneratorBundle/skeleton/crud/views/index.html.twig.twig`
=> l'arborescence du bundle source est conservée.

Il ne vous reste plus qu'à modifier le code de ce template selon vos besoins, puis de générer les CRUDS associés.

- [Source](http://symfony.com/doc/current/bundles/SensioGeneratorBundle/index.html#overriding-skeleton-templates)