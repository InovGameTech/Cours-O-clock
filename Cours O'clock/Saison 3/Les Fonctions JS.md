# Fonctions JS

Voir également la fiche [Objectifs](./objectifs.md).

## Interactions

### En fenêtre

- `alert(message)`
affiche une pop-up avec un message et un bouton `OK` :
``` js
alert('Hello!');
```

- `prompt()`
affiche une pop-up / boîte de dialogue permettant à l'utilisateur de saisir une valeur, avec un bouton `OK` pour valider, et possibliité d'`Annuler` :
``` js
name = prompt('What is your name ?', 'type your name here');
// name contiendra la chaîne de caractères entrée par l'utilisateur
// si l'utilisateur à annuler, name vaut null
```

- `confirm()`
affiche une boîte de dialogue permettant à l'utilisateur de choisir entre `Annuler` et `OK` :
```js
confirmation = confirm('Êtes-vous sûr ?');
// confirmation vaudra true (OK) ou false (Annuler)
```

**Note** : `alert()`, `prompt()`, `confirm()` bloquent l'exécution du JS, la page est « en pause. »

Voir également la fiche [DOM](dom.md).

### En console

[[MDN] Console](https://developer.mozilla.org/fr/docs/Web/API/Console)

- `console.log()` : affiche un message dans la console
- `console.info()` : alias de `console.log()`
- `console.warn()` : affiche un message d'avertissement (jaune avec icône) dans la console
- `console.error()` : affiche un message d'erreur (rouge avec icône d'erreur) dans la console

## Fonctions sur les variables

- `Number(string)` : transforme une chaîne de caractère en nombre (ex : `Number('42') => 42`)
- `parseInt(string)` : transforme une chaîne de caractère en nombre (comme `Number()`), mais en plus, est capable de rechercher les chiffres en début de texte pour les transformer en nombre (ex : `parseInt('3 pommes') => 3`)

### Fonctions sur les chaînes de caractères

##### length

[[MDN] String.length](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/String/length)

Permet de recupérer la longueur d'une chaîne de caractères :

```js
chaine = 'Une phrase assez courte.';

console.log(chaine.length); // => 24
```

##### indexOf()

[[MDN] String.indexOf()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/String/indexOf)

Permet de récupérer le premier index d'un élément dans une chaîne de caractères

```js
'fruits'.indexOf('i'); // => 3 (index 3 de la chaîne)
'fruits'.indexOf('a'); // => -1 ('a' n'est pas trouvé)
```

##### lastIndexOf()

[[MDN] String.lastIndexOf()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/String/lastIndexOf)

Permet de récupérer l'index de la position de la dernière occurence d'un élément dans une chaîne de caractères :

```js
'banane'.lastIndexOf('a'); // => 3 (index 3 de la chaîne, ie. 4ème lettre)
'banane'.lastIndexOf('f'); // => -1 ('f' n'est pas trouvé, donc -1)
```

### Fonctions sur les tableaux

##### length

[[MDN] Array.length](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/length)

Permet de recupérer le nombre d'éléments que possède un tableau :

```js
fruits = ['banane', 'clémentine', 'orange'];

console.log(fruits.length); // => 3
```

##### indexOf()

[[MDN] Array.indexOf()](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Objets_globaux/Array/indexOf)

Permet de recupérer l'index de la position de la première occurence d'un élément dans un tableau :

```js
fruits = ['banane', 'clémentine', 'orange'];

fruits.indexOf('orange'); // => 2 (index 2 du tableau fruits, ie. 3ème élément)
fruits.indexOf('banane'); // => 0 (index 0 du tableau fruits, ie. 1er élément)
fruits.indexOf('pomme'); // => -1 (pomme n'est pas trouvé, donc -1)
```

### Module `Math`

- `Math.random()` : génère un nombre aléatoire entre 0 et 1
- `Math.round()` : arrondi un nombre à l'entier le plus proche
- `Math.floor()` : arrondi un nombre à l'entier inférieur
- `Math.ceil()` : arrondi un nombre à l'entier supérieur