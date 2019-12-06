# Ressources Apache

## Vérifier que les .htaccess sont interprétés

Si vous avez un doute sur l'activation des .htaccess, écrivez n'importe quoi dedans, cela doit générer une erreur 500.

Si vous n'avez pas d'erreur, c'est que le .htaccess n'est pas lu par le serveur. Pour corriger cela il faut modifier l'option AllowOverride dans la directive <Directory > :

    AllowOverride **All**

Pour l'activer dans tout votre répertoire web, modifiez-la directement dans `/etc/apache2/apache2.conf` au niveau de `<Directory /var/www/>` (ou équivalent en fonctoin de votre système).

## Rediriger toutes les requêtes vers index.php en utilisant .htaccess

Ce bout de code dans votre .htaccess vous permet de rediriger tout dossier ou fichier qui n'existe pas vers index.php :

    RewriteEngine on
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteRule . index.php [L]

### Détail du code

Ceci active le moteur de réécriture d'URL d'Apache :

    RewriteEngine on

Ceci vérifie que le dossier (-d) ou fichier (-f) n'existe pas (dans le cas contraire il affichera le dossier/fichier) :

    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteCond %{REQUEST_FILENAME} !-f

Et ceci redirige la requête vers index.php :

    RewriteRule . index.php [L]

### En cas d'erreur

Si cela ne marche pas, assurez-vous que l'extension _mod_rewrite_ pour Apache est activée. Sur un système Unix vous pouvez éxécuter cette commande pour l'activer, puis redémarrer Apache :

    sudo a2enmod rewrite
    sudo service apache2 restart

Source [https://gist.github.com/RaVbaker/2254618](https://gist.github.com/RaVbaker/2254618)