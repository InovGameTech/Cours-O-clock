# php.ini

Pour configurer PHP sur sa machine, il faut modifier le fichier `php.ini`.

Il existe 2 fichiers `php.ini` :
- pour Apache (serveur Web)
- pour CLI (ligne de commande)

:warning: Attention, vous allez souvent voir des `;` en début de lignes, ce sont des **commentaires**

## Emplacements des fichiers

Pour localiser l'emplacement du fichier de `php.ini` pour le CLI : `php --ini`

### Sur le téléporteur

- Apache : `/etc/php/7.3/apache/php.ini`
- CLI : `/etc/php/7.3/cli/php.ini`

`7.3` est la version de PHP. Cette valeur peut donc évoluer dans le temps.

## Editeur

Pour modifier le contenu des fichiers `php.ini`, on va utiliser l'éditeur _VSCode_

- `sudo code /etc/php/7.3/apache2/php.ini`
- le mot de passe de votre user sera demandé (attention, aucune lettre ou * n'apparait quand on tape le mot de passe)
    - sur le Téléporteur, aucun mot de passe ne sera demandé
- faire de même avec le fichier CLI
- à la fin, on redémarre Apache pour qu'il prenne en compte les modifications
    - `sudo service apache2 restart`
    - s'il y a une erreur dans le fichier `php.ini`, la commande affichera une erreur et Apache ne sera pas démarré

## Activer les erreurs (mode développement)

Dans les 2 fichiers `php.ini`, effectuer les modifications suivantes :
- `display_errors=On` => rechercher `display_errors`
- `error_reporting=E_ALL` => rechercher `error_reporting`

## Migration de version de PHP

- [Modifier sa version de PHP](./config-migration.md)