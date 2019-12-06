# Les conditions

On va pouvoir exécuter des actions en fonction d'une condition.
Pour cela, on va utiliser le mot-clé `if`, qui permet de réaliser un test.

> NOTE : Le mot-clé `if` fait partie des **structures de contrôle** qu'offre PHP, [voir le site de PHP](http://php.net/manual/en/language.control-structures.php).

## Cas simple : un booléen

```php
<?php
$condition = true;

// true : on "entre" dans le if
// La PHP va donc afficher : Bonjour
if ($condition) {
	echo "Bonjour !";
}

```

```php
<?php
$condition = false;

// false : on "entre" pas dans le if
// Donc le PHP n'affiche rien
if ($condition) {
	echo "Bonjour !";
}

```

## Cas réel : les comparaisons

Utiliser un booléean directement, et donc faire un `if (true)`,
ce n'est pas très intéressant. On va pouvoir réaliser des comparaisons,
qui vont renvoyer `true` ou `false`.

### Les opérateurs de comparaison

- `<` : inférieur à  
Exemple : `10 < 20` renvoie `true`

- `>` : supérieur à  
Exemple : `40.5 > 50` renvoie `false`
_Attention : `40 > 40` renvoie `false` !_

- `<=` : inférieur ou égal à  
Exemple : `142 <= 31` renvoie `false`

- `>=` : supérieur ou égal à  
Exemple : `40 >= 35` renvoie `true`
_Cette fois-ci : `40 >= 40` renvoie `true` !_

- `==` : égal à  
Exemple : `40 == 39.999` renvoie `false`

- `!=` : différent de  
Exemple : `40 != 39.999` renvoie `true`

- `!` : "not", c'est-à-dire, l'inverse  
Exemple : `!true` renvoie `false`  
Exemple : `!(20 < 10)` renvoie `true`  

### Réaliser des comparaisons

OK, on sait faire des tests avec `if`, et on sait faire des comparaisons.
Les deux ensemble, voilà ce que ça donne :

```php
<?php

// On stocke dans une variable la valeur 21
$age = 21;

// 21 supérieur ou égal à 18 ? True.
$condition = $age >= 18;

// True = on entre pas dans le if
if ($condition) {
    echo "Vous êtes majeur";
}

```

Plus simplement, on pourra mettre notre comparaison directement dans les parenthèses de notre if.
On peut aussi définir un bloc `else`, qui va être appelé quand la condition est fausse.

```php
<?php

$age = 21;

// Supérieur ou égal à 18 ?
if ($age >= 18) {
    echo "Vous êtes majeur";
}
else {
    echo "Vous êtes mineur";
}

```

Avec `elseif`, on va même pouvoir définir plusieurs cas possibles :


```php
<?php

$age = 16;

// Ai-je 17 ans ou + ?
if ($age >= 17) {
    echo "Tu peux passer le permis";
}
// J'ai moins de 17 ans. Mais ai-je 15 ans ou + ?
elseif ($age >= 15) {
    echo "Tu peux passer le permis en conduite accompagnée";
}
// J'ai moins de 15 ans.
else {
    echo "Bon, bah tu prends le bus.";
}

```

## Cas complexe : tests multiples

Dans certains cas, on peut se retrouver à vouloir faire un test complexe.
On va alors pouvoir faire utiliser des opérateurs logiques.

### OR

Par exemple, si je fais un test sur des fruits que j'aime :

```php
<?php

$fruits = 'bananes';
if ($fruits == 'oranges') {
	echo "J'aime les $fruits.";
}
else {
	echo "Ah non, les $fruits, je n'aime pas ça !";
}

```

Mais si j'aime plusieurs fruits ? Je peux utiliser `||` :

```php
<?php

$fruits = 'bananes';
if ($fruits == 'oranges' || $fruits == 'bananes') {
	echo "J'aime les $fruits.";
}
else {
	echo "Ah non, les $fruits, je n'aime pas ça !";
}

```

`||`, que l'on peut aussi écrire `OR`, signifie **ou**.  
Dans le cas présent : si `$fruits` est égal à `oranges` **ou** si `$fruits` est égal à `bananes`.

En fait, c'est un opérateur qui va tester ce qu'il y a à gauche, et qui renvoie `true`
si ce premier test est `true`. Si ce premier test est `false`, alors on va tester
le test de droite pour voir si lui ne serait pas `true`.

```php
<?php
// Renvoie false
false || false;

// Renvoie true
true || false;

// Renvoie true
false || true;

// Renvoie true
true || true;

```

### AND

OK, super, on sait dire "si ça c'est vrai ou si ça c'est vrai".  
Mais on peut vouloir non pas l'un des deux, mais vouloir que les deux soient vrais.
Pour cela, on va pouvoir utiliser `&&`.

```php
<?php

$money = 20;
$hasInternet = true;

// J'ai assez d'argent et Internet, je peux m'abonner !
if ($money > 10 && $hasInternet) {
	echo "Je m'abonne à Netflix.";
}
// Si je n'ai pas d'argent ou si je n'ai pas Internet, je ne peux pas m'abonner
else {
	echo "Je regarde M6 :/";
}

```

`&&`, que l'on peut aussi écrire `AND`, signifie **et**.

Cette fois-ci, cet opérateur va s'assurer que le test de gauche soit `true`, et si oui,
il regarde si le test de droite aussi est `true`, dans ce cas il renvoie `true`,
sinon, il renvoie `false`.

```php
<?php
// Renvoie false
false && false;

// Renvoie false
true && false;

// Renvoie false
false && true;

// Renvoie true
true && true;

```


## Quelques fonctions utiles

- [`empty`](http://php.net/manual/fr/function.empty.php) : vérifie si la valeur est vide ou indéfinie.

```php
<?php
if (empty($_GET['age']) {
    echo "attention, vous n'avez pas renseigné votre âge !";
}

```

- [`isset`](http://php.net/manual/fr/function.isset.php) : vérifie si la variable est définie.

```php
<?php
if (!isset($uneVariableQuiNexistePas)) {
    echo "Cette variable n'existe pas.";
}

```

## L'opérateur ternaire

On se retrouve souvent à définir une variable en fonction d'un test.  
Par exemple :

```php
<?php

// Il est quelle heure ?
$heure = date('H');

// S'il est moins de 20h, je suis en forme, sinon je suis fatigué
if ($heure < 20) {
	$etat = 'en forme';
}
else {
	$etat = 'fatigué';
}

// On affiche
echo "Je suis $etat.";

```

On va pouvoir utiliser _l'opérateur ternaire_, qui va s'écrire de cette façon :  
`condition ? valeur si vrai : valeur si faux`

```php
<?php

// Il est quelle heure ?
$heure = date('H');

// S'il est moins de 20h, je suis en forme, sinon je suis fatigué
$etat = $heure < 20 ? 'en forme' : 'fatigué';

// On affiche
echo "Je suis $etat.";

```

## Syntaxe alternative

On peut utiliser une syntaxe alternative pour les conditions, notamment lorsque
l'on souhaite mixer PHP et HTML :

```php
<?php

if ($heure > 7 && $heure < 19):
?>
	<p>
		Il est <strong><?= $heure ?>h</strong>, il fait jour :)
	</p>
<?php
else:
?>
	<p>
		On ne voit rien, il est<strong><?= $heure ?>h</strong> donc il fait nuit :(
	</p>
<?php
endif;

```