# Flexbox

- [Flexbox sur W3C](https://www.w3.org/TR/css-flexbox)
- [Flexbox sur MDN](https://developer.mozilla.org/fr/docs/Web/CSS/Disposition_des_bo%C3%AEtes_flexibles_CSS/Utilisation_des_flexbox_en_CSS)
- [Flexbox playground](https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos)
- [CSS-tricks flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox)
- [Guide flexbox](https://internetingishard.com/html-and-css/flexbox/)

`flexbox` pour Flexible box, est une manière très puissante de réaliser une mise en page.

Avant tout, la connaissance de la terminologie est très utile pour saisir quelques subtilités.

![flex-terminology](https://www.w3.org/TR/css-flexbox/images/flex-direction-terms.svg)

---

**flex container**

L’élément parent dans lequel chaque élément flex sera contenu. Un conteneur flex est défini lorsque la propriété `display` possède la valeur flex ou inline-flex.

**flex item**

Chaque enfant d’un conteneur flex devient un élément flex. Le texte directement contenu dans un conteneur flex est englobé dans un élément flex anonyme.

**Axes**

Toute boîte suit deux axes : L’axe principal (main axis) sur lequel les éléments flex se suivent. L’axe secondaire (cross axis) est perpendiculaire à l’axe principal.

- La propriété `flex-direction` établit l’axe principal.
- La propriété `justify-content` définit comment les éléments flex sont positionnés le long de l’axe principal sur la ligne courante.
- La propriété `align-items` définit comment les éléments flex sont positionnés le long de l’axe secondaire sur la ligne courante.
- La propriété `align-self` définit comment un seul élément flex est aligné sur l’axe secondaire et surcharge le comportement par défaut défini par `align-items`.

**Directions**

Le début/fin du côté principal et du côté secondaire du conteneur flex décrit l’origine et la fin du flux d’éléments flex. Ils suivent l’axe principal et secondaire du conteneur flex dans le sens établi par writing-mode (gauche-vers-droite, droite-vers-gauche, etc.).

- La propriété `order` ordonne les éléments d’un groupe et détermine quel élément va apparaitre en premier.
- La propriété `flex-flow` raccourcis les propriétés `flex-direction` et `flex-wrap` pour positionner les éléments flex.

**Lines**

Les éléments flex peuvent être positionnés soit sur une seule ligne, soit sur plusieurs lignes via la propriété `flex-wrap`, qui contrôle la direction de l’axe secondaire et la direction dans chaque nouvelle lignes rajoutées.

**Dimensions**

Les termes désignant la hauteur et la largeur des éléments flex sont la taille principale (main size) et la taille secondaire (cross size), qui suivent respectivement l’axe principal et l’axe secondaire du conteneur flex.

- Les propriétés `min-height` et `min-width` ont une valeur initiale de auto.
- La propriété `flex` est un raccourci des propriétés `flex-grow`, `flex-shrink` et `flex-basis` pour établir la flexibilité des éléments flexibles.

> Provenant de MDN

---

## Avant de commencer

Prérequis indispensable

```css
* {
  box-sizing: border-box;
}
```

## La clé d'un monde merveilleux

`display: flex;` ou `display: inline-flex;`

La différence entre les 2 est la même que entre `block` et `inline-block`, aucun changement donc sur le comportement de flexbox.

## Main dans la main, 2 lots de règles

un 'flex-container' et des 'flex-item' fonctionnent ensemble, le container donne des règles de formatage et les items les respectent. Les items peuvent avoir des règles propres pour surpasser celles du container.

### flex-container

le `display: flex` s'applique sur le container

```css
.flex-container {
	display: flex; /* la clé ;) */
}
```

#### dans quelle direction vont les items ?

Basée sur le `main-axis`

**`flex-direction`**

- `row` * de gauche à droite
- `column` de haut en bas
- `row-reverse` de droite à gauche
- `column-reverse` de bas en haut

#### Comment les items seront alignés sur l'axe principal ?

**`justify-content`**
- `flex-start` * les items commencent à `main-start`
- `flex-end` les items commencent à `main-end`
- `center` les items sont centrés  sur l'axe principal `main-axis`
- `space-between` les items sont répartis sur l'axe principal depuis `main-start` jusqu'à `main-end`
- `space-around` les items sont répartis sur l'axe principal, espacés de manière égale.

#### Comment les items seront alignés sur l'axe secondaire `cross-axis` ?

**`align-items`**
- `stretch` * les items occupent tout l'espace disponible (sauf indication contraire sur un item)
- `flex-start` les items commencent à `cross-start`
- `flex-end` les items commencent à `cross-end`
- `center` les items sont centrés  sur l'axe secondaire `cross-axis`
- `baseline` les items sont alignés sur la même baseline [mdn](https://developer.mozilla.org/fr/docs/Web/CSS/align-items)

#### Les items tiennent sur une seule ligne ou sur plusieurs lignes ?

**`flex-wrap`**
- `nowrap` * les items tiennent sur une seule ligne
- `wrap` les items seront rangés sur plusieurs lignes de haut en bas
- `wrap-reverse` les items seront rangés sur plusieurs lignes de bas en haut

#### Quand les items sont sur plusieurs lignes, comment aligner ce bloc de lignes globalement  ?

`align-content` se comporte de la même façon que `justify-content` mais sur l'axe secondaire; *ne s'applique que sur plusieurs lignes d'items*

**`align-content`**
- `stretch` * les items sont réparties pour occuper l'espace
- `flex-start` les lignes sont regroupées à `cross-start`
- `flex-end` les lignes sont regroupées à `cross-end`
- `center` les lignes sont regroupées au centre du container
- `space-between` les lignes sont réparties sur l'axe secondaire depuis `cross-start` jusqu'à `cross-end`
- `space-around` les lignes sont réparties sur l'axe secondaire, espacées de manière égale.


### flex-item

```css
.flex-item { /* ... */ }
```
#### un item peut se ré-ordonner par rapport aux autres ?

**`order`**

0 représente la position par défaut, tous les nombres plus grands déplaceront l'item vers la fin, les plus petits vers le débuts.


#### un item peut être aligné différemment que les autres ?

**`align-self`**

écrase l'alignement par défaut fourni par `align-items`

`align-self: auto | flex-start | flex-end | center | baseline | stretch;`

#### Un item peut avoir une taille différente des autres ?

**`flex-basis`**

`auto` * flex utilisera `width` ou `height`
valeur - l'item prendra cette valeur par défaut comme taille mais avant l'attribution d'espace fait par flex

![flexbasis](https://www.w3.org/TR/css-flexbox-1/images/rel-vs-abs-flex.svg)

#### un item peut occuper plus ou moins d'espace que les autres ?

[Démo explicative](https://developer.mozilla.org/fr/docs/Web/CSS/flex-shrink#frame_Exemples)

**`flex-grow`**

si tous les items possèdent une `flex-grow` de 0, un item possédant un `flex-grow` de 1 occupera le maximum d'espace par rapport aux autres, donc si plusieurs items possède le meme `flex-grow` ils s'entendront pour se repartir l'espace.

**`flex-shrink`**

Facteur de rétrécissement autorisé