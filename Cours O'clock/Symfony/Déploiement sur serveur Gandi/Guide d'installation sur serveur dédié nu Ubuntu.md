# Deploiement projet - procedure

*Objectif : Mettre en ligne une application existante Symfony sur une machine **Ubuntu 18***

[Pour installer une distribution **Debian**, voir cette fiche](deploiement-gandi-debian.md).

1. Creation server
 
2. Installation serveur
    - 2.1 connexion ssh
    - 2.2 installer sudo (optionnel)
    - 2.3 Mettre a jour Ubuntu
    - 2.4 Installer Apache
    - 2.5 Installer PHP 7.2
    - 2.6 Installer MySQL
    - 2.7 Installer composer
    - 2.8 Installer git

3. Mise en production d'un projet existant symfony
    - 3.1 Les droits Apache et admin Gandi
    - 3.2 Rapatriement du projet
    - 3.3 Installation projet
    - 3.4 .htaccess & VirtualHost

----------------------------------------------------

### 1. CREATION SERVER - Interface gandi 4 https://v4.gandi.net

> Note : Seule les actions listées ci dessous sont nécessaires. Les autres valeurs sont à laisser par défaut

- Onglets : Services > Serveurs
- Bouton "Créé un serveur"

- Etape 1/2 - Page de création
    - RAM 512 (pas possible de mettre plus à ce stade)
      - Quand vous aurez vos crédits, vous pourrez modifier la RAM de votre serveur et la passer à 1024, notamment *si Composer lag fort*.
    - Valider
    
> Note: Dans notre cas nous utiliserons un peu plus de RAM notamment pour composer

- Etape 2/2 - Page "Configurer votre serveur"
    - Système > Systeme d'exploitation
        - "Ubuntu 18" (système très user-friendly)

    - Paramètres de connexion 
        - saisir "Identifiant administrateur", par ex. votre prénom
        - saisir "Mot de passe", ne pas oublier un caractère spécial, par ex. Azerty89$
        - ressaisir le mdp dans "Confirmation du mot de passe"

Fiche récap admin sys : https://github.com/O-clock-Alumni/fiches-recap/blob/master/ldc/adminsys.md

Pour plus d'informations système/Symfony :

Benchmarks : https://symfony.fi/entry/symfony-benchmarks-scaling-php-by-adding-cpu-ram

----------------------------------------------------

### 1.  INSTALLATION SERVEUR

#### 2.1 connexion ssh 

 - Cliquer au niveau de l'interface gandi sur le serveur fraichement créé et récupérer sont ip
 - Dans le terminal : `ssh votre_identifiant@mon_IP`, accepter le fingerprint (yes) puis entrer son mot de passe

#### 2.2 Ajouter votre user à sudo (pratique)


- `su`
- `usermod -aG sudo votre_user`
- Quitter le mode `su` en tapant `exit`
- Quitter le serveur en tapant `exit`
- Reconnectez-vous pour activer les changements : `ssh votre_identifiant@mon_IP`

#### 2.3 Mettre à jour Ubuntu

> Note: Si sudo n'est pas configuré il faudra alors passer par `su` (super utilisateur pous installer vos paquets)

- `sudo apt update`
- `sudo apt upgrade`
- `sudo apt dist-upgrade`

#### 2.4 Installer Apache

> Note: A faire avant l'installation de PHP car cela permettre d'activer la librairie PHP / Apache par la suite

- `sudo apt-get install apache2 -y`
- Activer le module de réécriture d'url `sudo a2enmod rewrite`
- Restart du server pour activer la reecriture `sudo service apache2 restart`

#### 2.5 Installer PHP 7.2 

- `sudo apt install php7.2`

Vérifiez votre installation : `php -v`

 - Installer les librairies nécessaires à Apache / PHP et Symfony : `sudo apt install php7.2-cli php7.2-common php7.2-curl php7.2-gd php7.2-json php7.2-mbstring php7.2-mysql php7.2-xml libapache2-mod-php7.2 php7.2-zip php7.2-mysql`

- Installer en complément les librairies suivantes (utiles pour Composer notamment) : `sudo apt-get install zip unzip`

