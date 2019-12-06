# Scrum

Scrum (signifiant une _mélée_ de Rugby), basé sur les principes agiles, est une méthode de gestion de projet ou plus exactement un cadre de développement.

Ainsi le [Scrum framework](https://www.scrum.org/resources/what-is-scrum) est appellé [](https://www.scrum.org/)

## Le concept

Des équipes pluridisciplinaires et auto-organisées réalisent des produits de manière itérative et incrémentale.

Scrum strucutre le développement en cycles de travail appelés **Sprint**. Ces cycles durent entre 1 et 4 semaines (en général 2 semaines) et s'enchaînent les uns après les autres.

Un sprint commence et fini à une date précise que le travail prévu soit achevé ou non. Les sprints ne sont jamais prolongés.

Avant chaque sprint, une réunion entre le chef de projet (Scrum master) et l'équipe se tient afin de déterminer les tâches (demandes) tangiblement terminables durant le sprint à venir. L'idée étant de pouvoir fournir / achever des fonctionnalités pouvant être "livrables". Suite à cette réunion, le sprint suivant ne recevra plus de nouvelles tâches.

Durant chaque sprint, l'équipe se réunit brièvement (10-15min) tous les jours afin de s'assurer de la progression, d'ajuster les prochaines étapes, de relever d'éventuels points bloquants.

Après chaque sprint, l'équipe présente le résultat de leur travail afin qu'il soit intégré au projet.

![Scrum](img/scrum.png) _issu de_ [scrum.org](https://www.scrum.org/)

### Ressources externes

- https://www.scrum.org/
- https://www.scrumalliance.org/why-scrum : lire "The SCRUM framework in 30 seconds"
- https://www.mountaingoatsoftware.com/agile/scrum/scrum-tools/task-boards
- Super guide en français : https://www.scrumguides.org/docs/scrumguide/v2017/2017-Scrum-Guide-French.pdf

2 vidéos :
- https://www.scrumalliance.org/learn-about-scrum (1m30)
- https://www.mountaingoatsoftware.com/presentations/an-introduction-to-scrum (1h)

## Les rôles

### Product owner

- Responsable du "produit"
- Expert métier
- Représente le client (enjeux, intérêts, priorités)
- S'assure du ROI (retour sur investissement)

### Scrum master

- Facilitateur du projet
- Responsable projet
- Assure le respect de Scrum (sprint, tâches, responsabilités, ...)
- Ne peut pas être le Product owner

### Équipe

- Pluridisciplinaire / plurifonctionnelle
- Construit le produit
- Les membres travaillent **ensemble**, objectif commun
- Analyste, concepteur, architecte, développeur, ...

## Les composants

### Product Backlog

Le Product Backlog centralise la liste de tout ce qui doit être fait.

Le Product Backlog est une feuille de route, il evolue tout au long de la vie du produit.

C'est donc un document central, maintenu par le Product owner, qui sert de référenciel durant tout le projet.

Bien que fréquent composé par des user-stories, la forme des éléments du PB ont peu d'importance tant que leur signification et leur implication sont claire.

Il ressemble généralement à ceci :

| Priorité | Élement                              | Détails | Effort | Sprint |
| -------- | ------------------------------------ | ------- | ------ | ------ |
| 1        | En tant que ... je veux ...          | ...     | 5      | 1      |
| 2        | Amélioration des performances de ... | ...     | 13     | 3      |
| 3        | Mise à jour des serveurs ...         | ...     | 8      | 1      |
| 4        | En tant que ... je veux ...          | ...     | 21     | 2      |
| ...      | ...                                  | ...     | -      | -      |

Un Product Backlog doit être **DEEP**

- **Détaillé** : Les éléments prioritaires sont très détaillés (très fins). Généralement le top 15 du PB doit être composé d'éléments de petite taille (temps de réalisation) afin d'être réparti facilement sur les sprints à venir
- **Estimé** : Les éléments doivent être estimés, l'effort : (difficultés, temps de production, risques).
- **Evolutif** (ou Emergent) : Le PB est continuellement en mutation, il évolue. Le Product owner doit prendre en compte les difficultés techniques, les impératifs, les temps, les nouvelles demandes, ...
- **Priorisé** : Il est crucial que le PB contiennent des éléments priorisés afin de dresser un schéma respectant le "Plus pour votre argent" = grande valeur métier / faible coût de production. Ce principe peut être outrrepasser par la gestion de l'urgence (sécurité, visibilité, etc...)

### Sprint Backlog

Le Sprint Backlog est le doc de regroupant l'ensemble des éléments du PB (Product Backlog) identifiés / choisis pour le sprint

Ce Sprint Backlog ne change pas durant le sprint.

Le processus de construction du doc peut être le suivant

```
En tant que client je veux ajouter un produit au panier

TODO

- Modifier la base de données
- Créer la page (UI)
- Créer la page (JS)
- Écrire les tests
- Mettre à jour la page d'aide utilisateur
- ...
```

## Les phases

### Sprint planning

Planification du sprint avec les items à réaliser

Cette réunion rassemble tous les membres de l'équipe, le PO et le Scrum Master

Cette réunion ne peut excéder 1 journée au maximum.

Pour estimer l'effort à investir, l'une des techniques est le *planning poker*

#### Planning Poker

- Permet de déterminer la complexité d'une tâche de façon ludique
- La complexité est définie par l'ensemble de l'équipe
- Amène un échange entre les différents intervenants
- Plus la tâche est longue ou complexe, moins la mesure est précise

##### Déroulement

Jeu de cartes - S'appuyant fréquement sur la suite de fibonacci

Cartes
- 1
- 2
- 3
- 5
- 8
- 13
- 21
- 34
- 55
- 89
- ?

Étape préalable : on prend une tâche évidente pour l'estimer afin d'avoir un référentiel.

Ensuite, pour chaque tâche :

1. Le PO explique la tâche
2. Chacun choisit une carte et la pose face cachée
3. Les cartes sont toutes retournées en même temps
4. Si tout le monde est d'accord, on choisit cette mesure, sinon les extrêmes expliquent les raisons de leur choix
5. On revient à l'étape 2 jusqu'à l'unanimité

##### Démarche empirique

- Les nombres sont des points récits dont la correspondance en jour homme varie selon l'équipe et les projets
- Il faut comparer avec d'autres tâches de niveau semblable pour avoir une idée de la difficulté
- Une démarche adaptable selon les équipes et entreprises

### Daily Scrum

Réunion debout d'une 15aine de minutes, animée par le Scrum Master.

Chaque participant expose 3 points :
- Ce qu'il a fait la veille
- Ce qu'il va faire aujourd'hui
- Les éventuels points bloquant qu'il rencontre

### Sprint review

Réunion de fin de sprint : entre 30 et 60 minutes

Participants : Equipe, PO, SM

- Objectifs : Rappels des objectifs du sprint (roadmap, étapes, ...)
- Statut : Items planifiés, achevés ou non, changement de priorité, ...
- Démo : Démo de quelques fonctionnalités, feedback
- Stats : Statistiques du sprint (efficacité, retard / avance)
- BLocage : Éventuels points bloquants, risques découverts pendant le sprint
- Feedback : Retour sur le sprint écoulé et quelques infos sur le sprint suivant

### Sprint retrospective

Réunion de fin de sprint : environ 1h

Participants : Equipe, PO, SM

- Prévision : Le sprint s'est passé comme ça... que faut-il prévoir pour les suivants ?
- Processus : Le process est le suivant... qu'est ce qui peut être amélioré  (communication, docs, infos)
- Stats : Les stats ont montré une situation... va t-elle durer, s'améliorer, empirer ?

## Les outils

### Burndown chart

- Lecture sur wikipédia : [Burndown chart](https://fr.wikipedia.org/wiki/Burndown_chart)
- http://www.agilenutshell.com/burndown


### Kanban

Kanban est un système utilisé afin de limiter les tâches en cours. [Wikipédia](https://fr.wikipedia.org/wiki/Kanban_(d%C3%A9veloppement)).

Kanban en ligne :

- La référence, Trello : https://trello.com
- github projects (présent sur les repo)
- Un équivalent Open Source, français, dont la documentation est pertinente : https://kanboard.net/fr
- Une autre alternative : https://taiga.io/

- Description ultra-simple d'un worflow Scrum avec Trello :
  - https://blog.hadrien.eu/2014/01/31/scrum-avec-trello/
  - https://trello.com/b/ultdy0tY/template-scrum-with-trello

[Ressources sur SCRUM/Trello](https://trello.com/b/VliA4Xzm/scrum)