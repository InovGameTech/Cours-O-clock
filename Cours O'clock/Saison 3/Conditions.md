# Conditions

---

## Condition `if`

### if

**Si** la condition est vérifiée, alors le bloc d'instructions associé est exécuté.

```
SI (condition) 
  ALORS Je fais qq chose
```

```js
if (condition) {
  // instructions si condition vérifiée
}
```

---

#### if...else

**Si** la condition est vérifiée, alors le premier bloc d'instructions est exécuté, **sinon** le deuxième bloc est exécuté.

```
SI (condition) 
  ALORS Je fais qq chose
SINON
  ALORS Je fais autre chose
```

```js
if (condition) {
  // instructions si condition vérifiée
}
else {
  // instructions si condition non vérifiée
}
```

---

### if...else if...else

- **Si** la 1ère condition est vérifiée, alors le premier bloc d'instructions est exécuté ;
- **sinon, si** la 2ème condition est vraie, alors le 2ème bloc est éxécuté (note : cette 2ème condition n'est testée que si la première est fausse) ;
- ... on peut mettre autant de `else if` qu'on veut (note : au bout d'un moment, ça devient compliqué/illisible ; on fera alors plutôt un `switch`) ;
- **sinon** si aucune des conditions précédentes n'est vraie, exécution du cas par défaut.

```
SI (la condition est vraie) 
  ALORS Je fais qq chose
SINON SI (la condition est vraie) 
  ALORS Je fais autre chose
SINON 
  ALORS Je fais autre chose
```

```js
if (condition1) {
  // instructions si condition 2 vérifiée
}
else if (condition2) {
  // instructions si condition 1 non vérifiée, et condition 2 vérifiée
}
else {
  // instructions si aucune condition vérifiée
}
```

---

## Conditions et booleéns

La structure de contrôle `if` attend une condition qui s'évalue à `true` ou `false` pour savoir si elle doit exécuter le bloc de code qui lui est associé.

```js
var confirmation = true;

if (confirmation === true) {
  // on passe ici !
}
```

est équivalent à :

```js
var confirmation = true;

// on peut directement utiliser la valeur booléene "confirmation" dans la condition
if (confirmation) {
  // on passe ici !
}
```

En résumé, une expression renvoyant un booléen, telle qu'un test d'égalité ou une valeur booléenne litérale, peut être directement utilisée comme condition.

Par exemple, si on possède une fonction `confirm` dont on sait qu'elle renvoie toujours un `booleen`, on peut l'utiliser comme suit :

```js
if (confirm('message de confirmation')) {
  // on passera ici si et seulement si l'appel à confirm a renvoyé true
}
```

---

## Condition `switch`

Cette structure de contrôle permet de spécifier un traitement différent selon la valeur d'une variable.

```js
var drink = 'coffee';

switch (drink) {
  case 'coffee':
    console.log('Expresso or Latte ?');
    break;
  case 'tea':
    console.log('Earl Grey or Green Tea ?');
    break;
  case 'soda':
  case 'water':
    console.log('Glass or bottle ?');
    break;
  default:
    console.log('Sorry, we don\'t have this here.');
}
```

Raccourci pour :

```js
if (val === 'val1') {
  // ...
} else if (val === 'val2') {
  // ...
} else {
  // ...
}
```