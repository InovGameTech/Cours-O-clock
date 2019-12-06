# Les fonctions

On peut utiliser des fonctions, comme `date()` ou `count()`.  
Mais on peut aussi définir nous-même nos propres fonctions. Ça va nous permettre
d'exécuter une série d'instructions. On va pouvoir lui donner un ou des paramètres,
qui sera repris dans le corps de la fonction.

## Définir une fonction

_Définir une fonction_, c'est préparer un ensemble d'instructions à l'avance.  
Ces instructions (entre `{` `}`) ne sont pas exécutées lors de la définition de la fonction.  
Lorsque la fonction sera appelée à un endroit du code, le corps de cette fonction (= les instructions dans la fonction) sera exécutée.  
Si cette même fonction est appelée une seconde fois dans le code, le corps de cette fonction sera à nouveau exécutée.

### Cas simple

Pour définir une fonction, on utilise `function` :

```php
<?php

function hello() {
	// Affiche une string
	echo "Hello World!";
}

```

### Avec des paramètres

Si on souhaite utiliser une fonction en lui fournissant des arguments,
il faut que la définition de la fonction possède des paramètres :

```php
<?php

function hello($name) {
	// Affiche une string
	echo "Hello $name";
}

```

#### Pourquoi utiliser des paramètres ?

Prenons l'exemple du téléphone, et exécutez la fonction `appeler()`.  
Le téléphone ne sait pas quoi faire, car **il ne sait pas qui appeler**.  
Donc, la fonction `appeler()` a besoin d'une information pour s'exécuter correctement.  
Cette information, on va la transmettre comme argument de la fonction : `appeler('Dario Spagnolo');`.  
Pour que la fonction récupère cet argument, elle doit déclarer un paramètre et lui donner un nom : `function appeler($nomDeLaPersonneAAppeler) { /* ... */ }` puis pourra utiliser la variable correspondante dans le corps de la fonction.

### Avec des paramètres optionnels

Si on souhaite utiliser une fonction en lui fournissant des arguments mais
pas forcément tous, il est possible de définir des paramètres optionnels.

Ceux-ci doivent être placés après les paramètres obligatoires (non-optionnels).
Lorsque le paramètre optionnel n'est pas fourni, c'est la valeur par défaut
(placé après le signe `=`) qui sera utilisée.

```php
<?php

function say($message, $name = 'World') {
	// Affiche une string en utilisant un paramètre obligatoire $message
	// et un paramètre optionnel $name
	echo "$message $name";
}

```

### Avec un retour

Dans la définition de notre fonction, on va définir une série d'instructions,
avec ce qu'on veut à l'intérieur. On va pouvoir aussi faire en sorte que cette
fonction "retourne" une valeur, avec `return` :

```php
<?php

function getHello($name) {
	// Retourne une string
	return "Hello $name";
}

```

Cette fois-ci, au lieu d'afficher, on retourne une string, qui pourra être utilisée par la suite.  
Ça sera plus clair quand on va exécuter une fonction :wink:

:warning: un `return` implique la sortie de la fonction => tout code placé après un `return` ne sera jamais exécuté

#### Pourquoi retourner une donnée ?

Prenons comme exemple la fonction `acheterUnEcranIncurveDe49Pouces()`.  
Déjà, pour fonctionner, la fonction a besoin de connaître notre budget => information à transmettre => argument => `acheterUnEcranIncurveDe49Pouces(1000)`.  
Une fois le budget fourni, la fonction fait son taf et achète un écran incurvé de 49" pour 900 €.  
Sauf que la fonction **ne retourne rien** => ne me donne pas mon écran => mais a bien pris 900 € sur mon compte :sob:  
Pour que la fonction me donne mon écran, il faudrait juste ajouter comme dernière instruction `return $ecranAchete;`. Ainsi, j'appelle la fonction, elle fait sa tambouille interne et j'attends l'écran en retour (qui m'est fourni grâce à l'instruction `return`).

## Exécuter une fonction

