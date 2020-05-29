# Déploiement projet sur serveur AWS Ubuntu - procédure

*Objectif : Mettre en ligne une application existante Symfony sur une machine **Ubuntu 18***

[D'abord avoir créé et installé son serveur AWS, voir cette fiche](https://github.com/O-clock-Alumni/fiches-recap/blob/master/adminsys/aws/install.md).
 
1. Ajustements serveur
    - 1.1 Module Rewrite pour Apache
    - 1.2 Modules complémentaires pour PHP 7.2
    - 1.3 Installer Composer

2. Mise en production d'un projet Symfony existant
    - 2.1 Les droits Apache et ubuntu AWS
    - 2.2 Rapatriement du projet
    - 2.3 Installation du projet
    - 2.4 .htaccess et VirtualHost

----------------------------------------------------

## 1. Ajustements serveur

### 1.1 Module Rewrite pour Apache

- Activer le module de réécriture d'URL `sudo a2enmod rewrite`
- Restart du server pour activer la reecriture `sudo service apache2 restart`

### 1.2 Modules complémentaires pour PHP 7.2 

Ajoutons quelques paquets utiles à Symfony
- `sudo apt install php7.2-curl php7.2-gd php7.2-zip`

Installer en complément les librairies suivantes (utiles pour Composer notamment)
- `sudo apt install zip unzip`

### 1.3 Installer Composer 

- `php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');"`
- `sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer`
  
> Tester avec `composer --version` => doit afficher la version de Composer.


## 2. Mise en production d'un projet Symfony existant

### 2.1 Les droits Apache et user ubuntu AWS

Pour pouvoir cloner et écrire dans `/var/www` il nous faut configurer les droits nécessaires aux utilisateurs de la machine distante. Parmi les solutions possibles :

**`chown` et `chmod`**

- `sudo chown -R ubuntu.www-data /var/www`
- `sudo chmod -R ug+rwx /var/www`

> Change la propriété de `/var/www` au user `ubuntu` (nous) et au groupe `www-data` (Apache), puis ajoute les droits à ce user et à ce groupe en lecture/écriture/exécution sur tout le dossier et ses enfants. Si Apache génère des fichiers (de log ou de cache Symfony par ex.) vous devrez peut-être réexécuter la commande dans le dossier var de Symfony.

### 2.2 Rapatriement du projet

- Se connecter sur github
- Se positionner sur le projet souhaité et cliquer sur le bouton `clone or download`
- Sur la pop-in , cliquer sur le lien `Use HTTPS` pour changer le lien récupérable via HTTPS (ou SSH si vous avez configuré la clé sur le nouveau serveur)
- Cloner le repository dans `/var/www/html` (ex `git clone https://github.com/xxx/symfo-exx-nom_du_projet.git`)
  - En mode HTTPS seulement : à la demande du terminal saisir votre Github username/password

> Note: Pour utiliser le mode SSH il sera nécessaire de répéter la procédure issue de la fiche récap dédiée à Git (génération des clés SSH et Github account settings - déjà fait depuis la Fiche récap' AWS)

### 2.3 Installation du projet

- `cd mon_projet_cloné`
- `composer install`
- Créer le fichier `.env.local` à la racine du projet.
- Modifier le fichier .env.local (`nano .env.local`) une **première** fois pour : 
  - Copier la ligne suivante pour la base de donnée de production `DATABASE_URL=mysql://votre_user:votre_password@127.0.0.1:3306/moviedb`

> Note : Adapter les credentials si besoin en fonction du user créé précedemment dans MySQL et le nom de la BDD en fonction du projet.

Ensuite, effectuer les actions suivantes **avant** le changement d'environnement. En effet, dans notre cas (movieDB), nous souhaitons utiliser nos fixtures et cette commande ne peux être executée qu'en environnement de développement (cf require-dev de composer.json).

- `php bin/console cache:clear`
- `php bin/console doctrine:database:create`
- `php bin/console doctrine:migration:migrate`
- `php bin/console doctrine:fixtures:load`
- La commande custom d'import de poster réalisée lors du projet `app:...`

Puis

- Modifier le fichier .env.local (`nano .env.local`) une **deuxième** fois pour : 
  - Remplacer`APP_ENV=dev` en `APP_ENV=prod`. Ceci permettra alors à votre application d'utiliser les configuration disponibles dans `config/packages/prod` et de ne plus afficher la debug toolbar notamment.
  - Exécuter `php bin/console cache:clear`
  - Exécuter `php bin/console cache:warmup` (cela crée tous les fichiers utiles à l'appli Symfo dans l'environnement courant).

:hand: En conditions réelles de production les fixtures ne sont généralement pas utilisées, puisqu'il existe/existera potentiellement des données présentes - phase de beta-test par ex. L'ordre des actions (modifications de `.env.local`) evoqué est relatif à la mise en production du projet MovieDB qui contient des données générées par les fixtures.

> Astuce : Le fichier `.env.local` étant ignoré du projet, votre configuration de développement ne pourra pas écraser vos modifications effectuées dans le `.env.local` de l'environnement de production.

### 2.4 .htaccess et VirtualHost

Si pas déjà fait dans le projet d'origine, installer le pack Apache pour Symfony 4 qui permettra la création du `.htaccess` dans le dossier public de votre projet. Cela permettra de prendre en compte les réécritures grâce au `mod_rewrite` déjà installé. Les VirtualHosts sont la configuration des hôtes web gérés par Apache (dont le répertoire `/var/www/html` qui est le dossier par défaut du serveur web).

- `composer require apache-pack`

Pour activer la réécriture pour nos sites dans `/var/www/html`

- `cd /etc/apache2/sites-available/`
- ouvrir le fichier de configuration avec `sudo nano 000-default.conf`  
- rajouter ce bloc à la fin à l'intérieur et à la fin du  bloc `VirtualHost *:80`

```
# Configuration du répertoire
<Directory "/var/www/html">
    # AllowOverride All permet d'autoriser la surcharge de la configuration d'Apache via .htaccess
    # Question de sécurité : on ne fait pas n'imoprte quoi avec la conf du serveur
    AllowOverride All
    Order allow,deny
    Allow from All
</Directory>
```

Pour donner ceci 

```
<VirtualHost *:80>

    # ...

    DocumentRoot /var/www/html

    <Directory /var/www/html>
        AllowOverride All
        Order Allow,Deny
        Allow from All
    </Directory>

</VirtualHost>
```
Il est aussi courant de placer son projet en dehors du dossier `html` soit directement dans `/var/www`. Si tel est votre cas, modifier les URLs de votre VirtualHost en conséquence.

> Note: le lien du projet <Directory /var/www/html/symfo-movieDB/public> est celui utilisé pour le projet de demonstration qui s'appelle `symfo-movieDB`. Ce path sera à remplacer par le vrai chemin de votre projet cloné.

- Puis restart Apache `sudo service apache2 restart` (prise en compte des modifications)
- Vérifier que le site et ses URLs sont fonctionnels : Aller sur l'URL de votre site à partir de son IP ex: http://xxx.xx.xxx.xx/symfo-movieDB/public
- Si il y a une erreur 500, verifier avec `cat` ou `tail -f` dans `/var/log/apache2/error.log` ce qui s'y passe puis régler les problèmes remontés.

> Note : Pour fonctionner avec Apache votre version de PHP doit impérativement être supérieure ou égale à 7.1.3

Pour plus d'informations

- [Symfony et serveur web](https://symfony.com/doc/current/setup/web_server_configuration.html)
- [Gérer son environnement de production (KNP)](https://knpuniversity.com/screencast/symfony-fundamentals/environment-tweaks)
- En complément, [Symfony > Documentation > Guides > Deployment](https://symfony.com/doc/current/deployment.html)

> Note : Certaines manipulations de ce fichiers sont propre à l'installation avec Ubuntu. De plus, toutes les manipulations d'installation **hors Symfony** doivent être effectuées avec `sudo`.