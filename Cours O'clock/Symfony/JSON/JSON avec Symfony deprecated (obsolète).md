# JSON `deprecated (obsolète)`

## Convertir une donnée en JSON depuis PHP et Symfony

Depuis un tableau PHP, `json_encode()` est capable de générer le JSON correspondant (même si le tableau contient des tableaux imbriqués). [Voir `json_encode()` sur php.net](http://php.net/manual/fr/function.json-encode.php).

Par exemple :

```php
$tableau = array (
  'actors' => [
    [
      'id' => 1,
      'name' => 'Audrey Tautou',
    ],
    [
      'id' => 2,
      'name' => 'Jean Dujardin',
    ],
  ],
);

json_encode($tableau);

// Donne :
```
```json
{
  "actors": [
    {
      "id": 1,
      "name": "Audrey Tautou"
    },
    {
      "id": 2,
      "name": "Jean Dujardin"
    }
  ]
}

```

**Mais ce n'est pas le cas avec des entités** et encore moins s'ils sont imbriqués les uns dans les autres, pour cela vous pouvez soit :

- **Parcourir votre objet et le convertir en tableau vous-même** (création d'un nouveau tableau qui peut contenir des tableaux), **puis utiliser json_encode** pour générer le JSON associé.
- **Générer votre fichier JSON avec Twig (monfichier.json.twig) : plutôt pratique !** Et renvoyer la vue **avec render et un objet JsonResponse**;
- **Utiliser le serializer de Symfony** : http://symfony.com/doc/current/components/serializer.html : concepts à apprendre et à pratiquer.

## Affichage d'un template sous forme de JSON

Exemple en Twig pour nos acteurs dans un fichier `Resources/views/movie/actors.json.twig` :

```twig
{
  "actors": [
    {% for actor in actors %}
    {
      "id": {{ actor.id }},
      "name": "{{ actor.name }}"
    }
    {% if not loop.last %}
    ,
    {% endif %}
    {% endfor %}
  ]
}
```

## Pratique

Editeur, correcteur, formateur JSON en ligne : http://www.jsoneditoronline.org/