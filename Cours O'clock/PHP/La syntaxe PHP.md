# La syntaxe PHP

## Création d'un fichier

Pour que tout se passe bien :
- Il faut se positionner à la racine du serveur web. Sur le téléporteur, c'est `/var/www/html`.
- Il faut créer un fichier avec l'extension `.php`.
- On vient placer le code PHP entre les balises `<?php` et `?>`.
- Si un fichier contient exclusivement du PHP, on peut omettre `?>`.

## Commentaires

Avant de commencer à écrire des instructions, on va pouvoir faire des commentaires,
comme en HTML et en CSS, pour donner des indications uniquement destinées au
développeur.

Il y a deux types de commentaires :
- Sur une ligne, avec `//` : tout ce qu'il y a à droite sera ignoré.
- Sur plusieurs lignes, avec `/*` et `*/`, comme en CSS.

```php
<?php
// Ceci est un commentaire sur une ligne

/*
	Et ça, c'est un commentaire
	sur plusieurs lignes
*/

```


## Première instruction

- On ouvre le php avec `<?php`.
- On utilise `echo`, une fonction de php permettant d'afficher du texte
- On écrit le message à afficher entre guillemets : `"Hello, World!"`.
- On termine notre instruction par `;`. Cela permet de délimiter chaque instruction, comme en CSS.

```php
<?php
// Affiche : Hello, World!
echo "Hello, World!";

```

## Variables

Là aussi présent dans tous les langages de programmation, les variables. Cela permet de retenir une
valeur en mémoire. En PHP, les variables sont préfixées d'un `$`.

### Affectation de variables

Ici, on stocke la string `"Lucie"` dans la variable `$prenom` :

```php
<?php
$prenom = "Lucie";

```

On appelle ça "affectation de variable" ou "assignation de variable".
Ensuite, on pourra par exemple utiliser `echo` pour afficher notre variable :

```php
<?php
$prenom = "Lucie";

// Affiche : Lucie
echo $prenom;

```

### Inspecter une variable

Pour voir ce qu'il y a dans une variable, on peut utiliser la fonction `var_dump`.

```php
<?php
$age = 32;
$prenom = "Lucie";

/* Affiche le type de donnée et le contenu */
// String(5) Lucie = une string de 5 caractères de long, "Lucie"
var_dump($prenom);

// Int(32) = un nombre entier, 32
var_dump($age);

```


## Types de données

Le PHP, comme la plupart des langages de programmation, possède plusieurs types de données.

### Scalaire (contient une seule valeur)

- String (chaîne de caractère). On écrit une string en entourant le message par des guillemets : `"` ou `'`.  
Exemple : `"Hello, World!"`

- Int (nombre entier).  
Exemple : `12`

- Float (nombre à virgule).  
Exemple : `120.75`.  
_Attention, `.` et non `,`, comme en CSS._

- Boolean (booléen).  
Deux valeurs possibles : `true` ou `false`, pour vrai ou faux.

### Constante

Une constante est un identifiant qui représente une valeur simple. Comme son nom le suggère, cette valeur ne peut jamais être modifiée durant l'exécution du script. Le nom d'une constante est sensible à la casse. Par convention, les constantes sont toujours en majuscules.

```php
<?php
// Définition dune constante
define("AGE_MINI", 7);
define("AGE_MAXI", 77);
define("SITE_TITLE", "Mon super titre de site");

// Usage
echo '<title>'.SITE_TITLE.'</title>';
```

### Composé (plusieurs valeurs scalaires)

#### Tableau simple (array)

Pour stocker plusieurs infos dans une même variable.  
Exemple : `["cerise", "banane", "kiwi"]`  
Exemple : `array("cerise", "banane", "kiwi")` (ancienne écriture)  

On accède au rang x en faisant `$mon_tableau[x]`. Par exemple :

```php
<?php

$fruits = ["cerise", "banane", "kiwi"];

// Affiche : cerise
echo $fruits[0];

// Affiche : banane
echo $fruits[1];

// Affiche : kiwi
echo $fruits[2];

```

On va même pouvoir rajouter des éléments à notre tableau :

```php
<?php

$fruits = ["cerise", "banane", "kiwi"];

// On rajoute "framboise" à la fin du tableau $fruits
$fruits[] = "framboise";

```

#### Tableaux associatifs

On peut aussi avoir des tableaux associatifs, c'est-à-dire qu'on va donner
nous même les index du tableaux.

```php
<?php

// Ce tableau…
$fruits = ["cerise", "banane", "kiwi"];

// …peut aussi être écrit comme ça
$fruits = [
	0 => "cerise",
	1 => "banane",
	2 => "kiwi"
];

// Mais on peut aussi donner nous même des index
$fruits = [
	"superbon" => "cerise",
	"sucre" => "banane",
	"acide" => "kiwi"
];

// Et dans ce cas, on va accéder aux valeurs en utilisant les clés qu'on a donné :
// Affiche : cerise
echo $fruits["superbon"];

```

Là aussi, on va même pouvoir rajouter des éléments à notre tableau :

```php
<?php

$fruits = [
	"superbon" => "cerise",
	"sucre" => "banane",
	"acide" => "kiwi"
];

// On rajoute à la clé "délicieux", la valeur "framboise"
$fruits["delicieux"] = "framboise";

// On peut aussi écraser un élément existant
$fruits["acide"] = "citron";

```

