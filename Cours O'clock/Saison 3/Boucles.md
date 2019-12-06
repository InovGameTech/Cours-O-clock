# Boucles

Toutes les boucles en JS se basent au minimum sur :

- une condition de répétition (on dit aussi « de sortie ») ;
- des instructions à répéter ;

et éventuellement sur :

- une gestion fine de la condition de sortie, avec par exemple un compteur numérique (par exemple, boucle `for`).

## while

[[MDN] while](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/while)

**Tant que** la condition est vérifiée, j'exécute les instructions :

```js
while(condition) {
  // ... instructions JS
}
```


## do...while

[[MDN] do...while](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/do...while)

J'exécute les instructions une première fois, puis **tant que** la condition est vérifiée, je recommence :

```js
do {
  // ... instructions
} while(condition)
```

## for

[[MDN] for](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/for)

**Pour** chaque nouvelle valeur de ma variable de contrôle de boucle, et ce jusqu'à ce que la condition ne soit plus vérifiée, j'exécute les instructions :

```js
for(var i = 0; i < 3; i++) {
  // ... instructions
}
```

Ici, la variable `i` (comme *increment*) sera incrémentée de 1 à chaque itération, et la condition ré-évaluée à chaque tour de boucle, jusqu'à ce qu'elle ne soit plus vérifiée et que la boucle s'arrête.

## for...in

[MDN for...in](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Instructions/for...in)

**Pour** chaque proprieté **dans** l'objet, j'exécute les instructions :

```js
var fruit = {
  nom: 'fraise',
  couleur: 'rouge'
};

for(var propriete in fruit) {
  console.log('Propriété ' + propriete + ' :');
  console.log('Le fruit est ' + fruit[propriete]);
}

// Affichage obtenu en console :
//
// Propriété nom :
// Le fruit est fraise
// Propriété couleur :
// Le fruit est rouge
```

> **NOTES**
> - Il est possible d'interrompre une boucle avec l'instruction `break;`.
> - Il est possible d'interrompre l'itération courante et de passer à la suivante avec l'instruction `continue;`.