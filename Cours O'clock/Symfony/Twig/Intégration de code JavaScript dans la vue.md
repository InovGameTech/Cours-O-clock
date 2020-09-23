# Intégrer du JavaScript dans les vues

## Exemple d'usage simple

Prenons l'exemple de notre blog, où nous souhaitons afficher le nombre de caractères saisis dans un champ text ou textarea.

Créons le fichier qui contient le code JS de notre fonctionnalité dans `web/js/` :

```js
$(document).ready(function(e) {

    function caracterCount($field) {
        var counter = $field.val().length;
        var target = $field.next();
        target.html(counter);

    }
    // Ajoute un span à chaque classe "js-count"
    $(".js-count").after('<span class="js-count-total">0</span> caractères saisis.');
    // Ecoute le release de la touche du clavier
    $(".js-count").keyup(function count() {
        caracterCount($(this));
    });

    $(".js-count").each(function(index) {
        caracterCount($(this));
    })
});
```
Intégrons ce fichier JS dans notre layout global (ainsi que jQuery si non déjà intégré) :

Fichier `app/Resources/views/base.html.twig`

```twig
{% block javascripts %}
<script src="https://code.jquery.com/jquery-3.2.1.slim.min.js"></script>
<script src="{{ asset('js/caracter-count.js') }}"></script>
{% endblock %}
```

Puis dans notre fichier de définition de formulaire, ajoutons l'attribut `'class="js-count"'`. Avec Symfony cela se fait en ajoutant la valeur `'class' => 'js-count'` au tableau de paramètres `'attr'` :

```php
// ...
->add('title', null, [
        'label' => 'Titre du post',
        'attr' => [
            'placeholder' => 'Veuillez mettre un titre optimisé SEO',
            'help_text' => 'Mais surtout ne dépassez pas 60 caractères.',
            'class' => 'js-count',
        ]
    ])
->add('image', FileType::class, ['label' => 'Illustration'])
->add('body', null, [
    'label' => 'Corps du post',
    'attr' => [
        'class' => 'js-count',
    ]
])
// ...
```
A l'édition ou à l'ajout d'un Post vous devriez voir :

![](img/twig-js-car-count.png)