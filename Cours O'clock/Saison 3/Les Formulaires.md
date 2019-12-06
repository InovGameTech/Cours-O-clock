# Les formulaires

## HTML

Sur notre `<form>`, on va pouvoir utiliser deux attributs :
- `action` : permet de spécifier le chemin de la page qui doit traiter le formulaire.  
Par défaut, les navigateurs envoient les infos sur la page actuelle.

- `method` : permet de choisir la façon dont on va soumettre les données.  
Par défaut, les navigateurs envoient les infos en GET.

```html
<!-- A la soumission du formulaire, j'envoie en GET à traitement.php -->
<form action="traitement.php" method="GET">
	...
</form>

<!-- A la soumission du formulaire, j'envoie en POST au chemin actuel -->
<form action="" method="POST">
	...
</form>

```

## PHP

Lorsque l'on valide son formulaire, les informations présentes dans les champs
sont envoyés au serveur. PHP peut récupérer ses valeurs grâce aux variables
`$_GET` et `$_POST`.

Les variables commençant par `$_` sont des variables
automatiquement assignées à PHP, nous n'avons pas besoin de les déclarer.
On les appelle des _superglobales_.

Les valeurs sont remplies avec les attributs `name` des champs de formulaires.  
On va pouvoir récupérer la valeur d'un champ avec `$_GET['nom-du-champ']`.


### Cas simple

`index.html` :
```html
<form action="traitement.php" method="GET">
	<!-- On pourra récupérer la valeur de cet input en demande le champ 'age' -->
	<input type="text" name="age" placeholder="Votre âge" />
</form>

```

`traitement.php` :
```php
<?php
// On appelle traitement.php en validant le formulaire
// Donc une variable $_GET est créé, avec le champ 'age'.
echo 'Vous avez ' . $_GET['age'] . ' ans.';

```

### Cas réel

`index.php` :
```php
<!doctype html>
<html>
	<body>
		<?php
			// Si le formulaire a été soumis
			// C'est-à-dire si $_GET['age'] n'est pas vide
			if (!empty($_GET['age'])) {
				// Alors, on affiche l'âge
				echo '<h1>Vous avez ' . $_GET['age'] . ' ans.</h1>';
			}
		?>
		<form action="" method="GET">
			<input type="text" name="age" placeholder="Votre âge" />
		</form>
	</body>
</html>
```

On peut aussi remettre la valeur soumise dans l'input :

`index.php` :
```php
<!doctype html>
<html>
	<body>
		<?php
			// Si le formulaire a été soumis
			// C'est-à-dire si on a une valeur saisie pour l'âge
			// C'est-à-dire si $_GET['age'] n'est pas vide
			if (!empty($_GET['age'])) {
				// Alors, on affiche l'âge
				echo '<h1>Vous avez ' . $_GET['age'] . ' ans.</h1>';
			}
		?>
		<form action="" method="GET">
			<input
				type="text"
				name="age"
				placeholder="Votre âge"
				value="<?php
					// Si on a une valeur saisie
					if (!empty($_GET['age'])) {
						echo $_GET['age'];
					}
				?>"
			/>
		</form>
	</body>
</html>
```

On peut _refactoriser_ notre code, c'est-à-dire le réordonner pour ne pas
se répéter et le rendre plus lisible. Dans ce cas précis, pour ne pas répéter
le test de `$_GET['age']`.

`index.php` :
```php
<?php

// Valeur par défaut
$age = "";

// Est-ce qu'une valeur a été soumise ?
if (!empty($_GET['age'])) {
	$age = $_GET['age'];
}

?><!doctype html>
<html>
	<body>
		<?php
			if ($age) {
				echo "<h1>Vous avez $age ans.</h1>";
			}
		?>
		<form action="" method="GET">
			<input
				type="text"
				name="age"
				placeholder="Votre âge"
				value="<?= $age ?>"
			/>
		</form>
	</body>
</html>
```

Et maintenant, on veut envoyer les données du même formulaire en POST (plus sécurisé car non _public_). Voici donc la version **POST** avec la superglobale `$_POST`.

`index.php` :
```php
<?php

// Valeur par défaut
$age = "";

// Est-ce qu'une valeur a été soumise ?
if (!empty($_POST['age'])) { // ligne modifiée
	$age = $_POST['age']; // ligne modifiée
}

?><!doctype html>
<html>
	<body>
		<?php
			if ($age) {
				echo "<h1>Vous avez $age ans.</h1>";
			}
		?>
		<form action="" method="POST"> <!-- ligne modifiée -->
			<input
				type="text"
				name="age"
				placeholder="Votre âge"
				value="<?= $age ?>"
			/>
		</form>
	</body>
</html>
```