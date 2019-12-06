# CSS ?

Le **CSS** ou **C**ascading **S**tyle **S**heets (feuilles de style en cascade) offre la possibilité de styliser des langages de balises comme le HTML. Appliquer des couleurs, définir des marges, positionner des éléments et bien d'autres choses...

Là où le HTML représente le **fond**, le CSS lui, représente la **forme**

## Où écrire du CSS

### En attribut

```html
<p style="color: blue;">Lorem ipsum dolor sit amet</p>
```

### Dans `<head>`

Dans une balise `<style>...</style>`

```html
<html>
  <head>
    <title>Hello</title>
    <style>
       p{ color: blue; }
    </style>
  </head>
  <body>
    <p>Lorem ipsum dolor sit amet</p>
  </body>
</html>
```

### Dans un fichier séparé


Le fichier CSS prendra `.css` pour extension

```css
/* Fichier styles.css */
p{ color: blue; }
```

La liaison avec le HTML est assurée par une balise `<link>`

```html
<html>
  <head>
    <title>Hello</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <p>Lorem ipsum dolor sit amet</p>
  </body>
</html>
```

Afin d'assurer la séparation entre le contenu (fond) et l'apparence (forme)
**cette méthode est la voie à suivre**