Une fois définie, on va pouvoir l'utiliser. On appelle ça **exécuter** / **appeler** la fonction.

### Cas simple

```php
<?php

// Je définis ma fonction
function hello() {
	echo "Hello World!";
}

// Je l'exécute
// Affiche : Hello World!
hello();

```

### Avec des paramètres

Si on a défini des paramètres dans la définition de notre fonction, on peut
exécuter notre fonction en lui donnant des "arguments", c'est-à-dire des valeurs
qui vont être prises comme paramètres.

```php
<?php

// Je définis ma fonction, avec le paramètre $name
function hello($name) {
	echo "Hello $name";
}

// J'exécute ma fonction avec l'argument "Rouky"
// Affiche : Hello Rouky
hello("Rouky");

```

Qu'est-ce qu'il se passe ?
1. J'exécute la fonction hello avec un argument `"Rouky"`
2. Ma fonction a été définie avec un paramètre `$name`, qui va stocker l'argument donné.  
C'est comme si avant d'exécuter la fonction, on faisait `$name = "Rouky";`
3. Chaque instruction de la fonction est interpretée

### Avec des paramètres optionnels

Si on définit des paramètres optionnels dans la définition de notre fonction, on peut exécuter notre fonction en lui donnant seulement une partie des "arguments optionnels".  
Si certains arguments ne sont pas fournis, la fonction utilisera la valeur par défaut fournie dans la définition du paramètre correspondant.

:warning: Attention :

- les paramètres non-optionnels doivent obligatoirement être fournis en arguments lors de l'appel de la fonction
- les paramètres optionnels peuvent ne pas être fournis en arguments lors de l'appel de la fonction

#### Exemple d'utilisation d'une fonction avec paramètres optionnels

```php
<?php

// Je définis ma fonction, avec le paramètre obligatoire $time 
// et avec le paramètre optionnel $name
// et je donne au paramètre $name une valeur par défaut 'World' avec le signe '='
function hello($time, $name = 'World') {
	echo "$time Hello $name";
}
```

```php
// J'exécute ma fonction avec les arguments "12:31" "Rouky"
// Affiche : 12:31 Hello Rouky
hello("12:31","Rouky");
```

Qu'est-ce qu'il se passe ?

1. J'exécute la fonction hello avec 2 arguments `"12:31"` et `"Rouky"`
2. Ma fonction a été définie avec 2 paramètres `$time` et `$name`, qui vont prendre la valeur des arguments fournis.  
  C'est comme si avant d'exécuter la fonction, on faisait `$time = "12:31";` et `$name = "Rouky";`
3. Chaque instruction de la fonction est interpretée

#### Autre exemple d'utilisation d'une fonction avec paramètres optionnels

```php
// J'exécute ma fonction avec le 1er argument "12:31" mais
//     sans fournir le 2ème.
// Le paramètre $time reçoit la valeur "12:31"
// Le paramètre $name ne reçoit aucune valeur et prend
//     donc sa valeur par défaut : 'World'
// Affiche : 12:31 Hello World
hello("12:31");

```

Qu'est-ce qu'il se passe ?

1. J'exécute la fonction hello avec un un seul argument `"12:31"`
2. Ma fonction a été définie avec 2 paramètres `$time` et `$name`.  
`$name` étant optionnel et n'étant pas fourni en argument, il prendra donc sa valeur par défaut : `World`.  
C'est comme si avant d'exécuter la fonction, on faisait :
`$time = "12:31";` et `$name = "World";`
3. Chaque instruction de la fonction est interpretée

#### Et si on veut préciser un paramètre optionnel, on doit préciser tous ceux placés avant

Ainsi, si la fonction définit plusieurs paramètres optionnels, seuls les paramètres placés après les paramètres fournis peuvent être omis.

