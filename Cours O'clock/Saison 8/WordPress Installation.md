# WordPress : Installation classique

## Prérequis

LAMP/ WAMP / config serveur perso

* Apache
* PHP
* MySQL

## Récupérer WordPress

* [WordPress](https://wordpress.org/)
* [WordPress FR](https://fr.wordpress.org/)

## Préparer la BDD

phpMyAdmin : Création d'un utilisateur base de données dédiée avec privilèges

## Suivez le guide

wp-admin > étapes d'installation
pas "admin", mot de passe sécurisé, accès

## Réglages WordPress

Pas d'indexation

## Permaliens

Activation des permaliens

### .htaccess

```
RewriteEngine on
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . index.php [L]
```

## Droits de fichiers

le groupe apache doit être déclaré

`<user>` : Votre utilisateur courant

à la racine du projet :

**sur mac**

```bash
sudo chown -R <user>:_www .
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 644 .htaccess
```

> :bulb: Il est également possible que sous Mac, Apache soit executé par l'utilisateur `daemon`. Dans ce cas, remplacer `_www` par `daemon`.

**sur linux**

```bash
sudo chown -R <user>:www-data .
sudo find . -type f -exec chmod 664 {} +
sudo find . -type d -exec chmod 775 {} +
sudo chmod 644 .htaccess
```

[Article du codex sur les droits de fichiers](https://codex.wordpress.org/Changing_File_Permissions)

## Traduction

* [Traduction FR Glotpress](https://translate.wordpress.org/locale/fr) - The Hard Way
* [WPcentral Traduction FR](https://wpcentral.io/internationalization/fr/) - C'est déjà mieux mais...
* [wp-config.php](wp-config.md) => FS_METHOD 

