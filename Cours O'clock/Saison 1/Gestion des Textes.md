# Gestion des textes

- [CSS Fonts MDN](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Fonts)
- [CSS Text MDN](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Text)
- [CSS Text Decoration MDN](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Text_Decoration)

## font-family [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/font-family)

La typo à utiliser

```css
body { font-family: serif; }
```
### Classification

Les noms de typos contenant des espaces doivent être notées entre `quotes`

5 groupes de typos existent dans lesquels sont répartis les différentes typos

On parle de typos sécurisées quand elles sont installées par défaut sur n'importe quel système d'exploitation

| Groupe | Typos sécurisées | Typos fréquentes |
| --- | --- | --- |
| **serif** | Georgia, "Times New Roman" | "Lucida Bright", "Lucida Fax", "Palatino" |
| **sans-serif** | Arial, "Arial Black", Verdana, Impact, "Trebuchet MS" | "Open Sans", "Fira Sans", "Lucida Sans"|
| **monospace** | "Courier New" | "Fira Mono", "DejaVu Sans Mono", Menlo |
| **cursive** |  | "Brush Script MT", "Brush Script Std", "Lucida Calligraphy" |
| **fantasy** |  | Papyrus, Herculanum, "Party LET" |

### Déclaration

Il convient de terminer une déclaration `font-family` par le groupe de typos auquel appartient la typo demandée, si elle n'est pas utilisable l'affichage restera tout de même cohérent
```css
body { font-family: "Georgia", serif; }

body { font-family: "Open sans", "Helvetica Neue", Arial, sans-serif; }
```

## font-size [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/font-size)

Taille de la typo

```css
body { font-size: 16px; }
/*
Valeurs possibles  :
  ...px
  ...%
  ...em
  ...rem
*/
```

## font-weight [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/font-weight)

Graisse de la typo

```css
body { font-weight: normal; }
/*
Valeurs possibles :
  normal | par défaut
  bold

  100 / Thin
  200 / Extra Light 
  300 / Light 
  400 / Normal 
  500 / Medium 
  600 / Semi Bold 
  700 / Bold
  800 / Extra Bold 
  900 / Ultra Bold 
*/
```

## font-style [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/font-style)

Mise en italique

```css
body { font-style: italic; }
/*
Valeurs possibles :
  normal | par défaut
  italic
  oblique
*/
```

## font-variant [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/font-variant)

Petites capitales

```css
body { font-variant: normal; }
/*
Valeurs possibles :
  normal | par défaut
  small-caps
*/
```

## line-height [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/line-height)

Interlignage

```css
body { line-height: 16px; }
/*
Valeurs possibles  :
  normal | par défaut
  valeur numérique sans unité = multiplicateur
  ...px
  ...%
  ...em
  ...rem
*/
```

## letter-spacing [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/letter-spacing)

Interlettrage

```css
body { letter-spacing: normal; }
/*
Valeurs possibles  :
  normal | par défaut
  ...px
  ...em
  ...rem
*/
```

## text-align [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/text-align)

Alignement du texte

```css
body { text-align: left; }
/*
Valeurs possibles :
  left | par défaut
  center
  right
  justify
*/
```

## text-decoration [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/text-decoration)

Soulignement du texte

```css
body { text-decoration: none; }
/*
Valeurs possibles :
  none
  underline
  overline
  line-through
  underline overline
*/
```

## text-transform [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/text-transform)

Majuscules / Minuscules

```css
body { text-transform: none; }
/*
Valeurs possibles :
  none
  capitalize
  uppercase
  lowercase
*/
```

## text-shadow [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/text-shadow)

Ombre du texte

```css
body { text-shadow: red 0 2px 5px; }
/*
Valeurs possibles :
  none
  <color> <x> <y> <blur-radius>
*/
```