# Les textes

Les textes dans une page HTML représentent la majeure partie du contenu.

Dans les différents éléments servant à gérer le contenu il est possible de qualifier finement le contenu
- Une notion importante [`<strong>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/strong)
- Une emphase [`<em>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/em)
- Une citation dans une phrase [`<q>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/q)
- Une abbréviation [`<abbr>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/abbr)
- Une heure ou une date [`<time>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/time)
- Un exposant [`<sup>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/sup)
- Un indice [`<sub>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/sub)
- etc...

## Paragraphe [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/p)

L'élément HTML de texte par excellence, `<p>` sert à délimiter un paragraphe de texte

```html
<p>
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Pellentesque scelerisque suscipit nibh quis porttitor.
  Integer iaculis mi urna, a pulvinar quam adipiscing ut. 
</p>
```

## Titres [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/Heading_Elements)

Les élements HTML de titres allant du niveau 1 au niveau 6 

- `<h1>` Titre principal
- `<h2>` Sous-titre
- `<h3>` Sous sous-titre
- `<h4>` ... 
- `<h5>` ... ...
- `<h6>` ... ... ...

## Citations 

Bloc de citation [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/blockquote)
```html
<p>William L. McKnight, PDG de 3M entre 1949 et 1966, a déclaré en 1948 :</p>
<blockquote>
  <p>
    "As our business grows, it becomes increasingly necessary to delegate responsibility and to encourage men and women to exercise their initiative. 
    This requires considerable tolerance. Those men and women, to whom we delegate authority and responsibility, if they are good people, are going to want to do their jobs in their own way.
  </p>
  <p>
    "Mistakes will be made. But if a person is essentially right, the mistakes he or she makes are not as serious in the long run as the mistakes management will make if it undertakes to tell those in authority exactly how they must do their jobs."
  </p>
  <p>
    "Management that is destructively critical when mistakes are made kills initiative. And it's essential that we have many people with initiative if we are to continue to grow."
  </p>
</blockquote>
```

Citation dans un paragraphe [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/q)
```html
<p>
  William L. McKnight encourage 3M à <q>"delegate responsibility and encourage men and women to exercise their initiative."</q> dans son management
</p>
```

## Listes

3 types de Listes

- Liste non-ordonnée `<ul>`
- Liste ordonnée `<ol>`
- Liste de définition `<dl>`

Les listes non-ordonnées `<ul>` et ordonnées `<ol>` ne peuvent avoir comme seuls enfants que des `<li>` items de liste . Les `<li>` contiendront les autres éléments.

### Liste sans ordre [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/ul)

- item 1
- item 2 
- item 3

```html
<ul>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ul>
```

### Liste ordonnée [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/ol)

1. item 1
2. item 2 
3. item 3 

```html
<ol>
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
</ol>
```

### Liste de définitions [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/dl)

Liste d'items comportant un terme et une définition de ce terme, idéal pour les glossaires

```html
<dl>
  <dt>Terme à définir</dt>
  <dd>Définition</dd>
  <dt>HTML</dt>
  <dd>Langage pour concevoir des pages web</dd>
</dl>
```
