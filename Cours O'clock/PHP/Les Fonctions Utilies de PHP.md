# Les fonctions utiles de PHP

## PHP.net

Pour découvrir les fonctions de PHP, on peut aller sur le [site officiel de PHP](http://www.php.net/),
qui comporte une documentation très complète avec des explications détaillées,
et des exemples de code fournis. C'est d'ailleurs l'une des forces de PHP !

Chaque page des fonction PHP est bien référencée sur Google, on peut donc
taper le nom de la fonction et tomber directement sur le manuel de la fonction
en question.

Cette page va décrire la **signature** de la fonction, c'est-à-dire comment
elle doit s'exécuter, avec quel(s) paramètre(s) et ce qu'elle retourne.

Exemple :
```
string number_format ( float $number [, int $decimals = 0 ] )
```

La fonction [`number_format`](http://php.net/manual/fr/function.number-format.php)
prend deux paramètres. Le premier doit être de type `float`, et le deuxième de type `int`.
Le deuxième est noté entre crochets pour signifier qu'il est facultatif. On a aussi
`= 0` pour signifier sa valeur par défaut si on omet ce paramètre.

Certains fonctions peuvent avoir plusieurs signatures (c'est le cas de `number_format`),
d'autres fonctions peuvent avoir plus d'explications sur leur paramètre comme la
fonction [`date`](http://php.net/manual/fr/function.date.php).


## Organisation de code

- [`include`](http://php.net/manual/fr/function.include.php) : importe un fichier.

```php
<?php
// Inclue le fichier header.php
include "header.php";

echo "Bonjour !";

// Inclue le fichier footer.php
include "footer.php";

```

- [`require`](http://php.net/manual/fr/function.require.php) : importe un fichier, et génère une erreur fatale si le fichier n'a pas été importé.

```php
<?php
// Inclue le fichier functions.php, et génère une erreur si le fichier n'existe pas
require "php/functions.php";

echo "Bonjour !";

```

- Il existe aussi les fonction `include_once` et `require_once` qui font la même chose,
avec un petit détail bien sympathique : ces deux fonctions vont s'assurer que le fichier n'a
pas déjà été inclus. Quand on a une base de code complexe, ça peut nous être utile !

_A savoir : ces 4 fonctions peuvent s'utiliser avec ou sans parenthèses, comme `echo`._


## Manipulation de chaînes

- [`date`](http://php.net/manual/fr/function.date.php) : retourne la date selon un format.

```php
<?php
$today = date('j/m/Y');

// Si on est le 2 mars 2017, ça affiche : 02/03/2017
echo $today;

```

- [`strlen`](http://php.net/manual/fr/function.strlen.php) : retourne la longueur d'une string.

```php
<?php
$chaine = "Hello, I'm a PHP developer.";

// Affiche : 27
echo strlen($chaine);

```

- [`number_format`](http://php.net/manual/fr/function.number-format.php) : pour formater un nombre.  
Exemple : Pour transformer `1990` en `"1 990,00"`. Utile pour des prix d'une boutique par exemple.

```php
<?php
$price = 15;
$price_format = number_format($price, 2, ',', ' ');

// Affiche : 15,00
echo $price_format;

```

## Tableaux

- [`count`](http://php.net/manual/fr/function.count.php) : retourne la longueur d'un tableau.

```php
<?php
$fruits = ["kiwi", "kaki"];

// Affiche : 2
echo count($fruits);

```

## Mail

- [`mail`](http://php.net/manual/fr/function.mail.php) : envoie un e-mail.

```php
<?php

$to = 'adrien@monemail.com';
$subject = 'Hello Adrien !';
$message = "Hey Adrien, je t'envoie un mail avec PHP !";

mail($to, $subject, $message);

```

- [`filter_var`](http://php.net/manual/fr/function.filter-var.php) : filtre une variable.  
Si la condition n'est pas respectée, la fonction renvoie `false`.

Par exemple, on peut filtrer une adresse e-mail :

```php
<?php

$email1 = 'adrien@monemail.com';
$email2 = 'mouhahahah, je ne suis pas un email';

// Affiche : email1 is OK
if (filter_var($email1, FILTER_VALIDATE_EMAIL)) {
	echo "email1 is OK";
}
else {
	echo "email1 is KO";
}

// Affiche : email2 is KO
if (filter_var($email2, FILTER_VALIDATE_EMAIL)) {
	echo "email2 is OK";
}
else {
	echo "email2 is KO";
}

```

## Serveur

- [`header`](http://php.net/manual/fr/function.header.php) : permet d'envoyer une en-tête HTTP.  
Exemples : faire une redirection, envoyer un code 404, etc.

```php
<?php

// On redirige vers https://oclock.io
header('Location: https://oclock.io/');

// Le script PHP continue quand même après un `header`
// On place donc souvent un `exit` pour arrêter le script.
exit;

```