# Upload de fichier avec Symfony

L'utilisation basique d'envoi de fichier depuis un formulaire et un champ `FieldType` :

https://symfony.com/doc/current/reference/forms/types/file.html

# Exemple d'upload de PDF avec Doctrine

[D'après la documentation](http://symfony.com/doc/current/controller/upload_file.html)

## Commentaire de code

### Dans l'entité
- On ajoute le champ qui contiendra _le nom de notre fichier_, ici `$brochure`.
- On y ajote la contrainte `@Assert\File` contenant le type MIME autorisé. Pour autoriser plusieurs types : `@Assert\File(mimeTypes={ "application/pdf", "image/jpeg", ... })`
- On oublie pas de générer les getters/setters et de mettre à jour le schéma bdd.

### Dans le formulaire de note Entité

- On ajoute le type FileType

### Dans la vue du formulaire

- Soit on ne fait rien si le formulaire est généré automatiquement.
- Soit on ajoute la ligne `{{ form_row(form.brochure) }}` si chaque champ est rendue un par un dans le template du form.

### Dans le contrôleur AJOUT et EDIT

- On récupère le fichier : `$file = $product->getBrochure();`.
- On crée un nom de fichier unique en devinant l'extension MIME : `$fileName = md5(uniqid()).'.'.$file->guessExtension();`.
- On déplace le fichier à l'endroit voulu : `$file->move(
    $this->getParameter('brochures_directory'),
    $fileName
    );`
- On met à jour l'entité pour stocker le nom du fichier : `$product->setBrochure($fileName);`

Le paramètre `'brochures_directory'` est créé dans `config.yml`, par exemple :

```yml
# app/config/config.yml

# ...
parameters:
    brochures_directory: '%kernel.root_dir%/../web/uploads/brochures'
```

Pour créer un lien vers le fichier uploadé on pourra écrire :

```twig
<a href="{{ asset('uploads/brochures/' ~ product.brochure) }}">Voir la brochure (PDF)</a>
```

### Dans le contrôleur EDIT (Important !)

Si vous avez déjà un champ qui contient _le nom_ de votre fichier en bdd, vous devez fournir un objet de type FILE au formulaire. Et le faire AVANT la création du formulaire.

```php
use Symfony\Component\HttpFoundation\File\File;
// ...

public function editAction(Product $product)
{
    // Le fichier réel sur le système, passé à $product
    $product->setBrochure(
        new File($this->getParameter('brochures_directory').'/'.$product->getBrochure())
    );

    // Création du formulaire
    $form = $this->createForm(ProductType::class, $product);

```

### Meilleure gestion des fichiers uploadés

[Astuces liés à la modification de fichiers existants](upload-more.md)

### Aller plus loin

+ [Création d'un service pour centraliser la logique des uploads hors des contrôleurs](https://symfony.com/doc/current/controller/upload_file.html#creating-an-uploader-service).
+ [Création d'un écouteur Doctrine pour uploader le fichier après persistence](https://symfony.com/doc/current/controller/upload_file.html#using-a-doctrine-listener).