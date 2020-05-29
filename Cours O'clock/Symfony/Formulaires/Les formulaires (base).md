# Formulaires avec Symfony

## Le composant Form

Le framework Symfony utilise le composant Symfony Form, décrit ici : [Components/Form](http://symfony.com/doc/current/components/form.html).

Cette doc vous donne tous les détails de fonctionnement et d'usage du le composant Form. Vous devez au moins la survoler même si vous n'en comprenez pas tous les tenants et aboutissants.

**Références**

- [Référence des Types de Champ](http://symfony.com/doc/current/reference/forms/types.html)
- [Référence des Contraintes de Validation](http://symfony.com/doc/current/reference/constraints.html)

## En bref

**Usage depuis un contrôleur**

On fait appel au "Form Builder" via :
```php
$form = $this->createFormBuilder()
```
Auquel on ajoute des champs et des contraintes de validation :
```php
$form = $this->createFormBuilder()
    ->add('task', TextType::class, array(
        'constraints' => new NotBlank(),
    ))
    ->add('dueDate', DateType::class, array(
        'constraints' => array(
            new NotBlank(),
            new Type(\DateTime::class),
        )
    ))
    ->getForm();
```
`getForm()` nous permet de récupérer l'objet de formulaire `$form` ainsi créé.

A fin de traiter le formulaire nous utilisons ces méthodes :

```php
// Equivaut à faire correspondre les données $_POST avec notre objet $form
$form->handleRequest($request);

    // SI formulaire soumis ET SI formulaire valide
    if ($form->isSubmitted() && $form->isValid()) {
        // data is an array with "name", "email", and "message" keys
        $data = $form->getData();
        // Dumper les données
        dump($data);
    }
```

Si l'on souhaite récupérer la valeur d'un champ spécifique, disons le champ _optinNewsletter_ : `$form->get('optinNewsletter')->getData();`

Afficher le formulaire via Twig :
```twig
{{ form(form) }}
```
Ou
```twig
{{ form_start(form) }}
{{ form_widget(form) }}
{{ form_end(form) }}
```
## Référence : formulaire sans entité

[Form sans entité](http://symfony.com/doc/current/form/without_class.html) (récapitule certains des éléments ci-dessus).

## Aller plus loin

Protection des formulaires contre les attaques CSRF :
- [Explication en vidéo](https://www.youtube.com/watch?v=58y6772MHKw)
- [Wikipédia](http://en.wikipedia.org/wiki/Cross-site_request_forgery)