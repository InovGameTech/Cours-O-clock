# DOM
[Référence du DOM sur MDN](https://developer.mozilla.org/fr/docs/Web/API/Document_Object_Model)

---

## Window [MDN](https://developer.mozilla.org/fr/docs/Web/API/Window)

### Propriétés

### Méthodes

#### `alert()`
affiche une pop up avec message + les boutons `ok` et `annuler`  
``` js
alert("Hello!");
```

#### `prompt()`
Affiche une pop up / boîte de dialogue qui permet à l'utilisateur de saisir une valeur  
``` js
name = prompt("What is your name ? ", "your name here");
```

#### `confirm()`
Affiche une boîte de dialogue qui permet à l'utilisateur de choisir entre `annuler` et `ok`,
```js
confirmation = confirm('Êtes-vous sûr ?');
```

#### `setTimeout()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/WindowTimers/setTimeout)

Exécute une fonction après un certain temps *(en millisecondes)*

```html
<div id="counter">En attente...</div>
```

```js
function writeOk() {
	var counter = document.getElementById('counter');
	counter.textContent = 'OK';
}

var timer = setTimeout(writeOk, 3000);
```

La fonction `writeOk()` sera exécutée au bout de 3000 millisecondes soit 3 secondes


#### `clearTimeout()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/WindowTimers/clearTimeout)

Annule un timer déclaré par `setTimeout`

```js
//...
var timer = setTimeout(writeOk, 3000);

clearTimeout(timer);
```


#### `setInterval()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/WindowTimers/setInterval)

Exécute une fonction à un certain interval de temps *(en millisecondes)*

```js
//...
var timer = setInterval(writeOk, 3000);
```


#### `clearInterval()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/WindowTimers/clearInterval)

Annule un timer déclaré par `setInterval`

```js
//...
var timer = setInterval(writeOk, 3000);

clearInterval(timer)
```

---

## Document [MDN](https://developer.mozilla.org/fr/docs/Web/API/Document)

### Méthodes

#### `getElementById()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/Document/getElementById)

Récupération d'un élément du DOM

```html
<p id="zone-contenu">Contenu original</p>
```

```js
var zoneContenu = document.getElementById('zone-contenu');
zoneContenu.textContent = 'Nouveau contenu';
```

#### `createElement()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/Document/createElement)

Création élément du DOM

```js
var listeItem = document.createElement('li');
//listeItem est un élément de type li, en tant qu'objet du DOM, ces propriétés peuvent être modifiés
listeItem.textContent = 'Un contenu texte';
```

#### `querySelector()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/Document/querySelector)

Permet de récupérer le premier élément correspondant à la syntaxe transmise ( à l'image des `selector` CSS )

```html
<div id="mon-contenu"></div>
```

```js
var monContenu = document.querySelector('#mon-contenu');
```

---

## Element [MDN](https://developer.mozilla.org/fr/docs/Web/API/Element)

### Propriétés

Partant de ce postulat :

```js
var monElement = document.getElementById('mon-element');
```


#### innerHTML

Permet d'ajouter du HTML dans un élément, le code HTML sera interprété

```js
monElement.innerHTML = '<p>du contenu HTML</p>';
```

#### textContent

Permet d'ajouter du texte dans un élément

```js
monElement.textContent = 'simple texte';
```

#### style

Permet de modifier l'attribut style d'un élément

```js
monElement.style = 'color: #F30';
```
Bien que la syntaxe précédente soit viable, il est conseillé d'adopter l'approche par les propriétés que nous offre `.style`

```js
monElement.style.color = '#F30';
```
La syntaxe à adopter suis la logique du `camelCase` aussi :

```js
monElement.style = 'margin-top: 20px';
//la syntaxe sera à adapter de la façon suivante
monElement.style.marginTop = '20px';
```

#### classList [MDN](https://developer.mozilla.org/fr/docs/Web/API/Element/classList)

Retourne la liste des classes (attribut `class="..."`)

`classList` possède plusieurs méthodes intéressantes

```js
monElement.classList.add('info','rouge');
// <div id="mon-element" class="info rouge">
monElement.classList.remove('rouge');
// <div id="mon-element" class="info">
monElement.classList.add('bleu');
// <div id="mon-element" class="info bleu">
monElement.classList.toggle("info");
// <div id="mon-element" class="bleu">
```

#### value

Permet de récupérer le contenu de l'attribut `value` d'un élément HTML (input par exemple)

```js
var valeur = monInput.value;
```

### Méthodes

#### `appendChild()` [MDN](https://developer.mozilla.org/fr/docs/Web/API/Node/appendChild)

Ajout d'un élément (enfant) à un noeud parent

```html
<ul id="liste"></ul>
```

```js
var liste = document.getElementById('liste');
var listeItem = document.createElement('li');

liste.appendChild(listeItem);
```


#### `focus()` [MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/focus)

Applique le **focus** sur un élément HTML

```js
 document.getElementById("mon-input").focus();
```

#### `blur()` [MDN](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement/blur)

Retire le **focus** d'un élément HTML

```js
 document.getElementById("mon-input").blur();
```