# Événements

JavaScript est un langage tourné vers la gestion des interactions entre l'utilisateur et le navigateur. Cliquer, scroller, soumettre un formulaire, etc. sont des événements utilisateurs, auxquels le développeur peut associer du code pour décrire ce qui devrait s'exécuter si un tel événement survient.

## addEventListener

[[MDN] addEventListener](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)

Permet de créer un écouteur d'événement, c'est-à-dire une fonction qui va permettre d'indiquer au navigateur comment réagir à des événements futurs d'un certain type. Schématiquement :

```js
element.addEventListener(
  eventType,
  handler
)
```

où :

- `element` est une référence vers un nœud du [DOM](dom.md), obtenue auparavant ;
- `eventType` est une chaîne de caractère décrivant le type d'événement à surveiller, sur `element` ;
- `handler` est une fonction anonyme (`function() { … }`) ou une référence de fonction (le nom d'une fonction existante).

Exemple :

``` js
// Au clic sur un bouton d'inscription, on déclenchera un comportement précis.

// Sélection de l'élément HTML concerné par l'événement (ici, clic sur un bouton #inscription).
var element = document.getElementById('inscription');

// Définition du handler de l'événement clic.
var subscribeUser = function() {
  // TODO: enregistrer l'inscription de l'utilisateur
};

// Raccordement entre l'élément et le handler, via l'événement de type 'click'.
element.addEventListener('click', subscribeUser);
```

### Objet-événement

Le handler, aussi appelé callback ou écouteur d'événement (_event listener_), est une fonction qui sera automatiquement appelée par le navigateur en réaction à un événement précis.

Ce handler recevra en paramètre [un objet décrivant l'événement survenu](https://developer.mozilla.org/fr/docs/Web/API/Event) :

``` js
// Exemple de handler acceptant un paramètre pour récupérer l'objet-événement :
var subscribeUser = function(evt) {
  console.log(evt);
  // TODO: enregistrer l'inscription de l'utilisateur
}
```

L'objet-événement contient de nombreuses informations utiles, et notamment une [méthode `preventDefault`](https://developer.mozilla.org/fr/docs/Web/API/Event/preventDefault) qui permet, lorsque c'est utile, de bloquer le comportement par défaut du navigateur :

``` js
document.getElementByTagName('form').addEventListener('submit', function(evt) {
  evt.preventDefault(); // empêche le rechargement automatique de la page
});
```

> Cas d'usage typique : empêcher le rechargement de la page lors de la soumission de formulaires, ce qui est normalement le comportement par défaut des navigateurs du marché.

## Plus en détails

### Types d'événements

[[MDN] Liste des types d'événements](https://developer.mozilla.org/en-US/docs/Web/Events)

Il existe de nombreux types d'événements auxquels réagir. Il est même possible de créer ses propres types avec [`new Event('montype')`](https://developer.mozilla.org/fr/docs/Web/Guide/DOM/Events/Creating_and_triggering_events).

### Handler et traitement d'informations

Un événement, par exemple un `'click'` sur un `.button`, peut survenir _plusieurs fois_. La fonction handler est définie _une seule fois_ mais sera executée à chaque occurence de l'événement, et comme pour toutes les fonctions en JS, il n'y a aucune persistance d'information entre les différents appels. Il convient donc de coder ses handlers de façon à ce qu'ils soient autonomes dans leurs traitements d'information, c'est-à-dire ne dépendent pas des occurences précédentes ou d'informations tierces non-fiables dans le temps.

Le handler peut recevoir un objet-événement en paramètre, il sera généralement nommé `event` ou `evt`. Cet objet est automatiquement rempli avec des informations diverses sur l'événement auquel le handler est entrain de réagir. Il n'est pas possible de personnaliser cet objet.

L'objet-événement donne accès à une référence vers l'élément du DOM qui a subit l'événement : `evt.target`. Cet élément du DOM peut notamment tout à fait exploiter les [attributs `data-`](https://developer.mozilla.org/fr/docs/Apprendre/HTML/Comment/Utiliser_attributs_donnes) pour transmettre des informations spécifiques du HTML vers le JS, informations exploitables dans le handler.

### Supprimer un écouteur d'événement

Pour retirer un écouteur d'événement d'un élément HTML, il faut préciser l'élément en question, le type d'événement et le handler :

```js
bouton.removeEventListener('click', cliqueBouton);
```