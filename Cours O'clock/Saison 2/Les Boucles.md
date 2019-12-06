# Les boucles

Souvent dans nos programmes, on va vouloir exécuter une même série d'instructions plusieurs fois.
Par exemple, pour écrire tous les `<option>` d'un `<select>`. Sans PHP, il fallait faire chauffer le copier-coller !

> NOTE : Les boucles font partie des **structures de contrôle** qu'offre PHP, [voir le site de PHP](http://php.net/manual/en/language.control-structures.php).

## For

Avec une boucle for, [comme dit la princesse](https://www.youtube.com/watch?v=pK8L0BdnReA&feature=youtu.be&t=2m4s),
on va pouvoir exécuter une même série d'instructions, en incrémentant la variable à chaque itération !

Pas très parlant, alors prenons des exemples.

### Cas simple

```php
<?php

for ($heure = 0; $heure < 24; $heure++) {
	echo 'Il est ' . $heure . 'h.';
	echo "<br />";
}

/*
	Cela affiche :
	Il est 0h.
	Il est 1h.
	Il est 2h.
	Il est 3h.
	Il est 4h.
	Il est 5h.
	Il est 6h.
	Il est 7h.
	Il est 8h.
	Il est 9h.
	Il est 10h.
	Il est 11h.
	Il est 12h.
	Il est 13h.
	Il est 14h.
	Il est 15h.
	Il est 16h.
	Il est 17h.
	Il est 18h.
	Il est 19h.
	Il est 20h.
	Il est 21h.
	Il est 22h.
	Il est 23h.
*/

```

Si on décortique les 3 instructions dans la parenthèse du for,
on peut voir qu'en fait, on fait :  
`for (initialisation; condition; incrementation)`.

```php
<?php

for (
	// Première instruction de la parenthèse, on définit l'action à faire avant la boucle
	// Ici, on initialise une variable heure à 0
	$heure = 0;

	// Deuxième instruction de la parenthèse, on définit la condition à tester pour continuer la boucle
	// Ici, on teste que $heure est inférieur à 24
	$heure < 24;

	// Troisième instruction de la parenthèse, on définit l'action à faire à chaque fois
	// 99% du temps ici, on va incrémenter la variable
	// Et surtout, il faut une action qui permettre à la condition de devenir fausse, sinon, boucle infinie !
	// Ici, on incrémente $heure
	$heure++
) {
	echo 'Il est ' . $heure . 'h.';
	echo "<br />";
}

```

A l'intérieur du `for`, on peut y mettre ce qu'on veut. Des `if` par exemple,
mais aussi une autre boucle `for` ! :smile:

### Cas réel : avec un tableau


```php
<?php

// Mon tableau à parcourir
$fruits = ["cerise", "banane", "kiwi"];

// Le nombre d'élément que j'ai
$nbFruits = 3;

// Je vais de 0 à 2, pour afficher $fruits[0], $fruits[1] et $fruits[2]
for ($index = 0; $index < $nbFruits; $index++) {
	echo $fruits[$index];
}

```

Avec `count()`, on peut connaître le nombre d'éléments du tableau, plutôt qu'avoir
à noter "en dur" le nombre d'éléments du tableau dans le code :

```php
<?php

// Mon tableau à parcourir
$fruits = ["cerise", "banane", "kiwi"];

// Le nombre d'élément que j'ai
$nbFruits = count($fruits);

// Je vais de 0 à 2, pour afficher $fruits[0], $fruits[1] et $fruits[2]
for ($index = 0; $index < $nbFruits; $index++) {
	echo $fruits[$index];
}

```

Puisque la première instruction du for, on l'utilise pour la définition des variables
utiles à notre boucle, on peut mettre le count directement dedans :

```php
<?php
$fruits = ["cerise", "banane", "kiwi"];

for ($index = 0, $nbFruits = count($fruits); $index < $nbFruits; $index++) {
	echo $fruits[$index];
}

```


## While

Avec `while`, on va aussi pouvoir faire une boucle. Mais plutôt que d'aller
de 0 à 10 par exemple, on va simplement définir une condition :

```php
<?php

// Mes économies
$savings = 0;

// Tant que je n'ai pas assez économisé
while ($savings < 100) {
	// Alors je travaille pour gagner quelques pièces
	$savings += 10;
}

// On sort de la boucle uniquement quand $savings est supérieur à 100
echo "Je suis riche !";

```

## Foreach

Encore mieux pour parcourir des tableaux, `foreach` :

```php
<?php
$fruits = ["cerise", "banane", "kiwi"];

foreach ($fruits as $fruit) {
	echo $fruit;
}

```

Plus besoin de se casser la tête avec des index !  
Ça marche aussi avec des tableaux associatifs :

```php
<?php
$fruits = [
	"superbon" => "cerise",
	"sucre" => "banane",
	"acide" => "kiwi"
];

/*
	Affiche :
	cerise, c'est superbon !banane, c'est sucre !kiwi, c'est acide !
*/
foreach ($fruits as $key => $fruit) {
	echo "$fruit, c'est $key !";
}

```

![schéma foreach](http://www.splessons.com/wp-content/uploads/2015/06/php-foreach-loop.jpg)

## Syntaxe alternative

On peut utiliser une syntaxe alternative pour les boucles, notamment lorsque
l'on souhaite mixer PHP et HTML :

```php
<?php

foreach($fruits as $key => $fruit):
?>
	<p>
		<strong><?= $fruit ?><strong>, c'est <?= $key ?> !
	</p>
<?php
endforeach;

```