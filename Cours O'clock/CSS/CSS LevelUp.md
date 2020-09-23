# CSS LevelUp

Un réflexe à adopter très rapidement est de s'assurer de la compatibilité d'une règle ou d'une pratique en se rendant sur [Caniuse](http://caniuse.com/)

Il est possible que certaines règles ne soit pas supportées par certains navigateurs ou que leur usage nécessite l'adoption de préfixe propre à chaque navigateur

## Pseudo-classes [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/Pseudo-classes)

La syntaxe comporte `:`

```css
selector:pseudo-classe{}
```

### `:hover`

Agira au survol de l'élément ciblé

```html
<p class="chapeau">Lorem ipsum dolor <span>sit</span> amet</p>
```

```css
.chapeau:hover span{
  background: #EAEAEA;
}
```
Au survol de `.chapeau` le `<span>` enfant changera de couleur de fond

### `:focus`

Agira au focus de l'élément ( quand le curseur se place dans un champ par exemple )

```html
<input class="adresse" value="Fond vert si sélectionné">
```

```css
.adresse:focus{
  background: green;
}
```
Au 'focus' du champ de formulaire `.adresse` sa couleur de fond devient verte

### `:first-child` & `:last-child`

Cible le premier/dernier élément de son niveau

```html
<ul>
  <li>Un élément</li>
  <li>Un autre élément</li>
  <li>Et encore un élément</li>
  <li>Ensuite...</li>
  <li>Un dernier élément</li>
</ul>
```

```css
li{
  color: blue;
}
li:first-child{
  color: red;
}
li:last-child{
  color: green;
}
```

Le texte des `<li>` est bleu sauf pour le premier qui lui est rouge et le dernier qui est vert.

> **Il existe beaucoup de pseudo-classes, elles sont toutes listées sur [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/Pseudo-classes)**