#### 2.6 Installer MySQL 

  - `sudo apt-get install mysql-server`
  - Important pour la liaison entre le driver MySql / PHP `sudo service apache2 restart`
  - Tester votre connexion en root avec `sudo mysql -u root` puis taper entrer
  - Si c'est ok, une console MySQL s'ouvrira. Rester dans la console afin de vous créer deux utilisateurs utilisables sans sudo dont un spécifique Symfony.

  Pour un user root classique, dans la console MySQL :

  - `DROP USER 'root'@'localhost';`
  - `CREATE USER 'root'@'localhost' IDENTIFIED BY '';`  
  - `GRANT ALL PRIVILEGES ON *.* TO 'root'@'localhost' WITH GRANT OPTION;`
  - `FLUSH PRIVILEGES;`

  Pour un utilisateur ayant l'identifiant `admin` et le mot de passe `adminpwd`:

  - `CREATE USER 'admin'@'localhost' IDENTIFIED BY 'adminpwd';`  
  - `GRANT ALL PRIVILEGES ON *.* TO 'admin'@'localhost' WITH GRANT OPTION;`
  - `FLUSH PRIVILEGES;`


#### 2.7 Installer Composer 

 - `php -r "copy('https://getcomposer.org/installer', '/tmp/composer-setup.php');"`
 - `sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer`
 - Tester avec `composer --version` => doit afficher la version de Composer.

#### 2.8 Installer git
 - `sudo apt install git`
 - `git config --global user.name "Claire fortin"` (remplacer par votre nom)
 - `git config --global user.email claire@oclock.io` (remplacer par votre email)

> Note: Afin de simplifier la procédure nous clonerons nos projet en HTTPS. Pour l'instant cela n'est pas encore possible cf 3.1 Les droits Apache et admin Gandi. Mais vous pouvez si vous le souhaitez créer et installer une clé SSH sur votre serveur, cela prend 2 minutes.

**Fiche Récap'** 

 - Git & ssh : https://github.com/O-clock-Alumni/fiches-recap/blob/master/ldc/git.md
 - Journée adminsys : https://github.com/O-clock-Alumni/fiches-recap/blob/master/ldc/installation-complete.md

Pour plus d'informations :

