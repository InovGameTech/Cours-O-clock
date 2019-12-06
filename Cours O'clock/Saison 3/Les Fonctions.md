# Les fonctions

Tout comme une variable sert à stocker une valeur, une fonction sert à stocker des instructions, pour les utiliser plus tard/loin dans le programme. Il y a toujours deux temps : définition d'une fonction, puis exécution de la-dite fonction.

Des fonctions telles que `alert` ou `prompt` sont disponibles par défaut dans JavaScript (on parle de fonctions natives). On peut également définir ses propres fonctions.

Une fonction peut éventuellement recevoir des informations de la part de la personne qui l'utilise, pour contextualiser son travail (notions de paramètres/arguments), ce qui en fait un outil très polyvalent.

## Fonction simple (sans paramètre)

### Définition

Pour définir une fonction, on utilise le mot-clé `function` et un bloc d'instructions délimité par des accolades :

```js
function hello() {
  console.log('hello world !');
}
```

> Attention, la structure minimaliste pour définir une fonction sera toujours `function nomDeLaFonction() {}`. Les parenthèses notamment sont obligatoires.

Il est également possible de définir une fonction anonyme, et de la stocker dans une variable :

```js
var hello = function () {
  console.log('hello world !');
};
```

> La différence entre fonction nommée et fonction anonyme tient surtout du style personnel. Dans les deux cas, l'exécution sera identique. Une fonction anonyme est parfois plus difficile à gérer dans les messages d'erreur.

### Exécution

```js
hello(); // produira un 'hello world !' dans la console
```

## Fonction avec valeur de retour

La définition d'une fonction peut prévoir que celle-ci retourne une valeur, avec le mot-clé `return` :

```js
function getMessage(name) {
  return 'hello ' + name +' !';
}
```

La personne utilisant (exécutant) la fonction peut, si elle le souhaite, récupérer et par exemple stocker cette valeur de retour :

``` js
// La variable message contiendra 'hello Gringo !'
var message = getMessage('Gringo');
```

**Attention** : quand le moteur JS rencontre une instruction `return`, il quitte la fonction (toute instruction ultérieure dans la fonction est ignorée).

## Fonction avec des paramètres

Si on souhaite utiliser une fonction mais que son travail dépend d'informations qui ne sont pas connues au moment de sa définition, il est possible de les lui fournir au moment de son exécution :

### Définition

La définition indique alors que la fonction prend un (ou plusieurs) **paramètre(s)**, par exemple ci-dessous `name`. 
Le paramètre est en fait une variable locale (définie uniquement au sein de la fonction), dont la valeur n'est pas spécifiée car inconnue à ce stade. La variable sera créée automatiquement lors de l'exécution, et contiendra alors une valeur précise.

```js
function hello(name) {
  console.log('hello ' + name +' !');
}
```

### Exécution

Lors de l'exécution, on passe en **argument** une valeur, par exemple ci-dessous `'Gringo'`. Cette valeur est assignée à la variable `name` dans le corps de la fonction, `name` étant le nom du paramètre qui correspond.

```js
hello('Gringo'); // produira un 'hello Gringo !' dans la console
```

**Que se passe t-il à l'exécution ?**

1. La fonction `hello` est appelée avec un argument `'Gringo'`.
2. La fonction ayant été définie avec un paramètre `name`, cet appel est valide.
3. Une variable `name` est créée et existera le temps que la fonction s'exécute. Elle stocke l'argument donné, c'est-à-dire la valeur `'Gringo'`. C'est comme si avant d'exécuter la fonction, on faisait `var name = 'Gringo';` au tout début de son bloc d'instructions.
4. Chaque instruction de la fonction est exécutée, jusqu'à tomber sur un `return` ou arriver à la fin du bloc.
5. La fonction s'arrête, le fil du code reprend à la suite de l'appel à la fonction. La variable `name` est détruite.

### Fonctions avec plusieurs paramètres 

Une fonction peut accepter plusieurs paramètres, auquel cas les arguments auront une correspondance pair-à-pair (premier argument -> premier paramètre ; second argument -> second paramètre ; etc.)

```js
function addition(a, b) {
  return a + b;
}

// resultat contiendra 12
var resultat = addition(5, 7);
```