- [Exemples sur CodePen](https://codepen.io/zakkain/pen/ALiBx) (code + résultat) d'usage complexe des pseudo-classes utilisant `child`.

---

## Pseudo-élément [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/Pseudo-%C3%A9l%C3%A9ments)

La syntaxe comporte `::`

```css
selector::pseudo-element {}
```
### `::before` & `::after`

Idéal pour la décoration, ces éléments peuvent être facilement manipulés sans impacter le selecteur principal

```html
<p class="chapeau">{::before agira ici} Lorem ipsum dolor sit amet {::after agira ici}</p>
```

```css
.chapeau::before {
  content: 'Début de la phrase : ';
  color: red;
}

.chapeau::after {
  content: ' La phrase est finie';
  color: blue;
}
```

### `::first-letter` [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/::first-letter)

Idéal pour traiter une lettrine

```css
.chapeau::first-letter {
  color: red;
  font-size: 130%;
}
```

## Transitions

[Transitions CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Transitions) & [Utiliser les transitions CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Transitions/Utiliser_transitions_CSS) sur le MDN

```css
div {
  /* Ce que l'on souhaite animer width, background, color, ... \ `all` par défaut*/
  transition-property: all;

  /* Auelle durée pour l'animation 0.3s, 500ms, 2s ... */
  transition-duration: 0.8s;

  /*  Mode d'animation ease, linear, ease-in, ease-out, ease-in-out | `ease` par défaut */
  transition-timing-function: ease;

  /* Durée de décalage du début de la transition 0.3s, 200ms, 1s ... */
  transition-delay: 0;
}

/* méthode courte */
div {
  transition: <property> <duration> <timing-function> <delay>;
}
```

Au survol d'un lien la transition de `background` et de `color` prendra 1 seconde

```css
a{
  background: black;
  color: white;
  transition: 1s;
}

a:hover{
  background: yellow;
  color: red;
}
```


## Animations

[Animations CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Animations_CSS) & [Utiliser les animations CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Animations_CSS/Utiliser_les_animations_CSS) sur le MDN

Partant du postulat suivant

```html
<div class="change-fond">Je suis changeant</div>
```

```css
.change-fond{
  color: white;
  font-family: monospace;
  width: 300px;
  padding: 20px 0;
  text-align: center;
  margin: 50px auto;
}
```

Nous allons animer la couleur de fond de notre `<div>`

```css

.change-fond{
  /* ... contenu précédent ... */

  /* L'identifiant de l'animation déclaré dans @keyframes ... */
  animation-name: changecouleur;

  /* La durée de l'animation 0.3s, 500ms, 5s ... */
  animation-duration: 8s;

  /* Mode d'animation ease, linear, ease-in, ease-out, ease-in-out | `ease` par défaut */
  animation-timing-function: linear;

  /* Durée de décalage du début de la'animation 0.3s, 200ms, 1s ... */
  animation-delay: 0s;

  /* Nombre de fois que l'animation sera jouée 3, 10, infinite  | `1` par défaut */
  animation-iteration-count: infinite;

  /* Sens de l'animation
    normal : démarre à 0% fini à 100% (par défaut)
    reverse : démarre à 100% fini à 0%
    alternate : démarre à 0% va à 100% revient à 0% repart à 100% ...  
    alternate  reverse : démarre à 100% va à 0% revient à 100% repart à 0% ...  
  */
  animation-direction: alternate;

  /* Quels styles sont appliqués avant le début de l'animation et après la fin de l'animation
    none : aucun style appliqué (par défaut)
    backwards : Les styles du point de départ sont appliqués avant l'animation
    forwards : Les styles du point d'arrêt sont appliqués après l'animation
    both : Les styles sont appliqués au point de départ et au point d'arrêt
  */
  animation-fill-mode: none;

  /* Lecture ou pause d'une animation
    running : lecture de l'animation (par défaut)
    paused : pause dans l'animation
  */
  animation-play-state: running;
}


/* méthode courte */
.change-fond{
  animation: <name> <duration> <timing-function> <delay> <iteration-count> <direction> <fill-mode> <play-state>;
}

@keyframes changecouleur {
  0% {
    background: #234567;
  }
  50% {
    background: #789654;
  }
  100% {
    background: #987654;
  }
}
```

Pour aider à la création d'animations complexes, des outils comme [Bounce.js](http://bouncejs.com/) peuvent être utilisés.

[Animate.css](https://daneden.github.io/animate.css/), une collection d'animations CSS peut également être utile  

## Transformations

Le [guide d'utilisation des transformations CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Transforms/Utilisation_des_transformations_CSS) du MDN est très simple et permet de comprendre rapidement le fonctionnement des transformations en CSS.

En passant par la propriété [`transform`](https://developer.mozilla.org/fr/docs/Web/CSS/transform)

```css
p {
	transform: translate(0, 20);
}
```

### translate

`translate` peut prendre 1 ou 2 arguments
- 1 argument : la valeur du déplacement sur `x`
- 2 arguments : le 1er pour la valeur du déplacement sur `x`  le 2eme pour `y`

```css
/* déplacement de 240px sur l'axe `x` et de 100px sur `y` */
transform: translate(240px, 100px);
```

Il existe les variantes `translateX()` et `translateY()` pour ne spécifier que la valeur de `x` ou de `y`

### rotate

`rotate()` prend 1 argument pour spécifier l'angle de rotation le plus exprimé en degrés `deg` mais [d'autres possibilités existent](https://developer.mozilla.org/fr/docs/Web/CSS/angle))

```css
/* rotation de 30 degrées */
transform: rotate(30deg);
```

### scale

`scale` peut prendre 1 ou 2 arguments
- 1 argument : proportion de redimensionnement uniforme pour la largeur et la hauteur
- 2 arguments : le 1er, redimensionnement de la largeur,  le 2eme, de la hauteur

```css
/* 2 fois plus petit */
transform: scale(0.5);

/* taille normale */
transform: scale(1);

/* 2 fois plus grand */
transform: scale(2);

/* symétrie, effet miroir */
transform: scale(-1);
```

Il existe les variantes `scaleX()` et `scaleY()` pour ne spécifier que le redimensionnement horizontal ou vertical

### skew

`skew` peut prendre 1 ou 2 arguments
- 1 argument : angle de déformation horizontale
- 2 arguments : le 1er, déformation horizontale,  le 2eme, verticale

l'angle de déformation est exprimé le plus souvent en degrés mais [d'autres possibilités existent](https://developer.mozilla.org/fr/docs/Web/CSS/angle)

```css
/* pas de déformation */
transform: skew(0deg);}
	
/* déformation de 45 degrées */
transform: skew(45deg);

/* équivalent à -60deg */
transform: skew(120deg);
```

## Timing

Il est possible de définir soi-même la temporisation (`transition-timing-function`, `animation-timing-function` ) : https://developer.mozilla.org/fr/docs/Web/CSS/single-transition-timing-function

Un outil très pratique permet d'aider dans la création `cubic-bezier()` : http://cubic-bezier.com/