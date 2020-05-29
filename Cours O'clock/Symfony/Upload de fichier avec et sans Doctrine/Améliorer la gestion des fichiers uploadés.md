# Améliorer la gestion des fichiers uploadés

Si vous testez votre formulaire d'upload, en ajout et en édition, vous vous rendrez vite compte que des erreurs sont générées dans les différente pages ou contrôleurs, ou encore qu'une image existante disparait de votre base de déonnées (mais pas de votre répertoire d'upload).

Il nous suffit d'ajouter des vérifications à certains endroits.

## Gestion CREATE et EDIT

**A l'ajout** d'un nouveau fichier, nous vérifions simplement si un fichier est uploadé avant de le stocker :

Voir `PostController::newAction` :

```php
// Gestion de l'image, si existante
if($post->getImage()) {
    // Récupération du champ image du formulaire reçu
    $file = $post->getImage();
    // Génère un nom unique pour le fichier avant de le sauvegarder
    $fileName = md5(uniqid()).'.'.$file->guessExtension();
    // Déplacement du fichier dans un répertoire de notre projet
    $file->move($this->getParameter('images_directory'), $fileName);
    // Met à jour le nom de l'image finale dans notre Post
    $post->setImage($fileName);
}
```

Attention toutefois à ce que votre champ _image_ puisse être _nullable_ ou vide par défaut, sinon si aucun fichier n'est envoyé à l'ajout, vous aurez une erreur SQL.

**A l'édition**, nous vérifions également si un fichier est présent MAIS SURTOUT, nous stockons la valeur du fichier si elle existe, afin que cette valeur ne soit pas écrasée si le fichier n'est pas remplacé :

Voir `PostController::editAction`:

```php
public function editAction(Request $request, Post $post)
{
    // Stocker le nom de l'image courante si existante
    $currentImage = $post->getImage();

    // ...

    $editForm = $this->createForm('AppBundle\Form\PostType', $post);
    $editForm->handleRequest($request);
    if ($editForm->isSubmitted() && $editForm->isValid()) {

        // ...

        // Gestion de l'image, si existante
        if($post->getImage()) {
            // Récupération du champ image du formulaire reçu
            $file = $post->getImage();
            // Génère un nom unique pour le fichier avant de le sauvegarder
            $fileName = md5(uniqid()).'.'.$file->guessExtension();
            // Déplacement du fichier dans un répertoire de notre projet
            $file->move($this->getParameter('images_directory'), $fileName);
            // Met à jour le nom de l'image finale dans notre Post
            $post->setImage($fileName);
        }
        else {
            // Si fichier non remplacé, on lui passe le nom du fichier actuel
            // car $post a été modifié au traitement du formulaire
            $post->setImage($currentImage);
        }

```
Ainsi, vous évitez de supprimer malencontreusement le fichier présent s'il n'est pas modifié.

## Modification du champ Twig FileType

Par défaut, lorsque vous affichez le champ FileType, vous ne voyez pas si le fichier associé existe ou non. **Nous pouvons afficher, par exemple, une vignette de notre image** (cela pourrait être simplement une icône générique d'image ou de PDF selon le type de fichier traité).

L'objectif est d'obtenir à minima ceci :

<kbd>![](img/twig-forms-file-image.png)</kbd>

**Pour cela nous allons surcharger le block _file_widget_ via Twig**, comme nous l'avons vu dans [Surcharger les formulaires avec Twig](themes/twig-forms.md) :

Création du nouveau fichier de thème pour le champ FileType :

```twig
{% block file_widget %}
    {% spaceless %}

    {{ block('form_widget') }}
    {% if form.vars.data is not null and form.vars.data.filename is not null %}
        <img src="{{ asset('/images/' ~ form.vars.data.filename) | imagine_filter('post_edit_thumb') }}"/>
    {% endif %}

    {% endspaceless %}
{% endblock %}
```
1. Ici nous indiquons que nous surchargeons le block _file_widget_, qui rend lui-même le block par défaut _form_widget_, auquel nous ajoutons notre code personnel.
2. La valeur de notre champ image se trove dans _form.vars.data.filename_ (voir dump de _form_ ci-dessous).
3. La vignette est traitée via un filtre _Imagine_ comme vu dans [Manipulation d'images avec LiipImagineBundle](liip-imagine-bundle.md).

Accès à la valeur _filename_ de notre champ :

`{{ dump(form) }}`

```dump
FormView {#586 ▼
  +vars: array:25 [▼
    "value" => ""

    // ...

    "data" =>File {#452 ▼path: "/var/www/html/sfblog/app/../web/uploads/images"
      filename: "0bfbdc3aa490342f71f466920c41b49e.jpeg"

      // ...

    "type" => "file"
  ]
  // ...
  ```

## Gestion du DELETE

Supprimer le fichier stocké en cas de delete : _à rédiger_