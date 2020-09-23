# Problématiques serveur

## Apache

Pour que votre fichier PHP soit bien interprêté, il est obligatoire de placer
votre projet dans le dossier lu par Apache :

* Sur le téléporteur, il s'agit de `/var/www/html`.

* Pour ceux qui sont sous MAMP (ou similaire), il s'agit du dossier `htdocs`.  
Sous macOS : `/Applications/MAMP/htdocs`

## Cache

Attention, quand on travaille dans un contexte client / serveur, le navigateur
n'a pas de moyen de savoir si le serveur est un serveur local ou distant. Il va
donc se comporter comme sur un site classique, et va potentiellement mettre en
cache vos assets, c'est-à-dire vos fichiers statiques (CSS, JS, images).

### Recharger en vidant le Cache

On peut forcer le navigateur à recharger la page en vidant le cache :

* Sur le téléporteur : `Ctrl + F5`

* Sous macOS : `Cmd + shift + R`

### Désactiver le cache

On peut aussi directement désactiver le cache du navigateur.

![disable cache](https://i.stack.imgur.com/Grwsc.png)

Plus d'infos par ici : http://stackoverflow.com/questions/5690269/disabling-chrome-cache-for-website-development