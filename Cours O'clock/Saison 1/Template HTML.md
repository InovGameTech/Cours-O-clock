# Template HTML

Une bonne base de document HTML est primordiale.

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<body>

	</body>
</html>
```


## Raccourci Atom

Dans Atom, si on est dans un fichier .html, il peut être générer avec un raccourci : il suffit de taper « html » puis la touche `tab`.

<kbd>![snippet html](img/snippet-html.gif)</kbd>


## Doctype

Déclare la version de HTML que le document contiendra, le doctype est la première information qui doit être mentionnée dans le document.

Aujourd'hui la norme est le **HTML5**, son doctype s'écrit de la façon suivante

```html
<!DOCTYPE html>
```


## La racine du document ou l'élément `<html>`

Tout le code HTML de la page sera contenu dans cet élément

Il est considéré comme l'élément racine et donc l'ancêtre de tous les autres éléments HTML du document.

```html
<!DOCTYPE html>
<html>
	<!-- Tout le reste du code HTML sera écrit entre ces 2 balises -->
</html>
```


## L'entête du document ou l'élément `<head>`

Toutes les informations annexes aux contenus (méta-données) se trouveront ici, le titre du document HTML, ses auteurs, des références aux styles graphiques, etc...

Cette partie ne doit pas être enrichie de contenus visuels ou textuels.

```html
<!DOCTYPE html>
<head>
	<!-- Jeu de caractères employé pour afficher le texte -->
	<meta charset="utf-8">

	<!-- Titre du document affiché dans l'onglet du navigateur -->
	<title>Titre</title>
</head>
```

### Si on omet l'UTF-8

On s'expose à des soucis d'encodage des accents !

![](img/martine-ecrit-en-utf-8.jpg)

## Le corps du document ou l'élément `<body>`

Contrairement à l'entête, tout ce que se trouvera dans cette partie sera visible dans le navigateur. C'est la zone pour tous les contenus.

```html
<body>
	<!-- L'ensemble des contenus iront entre ces 2 balises-->
</body>
```