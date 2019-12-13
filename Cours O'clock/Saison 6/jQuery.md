# jQuery

[jQuery](https://jquery.com/) est une librairie JavaScript (*library* en anglais), c'est-à-dire une bibliothèque de fonctions utilitaires. Initialement conçue en 2006 pour assurer la compatibilité entre navigateurs, cette bibliothèque a depuis évolué et propose de nombreux services autour de la manipulation du DOM. Elle permet une écriture rapide, intuitive et lisible du code JS.

## API (Référentiel des fonctions)

[jQuery API](https://api.jquery.com/)

[jQuery sur devdocs.io](https://devdocs.io/jquery/)

Beaucoup de fonctions sont disponibles, une vraie mine d'or !

## Installation

- directement sur le site de [jQuery](https://jquery.com/download/) (le fichier `jquery` téléchargé est à déposer dans le projet puis à charger dans le HTML)

```html
<script src="../js/jquery.min.js"></script>
```

- depuis un CDN (*Content Delivery Network*) : [code.jquery.com](https://code.jquery.com/) ou [cdnjs](https://cdnjs.com/libraries/jquery)

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.1.1/jquery.min.js"></script>
```

**Cet appel de jQuery doit se trouver avant les autres fichiers JS**

- via NPM : `npm install jquery`

```html
<script src="../node_modules/jquery/dist/jquery.min.js"></script>
```

## Quelques comparaisons entre JavaScript *Vanilla* et jQuery

### Sélectionner `<p id="hello"></p>`

En **JavaScript** dit Vanilla (JS classique)
```js
var element = document.getElementById('hello');
// ou
var element = document.querySelector('#hello');
```

En **jQuery**
```js
var $element = $('#hello');
```

### Modifier le contenu de mon `<p id="hello"></p>`

En **JS Vanilla**
```js
element.textContent = 'Hello!';
element.innerHTML = '<strong>Hello!</strong>';
```

En **jQuery**
```js
$element.text('Hello!');
$element.html('<strong>Hello!</strong>');
```

### Modifier les attributs d'un' `<a id="link" href="">Super lien</a>`

En **JS Vanilla**
```js
var element = document.getElementById('link');
element.href = 'https://oclock.io';
```

En **jQuery**
```js
$('#link').attr('href', 'https://oclock.io');
```

### Créer un élément

En **JS Vanilla**
```js
var item = document.createElement('li');
var list = document.querySelector('ul');
list.appendChild(item);
```

En **jQuery**
```js
var $item = $('<li>');
$('ul').append($item);
```

### Ajouter un écouteur d'événement

En **JS Vanilla**
```js
var element = document.querySelector('#elem');
element.addEventListener('click', handler);
```

En **jQuery**
```js
$('#elem').on('click', handler);
```

### Enlever un écouteur

En **JS Vanilla**
```js
var element = document.querySelector('#elem');
element.removeEventListener('click', handler);
```

En **jQuery**
```js
$('#elem').off();
```

### Agir après le chargement du DOM

En **JS Vanilla**
```js
document.addEventListener('DOMContentLoaded', app.init);
```

En **jQuery**
```js
$(app.init);

//ou pour une simple interaction
$(function() {
  // ...
});
```

### Agir sur une collection d'éléments
Par exemple pour ajouter un écouteur à chaque `button` d'un bloc `#buttons`

En **JS Vanilla**
```js
var buttons = document.querySelectorAll('#buttons button');
for (var index = 0; index &lt; buttons.length; index++) {
  var button = buttons[index];
  button.addEventListener('click', app.onClick);
}
```

En **jQuery**
```js
$('#buttons button').on('click', app.onClick);
```

---

## Un petit tour des possibilités
### Sélection et déplacement de sélection dans le DOM

- [jQuery $()](https://api.jquery.com/jQuery/)
- [jQuery Liste des sélecteurs](https://api.jquery.com/category/selectors/)
- [jQuery .find()](https://api.jquery.com/find/)
- [jQuery .closest()](https://api.jquery.com/closest/)
- [jQuery .parent()](https://api.jquery.com/parent/)
- [jQuery .children()](https://api.jquery.com/children/)
- [jQuery .siblings()](https://api.jquery.com/siblings/)
- [jQuery .first()](https://api.jquery.com/first/)
- [jQuery .last()](https://api.jquery.com/last/)
- [jQuery .next()](https://api.jquery.com/next/)
- [jQuery .prev()](https://api.jquery.com/prev/)
- [jQuery .eq()](https://api.jquery.com/eq/)
- [jQuery .index()](https://api.jquery.com/index/)


```html
<nav>
  <ul>
    <li class="item-1">item 1</li>
    <li class="item-2">item 2</li>
    <li class="item-3">item 3</li>
    <li class="item-4">item 4</li>
    <li class="item-5">item 5</li>
  </ul>
</nav>
```

```js
// Sélectionne <ul>
$('ul');

// Sélectionne tous les <li> du <ul>
$('ul li');

// Sélectionne le <li class="item-2">item 2</li> dans <ul>
$('ul li.item-2');

// Cherche et sélectionne le <li class="item-5">item 5</li> depuis <nav>
$('nav').find('li.item-5');

// Sélectionne le <ul> le plus proche dans l'arborescence
$('li.item-1').closest('ul');

// Sélectionne <nav>
$('ul').parent();

// Sélectionne tous les <li>
$('ul').children();

// Sélectionne tous les frères de <li class="item-3">item 3</li>
$('ul li.item-3').siblings();

// Sélectionne <li class="item-1">item 1</li>
$('ul li').first();

// Sélectionne <li class="item-5">item 5</li>
$('ul li').last();

// Sélectionne <li class="item-2">item 2</li>
$('ul li').first().next();

// Sélectionne <li class="item-4">item 4</li>
$('ul li').last().prev();

// Sélectionne <li class="item-3">item 3</li>
$('ul li').eq(2)

// Récupère l'index d'un élément, ici 3 (0 étant le premier élément)
$('ul li.item-4').index()
```

---

### Manipulation d'éléments
#### Création [API jQuery](https://api.jquery.com/jQuery/#jQuery-html-attributes)

La création d'un élément permet de le manipuler facilement

```js
// Creation d'un élément <img>
$('<img>');

// Création d'un élément et ajout immédiat d'attributs
$('<img>', {
  src: 'images/eiffel.jpg',
  alt: 'Photo de la Tour Eiffel'
});
```

#### Ajout au DOM

- [jQuery .append()](https://api.jquery.com/append/)
- [jQuery .appendTo()](https://api.jquery.com/appendTo/)
- [jQuery .prepend()](https://api.jquery.com/prepend/)
- [jQuery .prependTo()](https://api.jquery.com/prependTo/)

`prepend()` et `prependTo()` fonctionnent comme `append()` et `appendTo()` mais placent les éléments au début

```js
var articleBlog = $('#article-blog');

var imageArticle = $('<img>', {
  src: 'images/eiffel.jpg',
  alt: 'Photo de la Tour Eiffel'
});

articleBlog.append(imageArticle);
//ou
imageArticle.appendTo(articleBlog);
```

#### Modification

- [jQuery .attr()](https://api.jquery.com/attr/)
- [jQuery .css()](https://api.jquery.com/css/)
- [jQuery .addClass()](https://api.jquery.com/addClass/)
- [jQuery .removeClass()](https://api.jquery.com/addClass/)

`.attr()`
```js
// Récupère la valeur de l'attribut `id` de notre élément `.contenu`
$('.contenu').attr('id');

// Affecte la valeur `chapeau` à l'attribut `id` de notre élément `.contenu`
$('.contenu').attr('id', 'chapeau');

// Affecte les attributs de notre élément `.contenu` avec l'objet `attributs`
var attributs = {
  id: 'chapeau',
  title: 'Le chapeau de notre article'
};
$('.contenu').attr(attributs);
```

`.css()`
```js
// Récupère la valeur la propriété css `color` de notre élément `.contenu`
$('.contenu').css('color');

// Affecte la valeur `#FF0000` à `color` de notre élément `.contenu`
$('.contenu').css('color', '#FF0000');

// Affecte les proprietes de notre élément `.contenu` avec l'objet `attributs`
var proprietes = {
  color: '#F3900A',
  backgroundColor: '#C5C5C5'
};
$('.contenu').css(proprietes);
```

`.addClass()` & `.removeClass()`

```html
<p id="chapeau">Lorem ipsum dolor sit amet...</p>
```

```js
// Ajoute la classe `active`
$('#chapeau').addClass('active');

// Ajoute la classe `content` & `important`
$('#chapeau').addClass('content important');

// Supprime la classe `content`
$('#chapeau').removeClass('content');
```

> Après ces opérations...
>```html
><p id="chapeau" class="active important">Lorem ipsum dolor sit amet...</p>
>```

---
### Gérer le contenu

 - [jQuery .val()](https://api.jquery.com/val/)
 - [jQuery .text()](https://api.jquery.com/text/)
 - [jQuery .html()](https://api.jquery.com/html/)

`.val()`

Permet de récupérer très facilement la valeur de tous les types d'éléments de formulaire

```js
// input text, textarea, select, ... jquery recupère la valeur de la même façon
$('form #prenom').val();
```

`.text()`

Permet de récupérer le contenu texte

```js
// Récupère `Lorem ipsum dolor sit amet...`
$('#chapeau').text();

// Affecte `Mon nouveau contenu texte...`
$('#chapeau').text('Mon nouveau contenu texte...');
```

`.html()`

Permet de récupérer le contenu html

```html
<div class="container">
  <div class="box">Boite HTML</div>
</div>
```
```js
// Récupère le contenu HTML `<div class="box">Boite HTML</div>`
$('.container').html();

// Affecte `<span class="item">item simple</span>`
$('.container').html('<span class="item">item simple</span>');
```
---

### Animation d'éléments

- [jQuery .fadeIn()](https://api.jquery.com/fadeIn/)
- [jQuery .fadeOut()](https://api.jquery.com/fadeOut/)
- [jQuery .animate()](https://api.jquery.com/animate/)

```js
// Permet de faire apparaître un élément en fondu en 400 millisecondes par défaut
$('img').fadeIn();

// Il est possible de préciser une durée personnalisée en millisecondes
$('img').fadeIn(1000);

// Cette fois-ci un fondu
$('img').fadeOut(1000);

```
`.animate()`

Permet d'effectuer des animations basées sur les propriétés CSS

```js
// la largeur sera modifiée sur 2000ms soit 2 secondes
$('.contenu').animate({width: '70%'}, 2000);
```

```js
// Les proprietes CSS affectées et une liste d'options configurant l'animation
var proprietes = {
  color: '#8457D1',
  width: '70%'
};

var options = {
  //durée de l'animation
  duration: 2000,
  // mode de transition
  easing: 'easein',
  // callback appelé lorsque l'animation sera terminée
  complete: function(){
    console.log('Animation terminée');
  }
};

$('.contenu').animate(proprietes, options);
```



### Événements

- [jQuery .on()](https://api.jquery.com/on/)
- [jQuery .off()](https://api.jquery.com/off/)

`.on()`

```js
// Ajoute un écouteur sur #validation
$('#validation').on('click', handler);

// Si #formulaire possède plusieurs input, jquery créer autant d'écouteurs que nécesssaire
$('#formulaire input').on('keyup', handler);
```

`.off()`

```js
// Retire tous les écouteurs de #validation
$('#validation').off();

// Retire tous les écouteurs 'click' de #validation
$('#validation').off("click");
```


---

## Astuces
### Enchaîner des instructions

Une des forces de jQuery est le chaînage d'instructions

```js
// Donne moi le 3e enfant de l'élément suivant mon parent :)
$('#mon-div').parent().next().children().eq(2)
```

### Utiliser l'attribut html `data` avec jQuery

Il est possible d'utiliser l'attribut `data` dans une balise HTML pour stocker des informations

```html
<p id="chapeau" data-width="250">Lorem ipsum dolor sit amet...</p>
```

```js
var dataWidth = $('#chapeau').data('width');
//ou
var dataWidth = $('#chapeau').attr('data-width');
```

### Définir un délai dans une chaîne de modifications sans passer par setTimeout avec jQuery

[jQuery .delay()](https://api.jquery.com/delay/)

```js
// .alert est masqué puis s'affiche progressivement, 3 secondes plus tard, il disparaitra progressivement
$('.alert').hide().fadeIn().delay(3000).fadeOut()
```

---

## Plugins jQuery

### jQuery UI

[jQuery UI](https://jqueryui.com) propose une collection de plugins très utiles, comme pouvoir trier des listes d'items, déplacer en drag'n drop, gérrer des sliders, etc...

- [Téléchargement configurable](https://jqueryui.com/download/)
- [CDN](https://code.jquery.com/ui/)

jQuery UI doit être placé après jQuery

```html
<!--jQuery-->
<script src="https://code.jquery.com/jquery-3.1.1.min.js"></script>
<!--jQuery UI-->
<script src="https://code.jquery.com/ui/1.12.1/jquery-ui.min.js"></script>
```
#### Exemple

[Sortable](https://jqueryui.com/sortable/)
```js
$('#shop-list').sortable({
  axis: 'y',
});
```

### Autres plugins

Il existe une multitudes de plugins sur le web comme [FlexSlider](http://flexslider.woothemes.com/)