# Gestion de projet

La gestion de projet est une démarche visant à organiser de bout en bout le bon déroulement d’un projet. C'est tout l'opérationnel et le tactique qui font qu'un projet aboutit dans un triangle représentant l'équilibre qualité-coût-délai. [Wikipédia](https://fr.wikipedia.org/wiki/Gestion_de_projet).

![triangle-projet](img/triangle-projet.png)

L'objectif de la gestion de projet est de conserver un équilibre entre ces 3 aspects.

## Les grandes étapes d'un projet

_On isole 5 grandes phases dans tout projet._

![Les phases d'un projet](img/phases.png)

### Définition _d'une volonté vers une faisabilité_

- Objectifs du projet
- Reformulation du besoin
- Analyse des risques
- Planification
- Budgetisation
- Cahier des charges

### Conception _du besoin vers une solution technique_

- Spécifications fonctionnelles & techniques
- Description des modules
- Architecture (BDD, Application)
- Méthodes et outils

### Réalisation _d'un plan vers une implémentation_

- Production (nouveau code !)
- Suivi (évolution & maintenance du code existant !)
- Documentation (!!!)

### Validation _d'une production vers son exploitation_

- Jeux des tests (unitaires, fonctionnels)
- Validation des spécifications
- Vérifications de conformité (qualité)

### Livraison _d'un produit vers un outil_

- Revue qualité
- Documentation utilisateur
- Accompagnement
- Maintenance
- Rapport d'interventions

### En résumé

![Les phases d'un projet](img/gdp-phases.png)

## Méthodes et cycles de développement

_On met en musique les 5 grandes phases de différentes manières._

En fonction de la culture entreprise, du projet, des équipes, des impératifs, ...

- [Méthodes traditionnelles / classiques](methodes-classiques.md)
- [Méthodes Agiles](methodes-agiles.md)

## Documents - Livrables
*Outil : Google Drive*

### Cahier des charges
Le cahier des charges est le document qui décrit les besoins et contraintes d'un projet. Il peut être fourni ou non au début du projet... S'il n'est pas fourni il est recommandé de le rédiger, car c'est le document de référence qui cadre le projet, il fait office de contrat entre le client et l'équipe de développement.

Il _doit_ contenir :
- La présentation du projet : objectif(s), acteurs, ...
- Le périmètre fonctionnel : description des fonctionnalités attendues et des limites du développement.
- Les contraintes fonctionnelles et techniques : budget, délais, contraintes d'accessibilité, description de l'existant.

Il _peut_ contenir :
- La charte graphique à respecter.
- Les règles de gestion (description détaillée du fonctionnement de l'organisation).
- Toute autre information préalable nécessaire au projet.

S'il vous manque des informations => [Checklist de questions à poser pour guider l'expression des besoins](https://docs.google.com/a/oclock.io/document/d/1n_vmM3lJ3LcoNW6vDHg8DYsF64holkcJk-W6v_aKjCo/edit?usp=sharing)

#### Quelques exemples
Modèles de cahier des charges d'agences web, à remplir par le client (plus élaborés/complexes) :
- [MM Création](http://www.mmcreation.com/_doc/mmcreation-cahier-des-charges.pdf)
- [Petite fabrique du web](http://www.petitefabriqueduweb.com/fichiers/Cahier_des_charges_creation_site_internet.pdf)
- [Autres exemples de CDC](exemples-cdc/)

Exemple de CDC rédigé pour un appel à projet :
- https://fr.scribd.com/doc/12979924/Exemple-de-Cahier-Des-Charges

### Spécifications
Les spécifications contiennent toutes les informations nécessaires au développement. C'est l'équipe de développement qui les rédige pendant la conception de l'application.

#### Spécifications fonctionnelles

Une spec fonctionnelle est une description détaillée des scenarios d'utilisation d'une partie du site.

On utilise plusieurs outils pour créer une spec fonctionnelle.

##### Fonctionnalités et autorisations : *use-cases*

Un use-case (cas d'usage === fonctionnalité) décrit un usage particulier du système, généralement quelque chose de fondamental, à forte valeur ajoutée — en gros, une fonctionnalité importante du projet.

*Ex. **Commander sur le site** — Un achat est effectué par un client, ce qui donne lieu à livraison des produits.*

##### Scénarios : *user stories*

Un use-case doit être précisé par des scénarios alternatifs. Que se passe t-il si quelque chose cloche pendant le déroulé de la fonctionnalité ? Que se passe t-il si tout va bien ? Y a t-il une seule façon d'utiliser la fonctionnalité ? Etc. À chaque variante correspondra une user-story, écrite avec la structure suivante :

> "En tant que ... je veux ... pour ..."

*Ex. : **En tant** qu'employé de la librairie, **je veux** pouvoir consulter le stock de livres par référence, par auteur ou par titre, **pour** pouvoir renseigner les usagers qui viennent me demander un livre en particulier.*

*Ex. : **En tant** que responsable informatique, **je veux** pouvoir suspendre un accès utilisateur, **pour** garantir la sécurité de l'application suite à un comportement non désiré de cet utilisateur.*

##### Description de l'interface : *wireframes*

Un wireframe n'est pas une maquette graphique. On formalise simplement l'agencement des blocs de contenus et leurs relations, sans définir l'aspect visuel.

Outils classiques : [Creately](https://creately.com/), [Pencil Project], [Draw.io](https://www.draw.io/), [Wireframe.cc](https://wireframe.cc/), [MockFlow](https://www.mockflow.com/), [Balsamiq](https://balsamiq.com/), [Sketch](https://www.sketch.com/), [Whimsical](https://whimsical.com/wireframes/), [Adobe XD](https://www.adobe.com/fr/products/xd/wireframing-tool.html)…

##### Les règles de gestion

Aussi appelées « règles métier », elles cadrent les fonctionnalités. On les retrouve souvent intégrées en complément du document des use-cases, sauf s'il y en a vraiment beaucoup, auquel cas on fait des annexes dédiées.

*Ex. : Un abonné ne peut emprunter plus de 2 DVD en même temps.*

#### Spécifications techniques

On y trouve notamment :

- La description précises des données manipulées : *dictionnaire de données, MCD, MLD, MPD* (cf. [méthodologie/exemple pour concevoir une base de données relationnelle](conception-bd.md))
- L'architecture logicielle choisie : *outils/librairies, organisation des fichiers, …*

### Modéle OpQuast VPTCS

Il peut être intéressant de replacer la gestion de projet au sein du [modèle VPTCS d'OpQuast](../seo/opquast.md), pour cadrer la qualité en projet web.