- [How to Install PHP 7.2 on Ubuntu 18.04](https://thishosting.rocks/install-php-on-ubuntu/)
----------------------------------------------------

### 3. Mise en production d'un projet existant Symfony

#### 3.1 Les droits Apache et admin Gandi

Pour pouvoir cloner et ecrire dans `/var/www` il nous faudra rajouter les droits suffisants aux users présents sur notre machine.

Deux solutions possibles (et sûrement plus).

**1. Via chown et chmod**

- `sudo chown -R votre_user.www-data /var/www`
- `sudo chmod -R ug+rwx /var/www`

> Change la propriété de `/var/www` au user `votre_user` et au groupe `www-data` (Apache), puis ajoute les droits à ce user et à ce groupe en lecture/écriture/exécution sur tout le dossier et ses enfants. Si Apache génère des fichiers (de log ou de cache Symfony par ex.) vous devrez réexécuter la commande dans le dossier var de Symfony.

**2. Via les ACL**

- `sudo apt-get install acl`
- `sudo setfacl -dR -m u:www-data:rwX -m u:votre_user:rwX /var/www`
- `sudo setfacl -R -m u:www-data:rwX -m u:votre_user:rwX /var/www`

> [En savoir plus](http://symfony.com/doc/3.4/setup/file_permissions.html).

#### 3.2 Rapatriement du projet

- Se connecter sur github
- Se positionner sur le projet souhaité et cliquer sur le bouton `clone or download`
- Sur la pop-in , cliquer sur le lien `Use HTTPS` pour changer le lien récupérable via HTTPS (ou SSH si vous avez configuré la clé sur le nouveau serveur)
- Cloner le repository dans `/var/www/html` (ex `git clone https://github.com/xxx/symfo-exx-nom_du_projet.git`)
- A la demande du terminal saisir votre Github username / password (nécessaire au mode HTTPS)

> Note: Pour utiliser le mode SSH il sera nécessaire de répéter la procédure issue de la fiche récap dédiée à Git (generation des clefs SSH & Github account settings) 

#### 3.3 Installation projet

- `cd mon_projet_cloné`
- `composer install`

- Créer le fichier `.env.local` à la racine du projet.
- Modifier le fichier .env.local (`nano .env.local`) une **première** fois pour : 
  - Copier la ligne suivante pour la base de donnée de production `DATABASE_URL=mysql://admin:adminpwd@127.0.0.1:3306/moviedb`

> Note : Adapter les credentials si besoin en fonction du user créé précedemment dans MySql et le nom de la BDD en fonction du projet

Ensuite, effectuer les actions suivantes **avant** le changement d'environnement. En effet, dans notre cas (movieDB), nous souhaitons utiliser nos fixtures et cette commande ne peux être executée qu'en environnement de développement (cf require-dev de composer.json).

- `php bin/console cache:clear`
- `php bin/console doctrine:database:create`
- `php bin/console doctrine:migration:migrate`
- `php bin/console doctrine:fixtures:load`
- La commande custom d'import de poster réalisée lors du projet `app:...`

Puis

- Modifier le fichier .env.local (`nano .env.local`) une **deuxième** fois pour : 
  - Remplacer`APP_ENV=dev` en `APP_ENV=prod`. Ceci permettra alors à votre application d'utiliser les configuration disponibles dans `config/packages/prod` et de ne plus afficher la debug toolbar notamment.

En condition réelle de production les fixtures ne sont généralement pas utilisées. L'ordre des actions (modifications de `.env.local`) evoqué est relatif à la mise en production du projet MovieDB qui contient des données générées par les fixtures.

> Astuce : Le fichier `.env.local` étant ignoré du projet, votre configuration de développement ne pourra pas écraser vos modifications effectuées dans le `.env.local` de l'environnement de production.

#### 3.4 .htaccess & VirtualHost

Installer le pack apache pour Symfony 4 qui permettra la creation du `.htaccess` dans le dossier public de votre projet. Cela permettra vis à vis de votre configuration projet avec votre VirtualHost (cf 2.4 Installer Apache) de prendre en compte les bonnes redirections grace au `mod_rewrite` déjà installé.

- `composer require apache-pack`

Pour activer la réécriture pour nos sites dans /var/ww/html

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
....

   DocumentRoot /var/www/html

    <Directory /var/www/html>
        AllowOverride All
        Order Allow,Deny
        Allow from All
    </Directory>

</VirtualHost>
```
Il est aussi courant de placer son projet en dehors du dossier `html` soit directement dans `/var/www` ; Si tel est votre cas, modifier les urls de votre virtual host en conséquence.

> Note: le lien du projet <Directory /var/www/html/symfo-movieDB/public> est celui utilisé pour le projet de demonstration qui s'apelle `symfo-movieDB`. Ce path sera à remplacer par le vrai path de votre projet cloné.

- Puis restart apache `sudo service apache2 restart` (prise en compte des modifications)
- Vérifier que le site et ses urls sont fonctionnels : Aller sur l'url de votre site à partir de son IP ex: http://xxx.xx.xxx.xx/symfo-movieDB/public
- Si il y a une erreur 500, verifier avec `cat` ou `tail -f` dans `/var/log/apache2/error.log` ce qui s'y passe puis regler les problèmes remontés.

> Note : Pour fonctionner avec Apache votre version de PHP doit impérativement être supérieure ou égale à 7.1.3

Pour plus d'informations

- Symfony & Apache : https://symfony.com/doc/current/setup/web_server_configuration.html
- Gérer son environnement de production (KNP) : https://knpuniversity.com/screencast/symfony-fundamentals/environment-tweaks
- En complément déploiement symfony: https://symfony.com/doc/current/deployment.html

> Note : Certaines manipulations de ce fichiers sont propre à l'installation avec Ubuntu. De plus, toutes les manipulations d'installation **hors Symfony** doivent être effectuées avec `sudo`.