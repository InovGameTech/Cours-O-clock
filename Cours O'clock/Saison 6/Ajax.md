# ![ajax](https://upload.wikimedia.org/wikipedia/commons/thumb/0/04/Ajax_logo.svg/175px-Ajax_logo.svg.png)

## AJAX, c'est quoi ?

> Les sprays nettoyants ou autres détergents ne seront pas évoqués ici...

**AJAX** ou Asynchronous JavaScript And XML est un terme qui s'est démocratisé grâce à cet [article](http://adaptivepath.org/ideas/ajax-new-approach-web-applications/) de Jesse James Garrett en 2005.

C'est une autre approche, une autre architecture particulièrement adaptée aux applications web.

### Un peu d'histoire

- 1996 - JavaScript est ajouté au navigateur Netscape
- 1998 - Le Document Object Model (DOM)  
- 1998 - Microsoft créer XMLHTTP, un composant ActiveX pour Internet Explorer 5.
- 2002 ~ 2005 - Ajouté à la norme ECMAScript relative au langage JavaScript, XMLHttpRequest est mit en oeuvre sur la plupart des navigateurs (Mozilla, Safari, Opéra ...).
- 2005 - Article de Jesse James Garrett qui démocratise le terme et l'approche `AJAX`
- 2006 - XMLHttpRequest (xhr) devient une recommandation du [W3C](https://www.w3.org/TR/2006/WD-XMLHttpRequest-20060405/)
- 2012 - XMLHttpRequest Level 2 élaborée par le [W3C](https://www.w3.org/TR/XMLHttpRequest2)
- 2014 - [whatwg](https://xhr.spec.whatwg.org/) continue le travail autour de xhr

### L'approche classique

La plupart des actions effectuées par un utilisateur déclenche une requête HTTP vers un serveur web. Ce serveur effectue nombre d'opérations, decomposer la requête, appeler les services nécessaires, retrouver des données et suite à ce processus, retourner une page HTML à l'utilisateur.

Ce fonctionnement est adapté pour une consultation "classique" de contenus mais pas forcément pour des applications web.

### Une autre approche

Dans l'article de Jesse James Garrett, AJAX y est décrit non pas comme une technologie mais bien comme une association de plusieurs technologies, une nouvelle façon de penser l'architecture d'une application web :

- Présentation | HTML / CSS
- Interaction | DOM
- échange et manipulation de données | XML
- Récupération asynchrone de données | [XMLHttpRequest](http://www.xml.com/pub/a/2005/02/09/xml-http-request.html)
- Liaisons et assemblage | JavaScript


En comparant une application web classique et en AJAX il est plus simple de saisir les subtilités.

![web app ajax](img/web-app-ajax.png)
> Schéma inspiré de celui proposé par Jesse James Garrett

## Synchrone contre asynchrone

La différence principale entre synchrone et asynchrone est que chaque action d'un utilisateur qui devrait normalement générer une requête HTTP (synchrone) prendra à la place la forme d'un appel JavaScript au moteur AJAX (asynchrone). Chaque réponse à une action utilisateur ne nécessite donc pas d'attendre une réponse du serveur.

Le moteur AJAX prendra en charge les actions utilisateurs et il se chargera de récupérer les données nécessaire, si il en a besoin. Le moteur fait donc des requêtes asynchrones sans obliger l'utilisateur à subir un changement d'état complet de l'application à chacune de ses actions.

![web app ajax](img/web-app-async.png)
> Schéma inspiré de celui proposé par Jesse James Garrett

### Exemple : Le lazy loading

[Smashing Magazine](https://www.smashingmagazine.com/) (synchrone) VS [Twitter](https://twitter.com/) (asynchrone)

## Ajax avec jQuery

[`jQuery.ajax()`](https://api.jquery.com/jQuery.ajax/)

### Étape 1 : Création d'une requête

**Juste l'objet XHR**

```javascript
var xhr = $.ajax();
```

**Une requête complète**

```javascript
var xhr = $.ajax('demo.php');
```

Il est possible de passer plusieurs options

```javascript
var xhr = $.ajax('demo.php', { method: 'POST' });
```

```javascript
var dataToPost = {id: 10};
var xhr = $.ajax('demo.php', { method: 'POST', data: dataToPost });
```

### Étape 2 : Agir en fonction du retour serveur

```javascript
// En cas de succes
xhr.done(function(data){
  console.log(data); // Les données retournées sont accessibles via 'data'
});

// En cas d'échec
xhr.fail(function(){});

// Dans tous les cas
xhr.always(function(){});
```

## Quelques astuces et outils

### Rendre un formulaire exploitable en AJAX très rapidement avec jQuery

**Sous forme d'un chaîne de caractères** avec [`.serialize()`](https://api.jquery.com/serialize/)
```javascript
$('form#contact').serialize();
```

**Sous forme de tableau** avec [`.serializeArray()`](https://api.jquery.com/serializeArray/)
```javascript
$('form#contact').serializeArray();
```

### Bloquer les requêtes autres que via AJAX en PHP

La super globale [`$_SERVER`](https://secure.php.net/reserved.variables.server) contient beaucoup d'informations très interessante sur le serveur et les headers d'une requête

Une fonction bien utile s'appuyant sur `$_SERVER` pour définir si une requête est effectuée en AJAX

```php
function isAjax() {
  return isset($_SERVER['HTTP_X_REQUESTED_WITH']) && strtolower($_SERVER['HTTP_X_REQUESTED_WITH']) === 'xmlhttprequest';
}
```

### Envoyer un [header](https://secure.php.net/manual/fr/function.header.php) d'erreur en PHP


```php
header($_SERVER['SERVER_PROTOCOL'] . ' 500 Internal Server Error', true, 500);
```

### Nettoyer une chaîne de caractères en PHP

Une petite fonction intéressante pour nettoyer efficacement une chaîne avec [`trim`](https://secure.php.net/manual/fr/function.trim.php), [`strip_tags`](https://secure.php.net/manual/fr/function.strip-tags.php) et [`htmlspecialchars`](https://secure.php.net/manual/fr/function.htmlspecialchars.php)

```php
function sanitize($str){
  return htmlspecialchars(strip_tags(trim($str)));
}
```

Une autre option intéressante, mais avec [quelques subtilités](https://secure.php.net/manual/fr/filter.filters.sanitize.php) à prendre en compte

```php
filter_var($str, FILTER_SANITIZE_STRING);
```


## Comprendre XMLHttpRequest

> The Hard Way

[XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) est un objet sur lequel repose l'architecture AJAX.

### Étape 1 : Création de l'objet XHR

```javascript
var xhr = new XMLHttpRequest();
```

L'objet possède une longue liste de propriétés et méthodes (consultable sur [MDN](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) ou [Devdocs.io](https://devdocs.io/dom/xmlhttprequest))

À noter que la syntaxe au-dessus est vrai pour la plupart des navigateurs, toutefois pour les navigateurs plus anciens il faudra passer par une syntaxe plus complexe.

```javascript
function createXhrObject() {
  if (window.XMLHttpRequest)
    return new XMLHttpRequest();

  if (window.ActiveXObject) {

    var names = [
      "Msxml2.XMLHTTP.6.0",
      "Msxml2.XMLHTTP.3.0",
      "Msxml2.XMLHTTP",
      "Microsoft.XMLHTTP"
    ];

    for(var index in names) {
      try{
        return new ActiveXObject(names[index]);
      }
      catch(err){}
    }

  }

  window.alert("XMLHttpRequest n'est pas pris en charge.");

  return null; // non supporté
}

var xhr = createXhrObject(); //Objet XMLHttpRequest ou null
```

### Étape 2 : Écouter les changements de statut de l'objetXHR


```javascript
xhr.onreadystatechange = function(evt) {
  console.log(this.readyState);
  if (this.readyState == 4 ) {
    console.log(this.responseText);
  }
};
```

### Étape 3 : Initialiser une requête de l'objet XHR vers le serveur

`open('methode', 'destination', asynchrone ou non)`

```javascript
xhr.open('GET','demo.php', true);
```

### Étape 4 : Effectuer la requête

```javascript
xhr.send();
```