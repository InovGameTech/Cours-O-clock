## A propos de Symfony

+ Open Source ([Contribuer](http://symfony.com/doc/current/contributing))
  [What is Symfony ? > Symfony Roadmap](https://symfony.com/roadmap)
+ Web framework vs Composants stand-alone
  * Full-stack [PHP framework](http://symfony.com/at-a-glance)...
  * ...basé sur un ensemble de [composants indépendants](http://symfony.com/components)
  * avec lesquels vous pouvez même construire votre [propre framework](http://symfony.com/doc/current/create_framework)
+ [Pourquoi utiliser un framework ?](http://symfony.com/why-use-a-framework)

## Installation

### Création d'un nouveau projet standard basé sur le framework avec Composer

> :hand: **Il existe deux installations du framework Symfony**, `skeleton` qui contient **le minimum** de fonctionnalités et `website-skeleton` qui en contient **beaucoup plus**, notamment le serveur de développement, le support pour les annotations, le profiler, le moteur de template Twig, l'ORM Doctrine pour les bases de données et plus encore. **Dans le doute, choisissez `website-skeleton` pour avoir le framework complet** (création d'applications web classiques fullstack).

> :hand: A noter : Ces deux installations sont juste **une variante du même framework**, voyez-les comme **une voiture sans options** et **l'exacte même voiture avec des options**. Ces options sont modifiables à l'ajout comme à la suppression, quelque soit le squelette de départ choisit. On peut tout à fait imaginer partir de `skeleton` et lui ajouter les fonctionnalités de `website-skeleton` et vice-versa.

#### 1. Framework `skeleton` (plus léger, moins complet)

L'utilisation de `website-skeleton` est recommandée, toutefois si vous utilisez `skeleton` voici les étapes classiques pour compléter cette installation, selon vos besoins :

- Installation du projet
  - `composer create-project symfony/skeleton my-project`
- Ajout du serveur de développement
  - `composer require symfony/web-server-bundle --dev`
- Ajout des annotations
  - `composer require annotations`
- Ajout du Profiler (et sa debug toolbar !)
  - `composer require profiler`
- Ajout de Twig
  - `composer require twig`
- Ajout de Doctrine ORM
  - `composer require orm`

#### 2. Framework `website-skeleton` (recommandé)

- Installation du projet
  - `composer create-project symfony/website-skeleton my-project`

> :hand: En mode VM Server, en cas d'erreur de _timeout_, exécuter `export COMPOSER_PROCESS_TIMEOUT=4000` pour allonger le temps d'exécution de l'installation.

_Si pas déjà fait, [installer Composer](https://getcomposer.org/download/)._

#### 3. Erreurs à l'installation

Si Composer vous affiche des erreurs du genre _PHP requirements failure_ ou _PHP module is missing_, c'est qu'il vous manque une extension PHP. Identifier les extensions manquantes et installez-les comme suit, en général il s'agit de `zip` ou `xml`
- Vous devez déverouiller les mises à jour du téléporteur
  - `sudo oclock-apt-enable`
  - `sudo apt-get update`
- Puis installer les extensions selon votre version de PHP CLI ! Pour la 7.2 par ex. :
  - `sudo apt install php7.2-zip`
  - `sudo apt install php7.2-xml`
  - Etc. selon ce qui manque.
  - Pour vérifier votre version de PHP CLI : `php -v`

#### Exécuter l'application

##### a. Avec le serveur de développement fourni

Exécuter l'application fraichement créée en lançant le serveur intégré à Symfony, depuis la racine de votre projet via
```
php bin/console server:run
```
(ou `server:start`, la différence étant la trace des accès avec `server:run` et que le terminal reste occupé, vous devrez ouvrir un nouveau terminal pour continuer à travailler).

##### b. Via Apache et localhost

Pour accéder à votre application Symfony via Apache (`http://localhost/.../nom_du_projet/public`) vous devez installer le fichier `.htaccess` qui permet la réécriture d'URL pour Symfony.
- `composer require apache-pack`

> :hand: Ce package sera également nécessaire quand vous travaillerez sur le VPN via vos URLs personnelles du type `nom-prenom.vpnuser.oclock.io`

### Infos complémentaires

#### Vérifier les [pré-requis](http://symfony.com/doc/current/reference/requirements.html) pour le serveur Web :

```
cd mon_projet/
composer require symfony/requirements-checker
```
Puis accéder à `check.php` dans le dossier *public*  à l'aide du navigateur (par ex. `http://127.0.0.1:8000/check.php`).

> Attention : vous pouvez lancer plusieurs serveurs depuis plusieurs projets Symfony, le port peut donc changer : 8000, 8001, 8002, etc.

#### Pour installer les vendors suite à un cloning de dépôt

```
cd mon_projet/
composer install
```

#### Pour mettre à niveau votre application Symfony

Voir en bas de la page "Setup", les liens suivants :

- [Upgrading a Major Version (e.g. **3**.4.0 to **4**.0.0)](https://symfony.com/doc/current/setup/upgrade_major.html)
- [Upgrading a Minor Version (e.g. 3.**3**.3 to 3.**4**.0)](https://symfony.com/doc/current/setup/upgrade_minor.html)
- [Upgrading a Patch Version (e.g. 3.3.**2** to 3.3.**3**)](https://symfony.com/doc/current/setup/upgrade_patch.html)

#### Installer un bundle via Composer

Cherchez le bundle que vous souhaitez installer, sur [Packagist.org](https://packagist.org/), (admettons `friendsofsymfony/user-bundle`) puis une fois trouvé, installez-le comme suit :

`composer require friendsofsymfony/user-bundle`

### Installation de la démo officielle complète

`composer create-project symfony/symfony-demo`

Ce projet utilise le gestionnaire de bases de données SQLite, si vous avez une erreur 500, installez SQLite en LDC :

`sudo apt-get install php7.2-sqlite`

=> si on vous dit que la configuration du php.ini est en conflit, choisissez `Garder la version actuelle`

Puis redémarrez le serveur web Apache :

`sudo service apache2 restart`

### Donner le droit au serveur web d'écrire dans le dossier `var`

> :hand: A partir de Symfony 4 ceci n'est plus nécessaire.

En se plaçant à la racine du projet :

```
sudo setfacl -dR -m u:www-data:rwX -m u:mint:rwX var
sudo setfacl -R -m u:www-data:rwX -m u:mint:rwX var
 ```
 Cela permet de donner les droits de lecture (r), d'écriture (w) et d'éxécution (X) aux utilisateurs `www-data` et `mint`, sur les sous-dossiers et fichiers du dossier `var`. En pratique, quand vous naviguez sur le site, `www-data` (Apache) vient écrire dans ce dossier (cache, sessions, logs). Lorsque vous (`mint`) exécutez des lignes de commandes `php bin/console <command>`, vous devez également pouvoir écrire dans ce répertoire.

Sinon plus simple mais moins "propre" (si la commande du dessus ne fonctionnait pas) :
 `sudo chmod -R 777 var`

## Architecture
[Système de fichiers](http://symfony.com/doc/current/page_creation.html#checking-out-the-project-structure)

### Composants
* [Symfony Core: Router et Controllers](core-routing-controllers.md)

![Ecosystem Symfony](img/symfony-ecosystem.png)  