## Opérations

### Arithmétique

Sur les nombres, on va pouvoir faire les opérations arithmétique de base : `+`, `-`, `*`, `/`.

```php
<?php
// Affiche 8
echo 4 + 4;

// Affiche 0
echo 4 - 4;

// Affiche 16
echo 4 * 4;

// Affiche 1
echo 4 / 4;

```

### Concaténation

Concernant les string, on va pouvoir "additionner" deux chaînes de caractères,
c'est-à-dire les "coller". On appelle ça la _concaténation_, que l'on réalise
avec `.`.

```php
<?php
$prenom = 'Christelle';
echo 'Bonjour ' . $prenom . ' !';

```

Si on utilise les doubles-quotes `"` plutôt que les simples-quotes `'`,
on peut afficher le contenu d'une variables. On peut donc écrire le code
précédant comme ça :

```php
<?php
$prenom = 'Christelle';

// Affiche : Bonjour $prenom !
echo 'Bonjour $prenom !';

// Affiche : Bonjour Christelle !
echo "Bonjour $prenom !";

```

### Echappement

Parfois, on a envie d'afficher `"` ou `'`, alors justement qu'on utilise ces
caractères pour créer une string en PHP. Par exemple, quand on écrit du HTML.

Chaque fois qu'on va vouloir utiliser un caractère déjà utilisé par PHP,
on va pouvoir utiliser `\`. On peut aussi utiliser des `"` lorsqu'on a besoin de `'`
et inversement.

```php
<?php
// Je veux afficher des ', alors j'utilise des " pour créer ma string
// Affiche : Il m'a dit que j'étais balèze !
echo "Il m'a dit que j'étais balèze !";

// Je veux afficher des ", alors j'utilise des ' pour créer ma string
// Affiche : Je suis "balèze" !
echo 'Je suis "balèze" !';

// Je veux les deux ! Pas le choix, je dois échapper.
// Affiche : Il m'a dit que j'étais "balèze" !
echo "Il m'a dit que j'étais \"balèze\" !";

// On aurait pu échapper les '
echo 'Il m\'a dit que j\'étais "balèze" !';

```

### Raccourcis

La syntaxe PHP permet quelques raccourcis pour venir modifier une variable.

#### Incrémentation

Souvent, on va vouloir _incrémenter_ une variable, c'est-à-dire augmenter sa valeur de 1.
Par exemple, si on fait un compteur.

Pour cela, on peut utiliser la notation `$compteur++`.  
Cela équivaut à `$compteur = $compteur + 1`.

```php
<?php

// J'ai 500 euro dans ma tirelire
$savings = 500;

// Tous les jours, j'ajoute un euro
$savings++;

// Affiche : 501
echo $savings;

```

On peut aussi _décrémenter_, c'est-à-dire diminuer la valeur de 1, avec `$compteur--`.  
Cela équivaut à `$compteur = $compteur - 1`.

```php
<?php

$fruits_restants = 10;

// J'ai faim, je prends un fruit
$fruits_restants--;

// Affiche : 9
echo $fruits_restants;

```

#### Opérateurs combinés

OK, augmenter de 1 ou diminuer de 1, ça sera très souvent pratique,
on le verra avec les boucles par exemple. Mais on est aussi souvent amenés
à faire des opérations sur une même variable, en dehors de +1 ou -1.

On peut utiliser la notation : `$variable += 1;`.

```php
<?php

// On a 2000€ d'économie de côté
$phrase = "J'ai économisé ";
$savings = 2000;

// Loyer : 800€
$savings -= 800;

// Salaire : 1500€
$savings += 1500;

// Intérêts de la banque à 0,75%
$savings *= 1.0075;

// Je fais du shopping, je crame la moitié de mes économies
$savings /= 2;

// Je concatène $savings à la fin de $phrase
$phrase .= $savings;

```

## Un peu de HTML avec ça ?

### Du HTML dans le PHP

Ce qui est affiché par PHP sera interprêté par le navigateur, comme si on avait
fait un fichier `.html` :

```php
<?php
echo "<h1>Ma page en PHP</h1>";

```

### Du PHP dans le HTML


Si on ferme le PHP avec `?>`, tout ce qui se retrouve à l'extérieur du PHP sera
affiché tel quel. On peut donc s'en servir lorsque l'on veut afficher beaucoup
de contenu statique.

```php
<?php
// On définit une variable, mais on n'affiche rien
$titre = "Ma page en PHP";

// Ensuite, on fermant PHP, tout ce qui suit sera affiché
?><!doctype html>
<html>
	<body>
		<!--
			Pour éxécuter à nouveau du PHP,
			par exemple pour afficher une variable,
			on peut rouvrir PHP
		-->
		<h1><?php echo $titre; ?></h1>
	</body>
</html>
```

On peut aussi utiliser le raccourci `<?=` lorsque l'on souhaite ouvrir et fermer
PHP juste pour faire un `echo` :


```php
<?php
// On définit une variable, mais on n'affiche rien
$titre = "Ma page en PHP";

// Ensuite, on fermant PHP, tout ce qui suit sera affiché
?><!doctype html>
<html>
	<body>
		<!--
			Pour éxécuter à nouveau du PHP,
			par exemple pour afficher une variable,
			on peut rouvrir PHP
		-->
		<h1><?= $titre; ?></h1>
	</body>
</html>
```