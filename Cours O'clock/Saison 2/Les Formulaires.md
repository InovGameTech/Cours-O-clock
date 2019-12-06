# Les formulaires

## form

`<form>` permet de définir une zone de formulaire dans une page. 

```html
<form action="traitement.php" method="POST">
  <input type="text" name="prenom">
  <input type="submit">
</form>
```

Le formulaire pourra être composé de cases à cocher, listes de choix, champ de saisie, etc...

```html
  <input type="text">
  <input type="radio">
  <input type="checkbox">
  <select>
  	<option>1</option>
  	<option>2</option>
  </select>
```
etc...

2 attributs sont nécessaires 
- `action` contient l'adresse de la page où les informations du formulaire seront envoyées
- `method` défini la méthode utilisée pour envoyer ces données, les valeurs possibles sont `GET` ou `POST`

### Envoyer les informations

#### Un nom distinct

Les champs souhaitants être utilisés pour transmettre des informations doivent posséder l'attribut `name` qui associe un nom à la future valeur.

```html
<input type="text" name="prenom">
```

#### Une valeur

Des données peuvent être attribuées par défaut aux champs dans leur attribut `value` (à l'exception de `<textarea>la valeur est ici</textarea>`)

```html
<input type="text" name="prenom" value="jean-françois">
```

```html
<textarea name="message">la valeur est ici</textarea>
```

#### Soumission

Afin d'envoyer les informations saisies, il faut un déclencheur.

Il peut être de 2 types

- **`submit`** `<input type="submit" value="Envoyer">`
- **`<bouton>`** `<button>Envoyer</button>`


## Labels

Les labels permettent d'ajouter un titre contextuel à un champ

```html
<label>Prénom</label>
<input type="text" name="prenom">
```

Il est possible d'associer le label et le champ qu'il représente avec l'attribut `for` sur le label qui devra faire écho à l'attribut `id` placé sur l'élément en rapport. Un clic sur le label lancera un focus du champ associé.

```html
<label for="champ-prenom">Prénom</label>
<input type="text" id="champ-prenom" name="prenom">
```

## Les champs textes

|Type de champ|HTML                      | Note                                                                                 |
|-------------|------------------------- | -------------------------------------------------------------------------------------|
|Texte        |`<input type="text">`     | N'importe quel contenu texte                                                         |
|Email        |`<input type="email">`    | Vérifie la bonne structuration d'une adresse email                                   |
|Mot de passe |`<input type="password">` | Le contenu est remplacé par des `*`                                                  |
|Nombre       |`<input type="number">`   | Valeur modifiable par saisie, avec les flèches du clavier ou via les boutons intégrés|
|Zone de texte|`<textarea></textarea>`   | Idéal pour des saisies sur plusieurs lignes                                          |

Un attribut très pratique le `placeholder` permet d'afficher à l'intérieur d'un champ vide la valeur attendue

```html
<input type="text" name="prenom" placeholder="Votre prénom...">
```

## Radio & checkbox

### Checkbox

Il est possible d'ajouter un attribut `checked` afin de sélectionner une option particulière par défaut

```html
<label>
  <input type="checkbox"> Je suis d'accord avec les termes...
</label>
```

### Radio

Il est possible d'ajouter un attribut `checked` afin de sélectionner une option particulière par défaut

L'attribut `name` est le point commun entre toutes les valeurs associées

```html
<label>Situation personnelle</label>
<label>
  <input type="radio" name="statut"> Célibataire
</label>
<label>
  <input type="radio" name="statut"> Marié
</label>
<label>
  <input type="radio" name="statut"> Divorcé
</label>
<label>
  <input type="radio" name="statut"> Veuf
</label>
```

### Choisir entre radio et checkbox

Une checkbox se suffit à elle même pour avoir un intérêt, elle peut être cochée ou non. Les radios n'ont un intérêt que lorsqu'il y a au moins 2 possibilités.

- **checkbox** `j'ai lu et j'accepte les conditions générales...`
- **Radio** Civilité `Madame`, `Monsieur`

## Liste de sélection

### Choix unique
Une liste de sélection est l'association de l'élément de liste `<select>` et de plusieurs éléments `<option>` qui représentent les choix possibles.

`<select>` prendra l'attribut `name` et les différentes `<option>` la valeur associée grâce à `value`.

Il est possible d'ajouter un attribut `selected` ou `selected="selected"` afin de sélectionner une option particulière par défaut. Sans cet attribut, le premier `<option>`de la liste est sélectionné par défaut.

```html
<label for="film-like">Quel film avez-vous préférez</label>
<select name="" id="film-like">
  <option value="film1">Star Wars IV</option>
  <option value="film2" selected>Star Wars V</option>
  <option value="film3">Star Wars VI</option>
</select>
```

### Choix multiples

Avec un attribut `multiple` sur le `<select>` il est possible de définir une liste à choix multiples.

En utilisant la touche `cmd` sur Mac ou `ctrl` sur Linux ou Windows il est possible de sélectionner plusieurs options

```html
<label for="film-like">Quel film avez-vous préférez</label>
<select name="" id="film-like">
  <option value="film1">Star Wars IV</option>
  <option value="film2">Star Wars V</option>
  <option value="film3">Star Wars VI</option>
  <option value="film3">Star Wars VII</option>
</select>
```





