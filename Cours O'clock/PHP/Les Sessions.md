# Les sessions

Les **sessions** vont nous permettre d'associer des données à un visiteur,
et d'y accéder dans nos scripts.

## Principe de fonctionnement

![](img/schema-sessions-php.png)

## Activer les sessions

Avant d'utiliser quoi que ce soit, il faut activer les sessions en utilisant
la fonction `session_start`.

```php
<?php
session_start();
```
> Afin d'éviter des conflits en cas de session déjà ouverte, on s'assurera que `session_id()` est bien vide, via `empty(session_id())` ou équivalent, une session non démarrée entrainant `session_id = ""` (chaine vide).

## Utiliser les sessions

Après avoir exécuté la fonction `session_start`, on a accès à la superglobale `$_SESSION`,
un tableau dans lequel on va pouvoir stocker puis accéder à des informations.

```php
<?php
session_start();

// On ajoute un champ à notre tableau
$_SESSION["name"] = "Philippe";

```

Plus tard, sur une autre page, on pourra récupérer l'info :

```php
<?php
session_start();

// Affiche : Philippe
echo $_SESSION["name"];

```

## Supprimer la session

On peut supprimer les données stockées dans `$_SESSION` avec la fonction
`session_unset`.

```php
<?php

// Ici, $_SESSION n'est pas définie.

// On active les sessions, la variable $_SESSION est créée,
// avec toutes les données précédemment stockées sur d'autres scripts
session_start();

// Ici, $_SESSION est définie.

// On supprime les données stockées. Si on rafraichit la page, $_SESSION sera vide.
session_unset();

```

## Chrome DevTools

Dans l'onglet "Applications" du panneau pour développeur de Chrome
(inspecteur d'éléments), on peut voir les cookies stockés pour chaque
domaine.