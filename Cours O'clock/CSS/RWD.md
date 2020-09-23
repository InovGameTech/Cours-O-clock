## RWD en 3 étapes

**RWD** ou **R**esponsive **W**eb **D**esign / Webdesign (UI) qui s'adapte aux périphériques

- [ ] *Device* - Prendre en compte le périphérique
- [ ] *Mobile First* - Concevoir le CSS pour le mobile avant-tout
- [ ] *Breakpoints* - Définir des points de décrochage

## 1. *Device* - Prendre en compte le périphérique

Simplement avec un élément HTML `<meta name="viewport">` en spécifiant 3 informations

- `width=device-width` on se base sur la largeur du device
- `initial-scale=1` zoom réglé à 1
- `user-scalable=no` L'utilisateur ne peut pas zoomer (optionnel, en fonction des cas)

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

## 2. *Mobile First* - Concevoir le CSS pour le mobile avant-tout

L'objectif est d'intégrer avant-tout pour la plus petite taille d'écran.

### Outils

- [`width` sur MDN](https://developer.mozilla.org/fr/docs/Web/CSS/width)
- [`height` sur MDN](https://developer.mozilla.org/fr/docs/Web/CSS/height)
- [Unités sur MDN](https://developer.mozilla.org/fr/docs/Web/CSS/length#vh)

#### min & max

Permet de définir une largeur (ou hauteur) minimun ou maximun qu'un élément pourra avoir.

> En gardant à l'esprit que
>
>`min-width` **>** `max-width` **>** `width`
>
>`min-height` **>** `max-height` **>** `height`

#### em & %

Le calcul `cible / contexte = résultat` est très pratique pour adapté du fixe vers du fluide.

**Exemple**

Pour afficher un titre d'une taille de `24px`, tout en sachant que`<body>` est configuré avec une `font-size` de `16px`
> 24 / 16 = 1.5

Notre titre pourra donc être déclaré comme ceci

```css
h1 {
	font-size: 1.5em;
}
```

#### vh & vw

Donner la hauteur de la fenêtre à un élément est parfois bien compliqué.

L'unité `vh` s'appuie sur le `viewport`


- `vh` 1/100e de la hauteur du viewport.
- `vw` 1/100e de la largeur du viewport.
- `vmin` 1/100e de la valeur minimale entre la hauteur et la largeur du viewport.
- `vmax` 1/100e de la valeur maximale entre la hauteur et la largeur du viewport.

```css
section {
	height: 100vh;
}
```

---

## 3. *Breakpoints* - Définir des points de décrochage


Afin de respecter l'approche **Mobile First**, le mode de conception va du plus petit au plus grand. La principale caractéristique du CSS (Cascading) va rendre la tâche relativement simple.

### Structure d'une `Media Query`

[@media sur MDN](https://developer.mozilla.org/fr/docs/Web/CSS/@media)

```css
@media <media-query-list> {
	/* Règles CSS appliquées si la requête est vérifiée */
}
```

### Types de média

| Type | Description |
|---|---|
| `all` | Peut être appliqué quel que soit l'appareil. |
| `print` | Destiné aux œuvres paginés et aux documents qui sont vus sur des écrans pour l'aperçu avant impression. |
| `screen` | Destiné aux écrans d'ordinateur en couleurs. |
| `speech` | Destiné aux synthétiseurs vocaux. |

### Principales caractéristiques de média

| Caractéristique | Description | Notes |
|---|---|---|
| [`width`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/width) | Largeur de la zone d'affichage (*viewport*). | `min-...`, `max-...`  |
| [`height`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/height) | Hauteur de la zone d'affichage (*viewport*).| `min-...`, `max-...` |
| [`aspect-ratio`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/aspect-ratio)| Proportion de la largeur sur la hauteur pour la zone d'affichage (*viewport*).|`min-...`, `max-...`|
| [`orientation`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/orientation)| Orientation de la zone d'affichage (*viewport*).| `portrait` ou `landscape` |
| [`resolution`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/resolution)| Densité de pixels pour l'appareil d'affichage| `min-...`, `max-...` |

Et dans un avenir proche

| Caractéristique | Description | Notes |
|---|---|---|
| [`light-level`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/light-level) | Le niveau de lumière ambiante actuel.| Ajouté avec la spécification sur les requêtes média de niveau 4|
| [`scripting`](https://developer.mozilla.org/fr/docs/Web/CSS/@media/scripting)| La manipulation via les scripts (ex. JavaScript) est-elle disponible ?| Ajouté avec la spécification sur les requêtes média de niveau 4|

### Opérateurs

#### `and`

Combinaison de caractéristiques

```css
@media (min-width: 700px) and (orientation: portrait) {
	/* … */
}
```

Les styles seront appliqués si le périphérique a au moins une largeur de 700px et est en orientation portrait.

#### `,`

Association de plusieurs requêtes

```css
@media (orientation: portrait), screen and (max-width: 500px) {
	/* … */
}
```

Les styles seront appliqués pour tous les types de périphériques en orientation portrait et aux périphériques `screen`  avec au maximum une largeur de 500px.

D'autres opérateurs logiques sont disponibles comme `only`, le détail est disponible sur le [MDN](https://developer.mozilla.org/fr/docs/Web/CSS/Requ%C3%AAtes_m%C3%A9dia/Utiliser_les_Media_queries)

### Breakpoints types

```css
/* Mobile First CSS */

/* Mobile + */
@media (min-width: 400px) { /* ... */ }

/* Phablets */
@media (min-width: 550px) { /* ... */ }

/* Tablettes */
@media (min-width: 750px) { /* ... */ }

/* Desktop */
@media (min-width: 1000px) { /* ... */ }

/* Desktop HD */
@media (min-width: 1200px) { /* ... */ }

/* Desktop Wide */
@media (min-width: 1400px) { /* ... */ }
```

C'est alléchant de pouvoir cibler précisément certains devices en fonctions de leurs caractéristiques, pour autant il vaut mieux ne pas tomber dans ce genre de piège et rester sur des "fourchettes" globales; qui sait quelle taille d'écran sortira demain...