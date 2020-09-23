# Structrure et sémantique

Chaque élément HTML a un rôle précis, structuration ou organisation de page, délimitation du contenu, enrichissement sémantique. L'idée est de choisir chaque élément HTML avec soin afin de rendre cohérent la formulation du contenu avec la structure dans laquelle il sera placé.

L'objectif n'est pas de **TOUT** spécifier mais de structurer intéligemment le document pour qu'il reflète la teneur du contenu.

## Trouver chaussure à son pied

Pour utiliser les éléments HTML à bon escient il est nécessaire de bien découpé le contenu. 
Par exemple, sur une page de blog, 
- dans le `<body>`, un `<header>` contiendra le logo du blog et probablement un `<nav>` avec les autres pages du site
- le contenu principal sera à placer dans un élément `<article>`
- `<address>` contiendra les information de l'auteur de cet article
- `<hgroup>` regroupant le titre `<h1>` de l'article et un le chapeau `<h2>`
- plusieurs paragraphes `<p>` et titres `<h2>` et `<h3>` agrémentés de `<strong>` et d'`<em>` pour insister sur certaines notions importantes
- quelques `<blockquotes>` pour les citations d'autres auteurs cités dans l'article
- une zone `<aside>` avec des liens vers de précedents articles
- un `<footer>` avec des mentions légales et un formulaire pour une newsletter

Ce [référentiel](https://developer.mozilla.org/fr/docs/Web/HTML/Element) fourni l'ensemble des éléments HTML et leur valeur sémantique

## Sémantique, oui, mais pas que !

Quand du contenu n'a pas vocation à apporter de plus-values sémantique, par exemple pour de la présentation, il est bon d'utiliser des éléments cohérents.

- `<div>` type `block`
- `<span>` type `inline`

sont 2 éléments à connaître. En [CSS](../css/syntaxe.md) il sera facile d'ajouter du style.

## Les plus utilisés

Le [référentiel](https://developer.mozilla.org/fr/docs/Web/HTML/Element) MDN est très complet, seule un partie de ces éléments reviennent systématiquement

**Structure**
- `<header>`
- `<footer>`
- `<h1>`...`<h3>`
- `<nav>`
- `<section>`
- `<article>`

**Texte**
- `<p>`
- `<ul>`
- `<ol>`
- `<li>`
- `<blockquote>`

**En ligne**
- `<a>`
- `<strong>`
- `<em>`
- `<small>`
- `<q>`