# Bootstrap

[Bootstrap](https://getbootstrap.com/)

Bootstrap est un framework CSS, le plus populaire, utilisé pour des dashboards, du prototypage, des thèmes de multiples CMS, etc...

C'est un ensemble de composants structurés servant à créer une base de travail et à organiser le code. Le but principal est la simplification du travail pour les développeurs que ce soit pour le démarrage de projet, le prototypage ( Proof Of Concept ), la  maintenance ou encore la productivité.

Apprentissage et pratique étant les maîtres mots du développeur, il va sans dire que le meilleur moyen pour pleinement découvrir un outil est de lire sa documentation et d'expérimenter les différentes options qu'il propose. 

Bootstrap embarque par défaut :

- Reboot.css (depuis la v4, anciennement Normalize.css)
- Système de mise en page responsive basé sur une grille de 12 colonnes et de multiples outils autour de cette grille pour la réorganisation, le masquage d'éléments, l'adaptation en fonction des tailles d'écran.
- Des composants CSS pré-construits comme des barres de navigation, des blocs de formulaires ou des boutons.
- Des composants JS basés sur jQuery, modal box, carousel, menus dépliants, système d'onglets.
- Un système de customisation du thème de base.

## Système de grille

Le [système de grille](https://getbootstrap.com/docs/4.0/layout/grid/) de Bootstrap est très flexible et offre de nombreuses options de mise en page.

<table>
<thead>
<tr>
	<th>-</th>
	<th>Extra small</th>
	<th>Small</th>
	<th>Medium</th>
	<th>Large</th>
	<th>Extra Large</th>
</tr>
</thead>

<tbody>
<tr>
	<th>Device</th>
	<td>Téléphone</td>
	<td>Téléphone HD</td>
	<td>Tablette</td>
	<td>Desktop</td>
	<td>Desktop HD</td>
</tr>
<tr>
	<th>Breakpoint</th>
	<td>< 576px</td>
	<td>≥ 576px</td>
	<td>≥ 768px</td>
	<td>≥ 992px</td>
	<td>≥ 1200px</td>
</tr>
<tr>
	<th>Comportement</th>
	<td>Toujours côte à côte</td>
	<td colspan="4">Empilement au départ, côte à côte au dessus du breakpoint</td>
</tr>
<tr>
	<th>Class</th>
	<td><code>.col-*</code></td>
	<td><code>.col-sm-*</code></td>
	<td><code>.col-md-*</code></td>
	<td><code>.col-lg-*</code></td>
	<td><code>.col-xl-*</code></td>
</tr>
<tr>
	<th>Largeur du container</th>
	<td>Auto</td>
	<td>540px</td>
	<td>720px</td>
	<td>960px</td>
	<td>1140px</td>
</tr>
</tbody>
</table>

### Exemple de grille avec des `class` xs et md

![grid-exemple](img/grid-bootstrap.png)

## Composants

De multiples [composants](https://getbootstrap.com/docs/4.0/components/) sont disponibles avec Bootstrap, en voici quelques uns :

- Icônes
- Boutons dépliants
- Groupes de champs de formulaire
- Système d'onglets
- Barre de navigation
- Fil d'ariane
- Éléments de pagintaion
- Labels
- Badges
- Messages d'alertes
- Panneaux
- Bulles de navigation
- Modal
- Caroussel
- ...

## Personnalisation avancée

Il est possible de [configurer](https://getbootstrap.com/customize/) assez finement bootstrap.

- Couleurs de typos
- Breakpoints responsive
- Couleurs de fonds
- Nombre de colonnes dans la grille
- ...

---

**Autres Frameworks CSS**

D'autres frameworks existent, plus légers, plus lourds, plus simples, plus complexes, plus riches, plus versatiles... mais Bootstrap reste néanmoins de loin le plus largement utilisé.

- [Foundation](http://foundation.zurb.com/)
- [Skeleton](http://getskeleton.com/)
- [PureCSS](https://purecss.io/)
- [Materialize](http://materializecss.com/)
- [Sematic UI](http://semantic-ui.com/)
- ...