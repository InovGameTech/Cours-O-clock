# WordPress : wp-config.php

wp-config contient la configuration de WordPress

* Infos db
* salt
* configuration de debuggage
* ...

## Debug

Un fichier `debug.log` sera créé dans le répertoire `wp-content`

```php
define('WP_DEBUG', true);

if ( WP_DEBUG ) {
    define( 'WP_DEBUG_LOG', true );
    define( 'WP_DEBUG_DISPLAY', true );
}
```
Pour aller plus loin, le codex propose un [article](https://codex.wordpress.org/fr:D%C3%A9bogage_dans_WordPress) sur le debug dans WordPress

### no-white-screen

un `mu-plugin` très intéressant pour la gestion du debug : [no-white-screen](https://github.com/stracker-phil/wp-no-white-screen/)

### `error_log()`

Cette fonction permet d'écrire des messages dans le fichier `debug.log`. Il faut en abuser !

## Mode d'installation direct

Permet d'installer très simplement thèmes, plugins et langues

```php
define('FS_METHOD', 'direct');
```

## Désactivation de l'éditeur embarqué

```php
define( 'DISALLOW_FILE_EDIT', true );
```

## Désactiver l'installation de plugins ou themes

```php
define( 'DISALLOW_FILE_MODS', true );
```

## Génération d'image

```php
define( 'IMAGE_EDIT_OVERWRITE', true );
```

## Révisions

Par défaut révisions illimitées 

```php
// Désactivation totale = un peu brutal
define( 'WP_POST_REVISIONS', false );
// Plus intéressant
define( 'WP_POST_REVISIONS', 5 );
```

## Vider la corbeille des posts

Par défaut 30 jours

```
define( 'EMPTY_TRASH_DAYS', 10 );
```

## Cache

**Attention** SEULEMENT AVEC UN PLUGIN DE CACHE

```php
define( 'WP_CACHE', true );
```