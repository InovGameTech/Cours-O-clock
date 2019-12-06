# Modules JS

## Utilité d'un module

Un programme s'organise naturellement en thématiques : gérer un compte utilisateur, afficher des notifications à l'écran, réaliser un calcul de score dans un jeu, etc. Pour gagner en lisibilité, faciliter l'évolution du code et éviter les conflits de nommage, chaque thématique peut être isolée des autres grâce à un module.

L'application JS en entier peut également être considérée comme étant un module en soi (une page web pouvant très bien faire intervenir plusieurs applications JS).

## Créer un module

Il existe plusieurs manières de formaliser un module dans le code. La plus simple consiste à utiliser un objet.

Un objet JS peut contenir des clés, auxquelles sont associées des valeurs. Ces valeurs peuvent être de n'importe quel type (`number`, `string`, etc.), y compris des `function`. Ces fonctions peuvent alors être appelées, comme n'importe quelle autre fonction.

> Quand une valeur est d'un type autre que `function`, on parle de *propriété* de l'objet ; quand une valeur est une `function`, on parle de *méthode* de l'objet.

Une bonne pratique pour structurer son code consiste à rassembler les variables (propriétés) et fonctions (méthodes) qui ont trait au même sujet dans un objet, qu'on considère être un module.

``` js
// Exemple de module :
var module = {
  propriete: 'Valeur',
  methode: function() {}
};
```

Pour une application JS, et par convention, on aura tendance à nommer le module `app`, et à y inclure une méthode `init()` qui sert de « point d'entrée » dans le module : `init` contient tous les traitements qui « lancent » l'application, par exemple initialiser les valeurs, les écouteurs d'évenements, lancer un timer, etc.

```js
// Exemple d'application :
var app = {
  init: function() {
    console.info('Initialisation');
    app.name = 'Big Brother';
    app.ecouterEvenements();
  },
  
  ecouterEvenements: function() {
    window.addEventListener('click', app.reagir);
  },
  
  reagir: function() {
    console.log(app.name + ' > ' + 'un clic est survenu');
  }
};

// On lance l'application :
app.init(); // dans l'objet `app`, on exécute la fonction (méthode) stockée dans la clé `init`

```

> Il est courant d'associer l'exécution du point d'entrée `init` à un écouteur d'événement sur le chargement du `DOM` :
>
> ``` js
> // Une fois le DOM chargé, la méthode init de l'objet app est exécutée :
> document.addEventListener('DOMContentLoaded', app.init);
> ```
>
> Cette façon de faire n'est pas obligatoire : si vous placez le chargement du `<script>` en bas du `<body>`, il n'y a pas besoin de le faire !