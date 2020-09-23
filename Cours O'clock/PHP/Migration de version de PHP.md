# Migration de version de PHP

> Les informations contenues ici permettent la migration de PHP 7.0 sur le téléporteur V4 (Ubuntu 16). Si vous souhaitez plus d'informations sur les migrations d'autres versions, [rendez-vous sur le tuto ThisHosting.Rocks](https://thishosting.rocks/install-php-on-ubuntu/)

## Migration de PHP 7.x à PHP 7.2

### Ajout du dépôt PHP

> Permet à voptre système d'aller chercher le paquet PHP 7.2, non fourni par Ubuntu 16.

```
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
```

Répondez _"Yes"_ ou _"Oui"_ quand le terminal vous pose des questions (le cas échéant essayez de comprendre ce qu'on vous raconte :wink:).

### Installation de PHP 7.2

```
sudo apt-get install php7.2
```

Vérifiez la bonne installation via : 

```
php -v
```

Cela doit indiquer quelque chose du genre : 
```
PHP 7.2.5-1+ubuntu16.04.1+deb.sury.org+1 (cli) (built: May  5 2018 04:59:13) ( NTS )
Copyright (c) 1997-2018 The PHP Group
Zend Engine v3.2.0, Copyright (c) 1998-2018 Zend Technologies
    with Zend OPcache v7.2.5-1+ubuntu16.04.1+deb.sury.org+1, Copyright (c) 1999-2018, by Zend Technologies
```
Ce qui compte est bien sûr l'info `php7.2.x`, si vous voyez toujours `php7.0.x`, recommencez les opérations et vérifiez qu'il n'y a pas de message d'erreur. En cas de doute, rendez-vous sur *#entraide*.

Cette version de PHP est la version **CLI** (Command Line Interface) = ligne de commande/terminal.

Mais ce n'est pas terminé, la suite continue ci-dessous.

#### Installation de modules PHP recommandés

> Ces modules sont très utilisés et vous pouvez les installer comme ceci (attention, une seule ligne) :

```
sudo apt-get install php-pear php7.2-curl php7.2-dev php7.2-gd php7.2-mbstring php7.2-zip php7.2-mysql php7.2-xml
```

### Configuration de PHP 7.2 pour le serveur Web Apache

> Pour lier PHP à Apache il suffit d'exécuter les commandes suivantes :

```
sudo a2dismod php7.0
sudo a2enmod php7.2
sudo service apache2 restart
```

Cela désactive la version 7.0 et active la version 7.2 pour Apache. Ensuite Apache est redémarré.

#### Vérification via `localhost`

Pour vérifier que PHP 7.2 est bien activé sous Apache, créez un fichier `/var/www/html/info.php` :

```php
<?php
phpinfo();
```

Et rendez-vous à `http://localhost/info.php`, vous devriez voir :

![](img/php-apache-version.png)

Si vous voyez toujours `PHP Version 7.0.x`, recommencez les opérations et vérifiez qu'il n'y a pas de message d'erreur. En cas de doute, rendez-vous sur *#entraide*.

__Si PHP CLI et PHP Apache sont OK, votre configuration est bonne :ok_hand:__

#### :warning: Activation des erreurs sous Apache

- Maintenant que c'est fait, activez les erreurs comme indiqué [dans la page de configuration](config.md) (en remplaçant 7.0 par 7.2).

## Changer de version de PHP (exemple, retour à la 7.0)

Si par la suite vous souhaitez modifier votre version de PHP CLI (ici retour à la version 7.0) :

```
sudo update-alternatives --set php /usr/bin/php7.0
```

Pour le module Apache/Web (ici retour à la version 7.0) :

```
sudo a2dismod php7.2
sudo a2enmod php7.0
sudo service apache2 restart
```