Par exemple :
```php
<?php

// Je définis ma fonction, avec le paramètre optionnel $time (valeur par défaut 12:00)
// et avec le paramètre optionnel $name (valeur par défaut 'World')
function hello($time = "12:00", $name = "World") {
	echo "$time Hello $name";
}

// Je souhaite préciser la valeur du paramètre $name
// alors je dois forcément fournir tous les arguments optionnels placés avant $name
// même si je fournis la même valeur pour $time que sa valeur par défaut
// Affiche : 12:00 Hello Earth
hello("12:00", "Earth");
```

### Avec un retour

Lorsque l'on exécute une fonction définie avec un retour, non seulement les instructions de la fonction seront exécutées, mais ensuite une valeur de retour est envoyée.  
Ce retour peut être utilisée comme toute autre valeur, pour être afficher avec `echo` ou stockée dans une variable par exemple.

```php
<?php

function getHello($name) {
	// On retourne une string
	return "Hello $name";
}

// La variable $phrase contient la valeur "Hello Julie"
$phrase = getHello("Julie");

```

## Autres informations utiles

### :warning: **Attention** : Une fois que l'on utilise `return`, la fonction s'arrête.

```php
<?php

function getHello($name) {
	// On retourne une string, donc la fonction s'arrête
	return "Hello $name";

	// Le PHP n'ira jamais lire cette ligne
	echo "ce message ne sera jamais affiché !"
}

// La variable $phrase contient la valeur "Hello Julie"
$phrase = getHello("Julie");

```

### Dans nos fonctions, on peut avoir plusieurs paramètres ! :smiley:

**C'est l'ordre qui détermine les affectations** entre les arguments et les paramètres.  
2 paramètres, dans l'ordre `$a` et `$b`  
2 argument, dans l'ordre `5` et `7`  
Donc, le paramètre `$a` aura la valeur 5 et `$b` la valeur `7`

```php
<?php

function addition($a, $b) {
	return $a + $b;
}

// addition :
//     calcule 5 + 7
//     retourne 12
// => echo 12;
// Affiche 12
echo addition(5, 7);

```

## Portée des variables

A chaque fois que l'on définit une fonction, on crée une nouvelle **portée de variable**,  
c'est-à-dire qu'un nouveau stock de variable est créé.

``` php
<?php
$fruit = "Kiwi";

// Ici, la variable $fruit existe.
// On est dans la portée principale ("globale")
// ...

function hello($str) {
	// Ici, la variable $fruit n'existe pas.
	// Ici, la variable $str existe, avec la valeur passée en argument
	// cette variable $str est uniquement créée dans la portée de la fonction

	// On peut aussi définir des variables à l'intérieur de la fonction
	// qui elles aussi seront détruites à la fin de la fonction
	// et ne se retrouveront pas dans la portée principale ("globale")
	$name = 'Manu';
	echo $str . ' ' . $name . ' !';
}

// Ici, la variable $fruit existe toujours.
// et la variable $str n'existe pas.
// ...

// A l'intérieur de la fonction, $str vaudra "Bonjour"
// Affiche : Bonjour Manu !
hello('Bonjour');

// Ici, la variable $fruit existe toujours.
// et la variable $str n'existe toujours pas.
// ...

```

On peut utiliser le mot-clé `global` (non recommandé) pour utiliser une variable définie dans la portée principale.

```php
<?php

$fruit = "Kiwi";

function hello($str) {
	// global permet de créer un "pont" entre la portée de la fonction et la portée "globale"
	global $fruit;

	// Ici, la variable $fruit est définie, car on a explicitement
	// demandé avec `global` de récupérer la variable qu'on a créé.
	echo $str . ' ' . $fruit;
}

// Affiche : Bonjour Kiwi
hello('Bonjour');

```

### Analogie

Les fonctions, c'est comme une ~~boite de chocolat~~ boite hermétique (Tupper**** :wink:).

Tout ce qui est dans la fonction n'existe que dans la fonction et n'est pas disponible en dehors.  
Tout ce qui en dehors de la fonction n'existe qu'en dehors de la fonction et n'est pas disponible à l'intérieur.  
Utiliser le mot-clé `global`, c'est comme faire un énorme trou dans sa boite hermétique, qui n'est donc plus hermétique :cry: