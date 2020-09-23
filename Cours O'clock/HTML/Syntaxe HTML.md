# La syntaxe HTML

HTML signifie **H**yper**T**ext **M**arkup **L**anguage ou Langage de balises pour l'Hypertexte

Il sert à structurer le contenu, il représente le **fond**

Le HTML s'écrit dans un fichier possédant l'extension `.html`

---

## Commentaires

Pour écrire des commentaires au sein d'un code HTML il faudra utiliser une syntaxe particulière commençant par `<!--` et finissant par `-->`

```html
<!-- Je suis un commentaire -->

<!-- 
  Un commentaire peut être écrit
  sur plusieurs lignes
 -->
```

---

## Balises ou balise ?

**Un exemple d'élément HTML**

```html
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
```

Composé le plus souvent de 2 balises, ici pour notre élément de paragraphe

- balise ouvrante `<p>`
- balise fermante `</p>`

Le contenu de l'élément se trouve entre ces 2 balises

```html
<p>Phrase très courte</p> <!-- Paragraphe de texte -->
<strong>Notion importante</strong> <!-- Notion importante dans le texte -->
...
```

Certains éléments HTML, n'ayant pas vocation à contenir du texte ou d'autres éléments, s'écrivent avec une balise dite autofermante

```html
<br> <!-- Saut de ligne -->
<hr> <!-- Ligne de séparation horizontale -->
...
```

La liste exhaustive des [éléments HTML](https://developer.mozilla.org/fr/docs/Web/HTML/Element) sur Mozilla Developer Network

---

## Attributs

Les attributs viennent compléter un élément HTML avec des informations supplémentaires

Par exemple un lien, aura besoin d'un contenu mais également d'une adresse de destination

```html
<a href="https://github.com">Un lien vers GitHub</a>
```

Pour un lien, l'adresse de destination sera exprimée avec l'attribut `href`

Il existe un cetain nombre d'attributs universels comme 

- `class` permet d'ajouter une liste de classes utilisable en CSS ou en JavaScript
- `id` permet d'indiquer un identifiant unique qui peut être ciblé par un lien, du CSS ou du JavaScript
- `title` permet d'ajouter un texte descriptif du contenu souvent représenté par une bulle flottante
- etc ... 

La liste exhaustive des [attributs universels](https://developer.mozilla.org/fr/docs/Web/HTML/Attributs_universels) sur Mozilla Developer Network

Un certain nombre d'éléments HTML possède des attributs spécifiques, le plus simple est de se référer aux pages spécifiques des différents [éléménts HTML](https://developer.mozilla.org/fr/docs/Web/HTML/Element) éxistant.

---

## Un peu d'espace que diable !

Le navigateur interprète le code HTML et livre le résultat de cette interprétation. `<p>Mon contenu</p>` dans la source HTML sera interprété puis affiché comme ceci `Mon contenu`.

Lors de son interprétation, le navigateur ignore également un certain nombre de chose comme les sauts de lignes, les tabulations ou les espaces répétés

```html
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
```

```html
<p>
  Lorem ipsum 
  dolor 
  
  sit amet, 
  
  consectetur     adipiscing 
  
            elit.
</p>
```

Les 2 codes ci-dessus donneront le même résultat

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

---

## Indentation

Sachant que les tabulations, les espaces répétés ou les sauts de lignes ne sont pas interprétés, il convient de strucutrer la source HTML afin de la rendre plus lisible et plus simple à maintenir.

```html
<article><p>Lorem ipsum dolor <strong>sit amet</strong>, consectetur adipiscing elit.</p></article>
```

```html
<article>
  <p>
    Lorem ipsum dolor <strong>sit amet</strong>, 
    consectetur adipiscing elit.
  </p>
</article>
```

En comparaison, les extraits ci-dessus sont équivalents en terme de HTML par contre au niveau de la lisibilité...

---

## La famille c'est important !

![Poupées russes](https://upload.wikimedia.org/wikipedia/commons/thumb/7/7f/Floral_matryoshka_set_1.JPG/300px-Floral_matryoshka_set_1.JPG)

Le HTML est par nature voué à être structuré par encapsulation ou par imbrication.

`<body>` contient `<article>` qui contient `<h1>` qui contient un titre et `<p>` un paragraphe de texte.

```html
<body>
  <article>
    <h1>
      Lorem ipsum
    </h1>
    <p>
      Vivamus vel vestibulum mauris.
      Nam sed est a orci iaculis mattis eu non ante. 
      Vivamus aliquet purus non tincidunt posuere.
    </p>
  </article>
</body>
```

- `<body>` est 
  - le parent de `<article>`
  - l'ancêtre de `<h1>`
  - l'ancêtre de `<p>`

- `<article>` est 
  - l'enfant de `<body>`
  - le parent de `<h1>`
  - le parent de `<p>`

- `<p>` est 
  - le frère de `<h1>` 
  - l'enfant de `<article>`
  - le déscendant de `<body>`

---

## Types d'éléments

Les 2 types principaux sont `block` et `inline`

Par exemple

|block|inline|
|-----|------|
|`<p>` <br> `<h1>`...`<h6>` <br> `<main>`<br> `<section>`<br> `<article>`<br>`<div>`<br>...|`<a>`<br>`<em>`<br>`<strong>`<br>`<img>`<br>`<abbr>`<br>`<span>`<br>...|


### Les éléments ["en bloc"](https://developer.mozilla.org/fr/docs/Web/HTML/%C3%89l%C3%A9ments_en_bloc) 

- commencent sur une nouvelle ligne
- occupent le maximum d'espace disponible (la largeur de leurs conteneurs)
- peuvent contenir des éléments `block` ou `inline` 


### Les éléments ["en ligne"](https://developer.mozilla.org/fr/docs/Web/HTML/%C3%89l%C3%A9ments_en_ligne) 

- suivent le fil du texte
- occupent l'espace de leur contenu (la largeur de leurs contenus)
- ne peuvent contenir que des éléments `inline`; seule exception, le lien `<a>` qui lui peut contenir des éléments de type `block`

### Les autres types

D'autres types existent comme 
- **list item** `<li>`
- **table** `<table>`
- etc...

> Pour aller plus loin avec les types d'éléments, la page sur les [catégories de contenu](https://developer.mozilla.org/fr/docs/Web/HTML/Cat%C3%A9gorie_de_contenu) du MDN est très complète

---

## Les liens

Les liens hypertextes sont la base du web, ils permettent de naviguer au sein d'un même site ou vers des sites distants.

Plusieurs types de cibles sont donc possible

- Liens dans la même page | **les ancres**
- Liens dans d'autres pages du même site | **les chemins relatifs**
- Liens vers des sites distants | **les chemins absolus**

Quelque soit la cible, l'élément HTML reste le même, il s'agit de `<a>`; l'attribut `href` permettra de différencier les différentes destinations

### Les ancres

Les ancres permettent de naviguer dans la même page grâce à l'attribut `id`

```html
<header id="header-page">
  <h1>Le blog</h1>
  ...
</header>


...


<a href="#header-page">Retour en haut de la page</a>
```

### URL relative

Le chemin relatif vers un fichier depuis la page courante

![Arborescence fichiers](img/arbo.png)

En simulant une navigation entre les différents fichiers, la structure relative est plus claire

Depuis **index.html**
```html
<nav>
  <a href="index.html">Accueil</a> <!--page courante-->
  <a href="articles/hero-corp.html">Hero Corp</a>
  <a href="articles/jessica-jones.html">Jessica Jones</a>
</nav>
```
Pour atteindre `Hero Corp` il faut d'abord aller dans `articles/`, le répertoire  qui le contient

Depuis **articles/hero-corp.html**
```html
<nav>
  <a href="../index.html">Accueil</a>
  <a href="hero-corp.html">Hero Corp</a> <!--page courante-->
  <a href="jessica-jones.html">Jessica Jones</a>
</nav>
```
Pour retourner à `Accueil` il faut d'abord remonter d'un le répertoire avec `../`

Pour aller à `Jessica Jones` il suffit de le cibler directement, il se trouve dans le même répertoire

Depuis **articles/jessica-jones.html**
```html
<nav>
  <a href="../index.html">Accueil</a>
  <a href="hero-corp.html">Hero Corp</a> 
  <a href="jessica-jones.html">Jessica Jones</a> <!--page courante-->
</nav>
```

### URL absolue

Les URLs absolues sont composées de 3 parties

Exemple : `http://blog-heroique.com/articles/hero-corp.html`

- **le protocle** `http://`
- **le domaine** `blog-heroique.com`
- **le chemin du fichier** `articles/hero-corp.html`