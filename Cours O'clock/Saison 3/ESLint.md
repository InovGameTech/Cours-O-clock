# ESLint

L'idée est d'avoir un assistant qui vérifiera la syntaxe utilisée lors de l'écriture d'un fichier JavaScript, afin de s'assurer du respect des bonnes pratiques, tout en nous aidant a améliorer notre code au fur et à mesure de l'avancée du développement.

[ESLint](https://eslint.org/) est un outil indépendant, et les éditeurs de textes utilisent le plus souvent un plugin pour l'intégrer directement.

## Fichier de configuration `.eslintrc`

Le fichier caché `.eslintrc` va contenir une configuration pour votre projet.

### Exemple de configuration

```json
{
  "env": {
    "browser": true
  },
  "extends": "eslint:recommended",
  "rules": {
    "indent": ["error", 2],
    "quotes": ["error", "single"],
    "semi": ["error", "always"],
    "no-console": "off",
    "eqeqeq": "warn"
  }
}
```

ESLint connaît des centaines de règles syntaxiques et de bonnes pratiques. Dans cet exemple, nous nous appuyons sur un corpus déjà existant, `eslint:recommended`, mais en le personnalisant pour notre usage (en ajustant certaines des *rules*).

Il est possible de configurer ESLint très précisement *via* une multitude de règles. Le site d'[ESLint](http://eslint.org/docs/rules/) fourni une documentation très claire au sujet de chacune d'entre elles.

Certains outils ou librairies très populaires sont même directement supportées par ESLint. Par exemple, pour prendre en compte les spécificités syntaxiques liées à l'utilisation de jQuery, on ajoutera `"jquery": true` dans `"env"` :

```
"env": {
    "browser": true,
    "jquery": true
},
```

## Désactiver à la volée

Parfois, en particulier quand on a une configuration avancée,
il sera pratique de pouvoir désactiver temporairement et à la volée les règles ESLint, pour une ligne spécifique par exemple.

Par exemple, si on veut exceptionnellement utiliser `==` au lieu de `===` :

```js
// eslint-disable-next-line
if (x == null) {
  // ...
}
```

Pour voir tous les commentaires possibles, c'est par ici :  
→ https://eslint.org/docs/user-guide/configuring#disabling-rules-with-inline-comments


## En ligne de commande

### En global

Vous pouvez installer ESLint en global :
```shell
# Npm
[sudo] npm install --global eslint

# Yarn
[sudo] yarn global add eslint
```

Vous pouvez alors utiliser la commande suivante pour vérifier les erreurs dans un fichier :

```shell
eslint monfichier.js
```

Vous pouvez également passer en argument un dossier entier ! Par exemple, si vous êtes à la racine de votre projet, vérifiez tous vos fichiers d'un coup en passant le *dossier courant* `.` :

```shell
eslint .
```

On peut également utiliser l'option `--fix` pour résoudre automatiquement certaines erreurs triviales, comme les problèmes de quotes ou points-vigules.

Par exemple : `console.log("hello world")` => `console.log('hello world');`

### Au sein d'un projet

On peut installer ESLint localement, dans notre projet :

```shell
# Npm
npm install --save-dev eslint

# Yarn
yarn add --dev eslint
```

Si vous avez installé ESLint en local dans votre projet de cette manière, utilisez la version locale pour lancer `eslint` :

```shell
./node_modules/.bin/eslint .
```

Pour plus de simplicité, on peut également s'en faire un script. En effet, le dossier `./node_modules/.bin` est ajouté au `$PATH` lorsque l'on utilise un script npm.

```json
{
  "scripts": {
    "lint": "eslint ."
  }
}
```

Il suffira ensuite d'utiliser ce script :

```shell
# Npm
npm run lint

# Yarn
yarn lint
```

## Intégration aux éditeurs de texte

L'intégration d'ESLint à Atom, Visual Studio Code, Sublime Text, etc. nécessite d'installer le programme `eslint` et un plugin pour le raccorder à l'éditeur de texte.

Pour simplifier cette procédure, on va mettre en place une configuration par défaut globale.

L'exemple ci-dessous permet de faire travailler ESLint sur des projets ES6+ et Node.js :

``` sh
[sudo] npm install -g eslint
# On utilise dans cet exemple une configuration "Standard" pour ESLint :
[sudo] npm install -g eslint-config-standard eslint-plugin-standard
[sudo] npm install -g eslint-plugin-promise eslint-plugin-import eslint-plugin-node
```

Il faut ensuite installer le plugin requis pour votre éditeur de texte :

* [plugin ESLint pour VSCode](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

Enfin, il faut fournir une configuration .eslintrc globale, enregistrée dans \~/.eslintrc (\~ représentant votre dossier personnel, /home/[votre_identifiant]) :

``` js
{
  "env": {
    "browser": true,
    "es6": true
  },
  "extends": "standard",
  "rules": {
    "semi": ["error", "always"],
    "space-before-function-paren": ["error", {
      "anonymous": "never",
      "named": "never",
      "asyncArrow": "always"
    }],
    "quotes": ["error", "single"],
    "no-console": "off",
    "eqeqeq": "warn"
  }
}
```

Désormais, les fichiers .js bénéficieront automatiquement de l'aide d'ESLint.