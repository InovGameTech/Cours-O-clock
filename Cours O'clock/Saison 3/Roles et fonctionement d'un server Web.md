Rôle et fonctionnement d'un serveur web
=======================================

## Rôle

Un serveur web (Apache, Nginx, Caddy…) est un logiciel, installé sur une machine, responsable du traitement d'une portion bien spécifique du trafic web. Un serveur est en effet associé à une [adresse IP](https://fr.wikipedia.org/wiki/Adresse_IP), et seules les requêtes émises à destination de cette IP seront traitées par le serveur qui s'est déclaré responsable de cette IP.

## Fonctionnement

### Déroulé d'une requête/réponse

Schématiquement :

- une requête est initiée par un client vers http://nom-de-domaine.com/contact (requête de [type GET](https://fr.wikipedia.org/wiki/Hypertext_Transfer_Protocol))
- une [résolution DNS](https://fr.wikipedia.org/wiki/Domain_Name_System) permet de trouver l'IP du serveur responsable de nom-de-domaine.com
- la requête est transportée sur le réseau internet jusqu'au serveur
- le serveur réceptionne la requête et la traite :
  - il analyse son protocole (ici HTTP), son chemin (/contact), et d'autres infos (verbe et _headers_ HTTP, etc.)
  - en fonction du résultat de cette analyse, il peut répondre immédiatement, ou déléguer
  - _souvent_, le serveur choisit de déléguer à une application web (application _backend_, encore appelé serveur applicatif ou _application server_)
  - dans tous les cas, une réponse est préparée, puis envoyée au client ayant initié la requête

Du point de vue du client, le serveur fournit un service : il lui donne accès à des informations qu'il ne possède initialement pas. Le client est donc en attente d'une certaine qualité de service, et les serveurs web sont conçus pour être fiables et qualitatifs. Ils doivent idéalement « tenir la charge », c'est-à-dire être capables de s'adapter au trafic entrant (le nombre de requêtes/seconde). Dans le cas où le serveur web délègue le travail de préparation de la réponse à une application web _backend_, les problématiques de service (fiabilité, qualité, charge) se retrouvent dédoublées.

### Architecture interne

![Schéma modèle client/serveur](img/client-serveur.png)

Coté client, un _User Agent_ :

- par exemple un navigateur internet, le programme `curl`, etc.
- il initie un requête web à destination d'un serveur
- il traite les réponses web provenant du serveur contacté par la requête initiale

Coté serveur, un _server stack_ généralement composé de :

- un serveur web frontal :
  - par exemple Apache, Nginx, etc.
  - il réceptionne les requêtes entrantes
  - il peut répondre directement (rapidement) dans certains cas (réponses en cache, _assets_ statiques type CSS, etc.)
  - en général, il délègue à un serveur applicatif (qui lui fournira une réponse toute prête qu'il n'aura plus qu'à envoyer au client)
  - il gère certaines choses essentielles comme HTTPS, la répartition de charge, etc. (cf. section _Reverse proxy_ ci-dessous)
- un serveur applicatif (« application web ») :
  - par exemple une application PHP, Node.js, Python, Ruby, etc.
  - il détient la logique métier spécifique à l'application web qui doit traiter les requêtes clientes
  - il travaille souvent en coordination avec une base de données
  - il se comporte souvent comme une usine à HTML/CSS/JS (mais peut aussi renvoyer du JSON, du simple texte, des images & vidéos, etc.)
- une base de données :
  - par exemple MySQL, MongoDB, etc.
  - elle détient les informations recherchées par le client, sous une forme brute
  - son accès est sécurisé, contrôlé et réservé à l'application web

> Coté serveur, il n'y aucune obligation à systématiquement utiliser ces trois composants. Un serveur applicatif seul peut suffire, une base de données peut être un simple objet en mémoire dans ce même serveur applicatif, etc. Néanmoins, l'application du principe de [séparation des préoccupations](https://fr.wikipedia.org/wiki/S%C3%A9paration_des_pr%C3%A9occupations) s'applique également avantageusement au stack technique, et il est recommandé de fonctionner avec cette architecture serveur. On parle alors d'[application trois-tiers](https://fr.wikipedia.org/wiki/Architecture_trois_tiers) : le client, le « serveur » (englobant serveurs web et applicatif) et la base de données.

## Vocabulaire

Par « serveur web », on désignera tantôt :

- la machine physique sur laquelle est installé le logiciel de type serveur web (« je me connecte au serveur en SSH »)
- le logiciel de type serveur web (« au boulot, on utilise plutôt Nginx qu'Apache »)

On désigne parfois le logiciel par le terme « frontal », comme dans « notre frontal est tombé sous la charge, hier. » Le serveur web fait en effet frontablement face au trafic web entrant.

Un serveur web peut gérer [plusieurs types de services](https://fr.wikipedia.org/wiki/Service_web) : pages web, transfert de fichiers, mails, échange de données git, etc. Chaque service ayant ses contraintes et besoins spécifiques, il n'existe pas une seule manière de communiquer entre un client et un serveur, mais plusieurs, plus ou moins spécialisées et adaptées aux services supportés par le serveur web. On parle de [protocole de communication](https://fr.wikipedia.org/wiki/Suite_des_protocoles_Internet). Par exemple, l'échange de pages web se fait préférentiellement avec le protocole HTTP, tandis que le transfert de mails se fait préférentiellement avec le protocole SMTP.

Chaque service est exposé par le serveur sur un [port dédié](https://fr.wikipedia.org/wiki/Port_(logiciel)). Certains ports sont donc traditionnellement associés à certains protocoles. Par exemple, le port :80 correspond (en général) au service _pages web formatées_ qui utilise (en général) le protocole HTTP ; les ports :20 et :21 sont (en général) utilisés pour les transferts de fichiers avec FTP ; etc.

> Le port :80 est le port par défaut des [URL](https://fr.wikipedia.org/wiki/Uniform_Resource_Locator)s dans les navigateurs ; le protocole HTTP est le protocole web par défaut. Ainsi, oclock.io est interprété comme http://oclock.io:80/ et taper cette URL implicite dans la barre d'adresse d'un navigateur revient à déclencher une requête `GET http://oclock.io:80/`.

On dira qu'on code « coté serveur » (_backend_) ou « coté client » (_frontend_). Une application web est _toujours_ la résultante d'une interaction entre un client et un serveur, de sorte qu'il y a toujours, et du back, et du front (le partage des responsabilités donnant lieu à des décisions architecturales et technologiques spécifiques à chaque projet). Coder coté serveur signifie souvent mettre l'accent sur la gestion (flux, stockage) de données, indépendamment de leur représentation (graphique, sonore, etc.).

## Concepts avancés

### _Reverse proxy_

> En informatique, un proxy est un intermédiaire. Un serveur web étant par nature un intermédiaire entre une requête entrante et une réponse sortante, on peut toujours le qualifier de proxy. Par contre, le sens importe. Quand on qualifie un serveur web de _proxy_, on se place du point de vue de la requête sortante, qui part du serveur applicatif et se dirige vers le client. Un _reverse proxy_ est simplement la même chose, mais vue « dans le sens inverse » : du point de vue de la requête entrante, qui part du client et cherche à rejoindre un serveur applicatif. La question se pose alors : où est l'application web en question ?

Certaines applications web, par exemple [Phoenix](https://phoenixframework.org/), offrent des performances et des fonctionnalités suffisantes pour envisager de se passer d'un serveur classique (frontal Apache, Nginx, etc.) Toutefois, un tel serveur web frontal reste requis lorsqu'on souhaite l'utiliser comme _reverse proxy_. Les rôles d'un reverse proxy sont multiples :

- rediriger les requêtes entrantes vers la bonne application web, dans le cas où le serveur applicatif est composé de plusieurs applications web :
  - soit qu'elle soient de natures différentes
  - soit qu'il s'agisse du même code, mais dupliqué pour gérer une répartition de charge (_horizontal scaling_)
- traiter plus rapidement, et plus tôt, certaines requêtes simples et dont la réponse est prédictible :
  - feuilles de style CSS statiques et déjà requises, donc disponibles dans un cache à accès ultra-rapide
  - erreurs protocolaires
  - redirections
- implémenter des mécanismes de sécurité, types TLS (utilisation du protocole HTTPS)

### _Load balancing_

Pour « tenir la charge » face à un trafic entrant soutenu, les serveurs web ont plusieurs stratégies :

1. ajouter du cache, pour répondre plus vite et plus directement aux requêtes récurrentes
2. si le goulot d'étranglement se situe au niveau du serveur applicatif, on peut compter sur un _scaling_ horizontal au niveau de l'application web (si on met 10 instances du serveur applicatif, on a 10x plus de « bande passante »)
3. si le goulot d'étranglement se situe au niveau du serveur web lui-même, on peut également compteur sur un _scaling_ horizontal, du serveur frontal cette fois
4. dans tous les cas, un _scaling_ vertical peut aider (augmenter la RAM, les capacités CPU, etc.)

La seconde stratégie est souvent celle essayée en premier, car elle est assez simple à mettre en place. Elle consiste à gérer de la répartition de charge (_load balancing_). Le serveur web va maintenir une liste de serveurs applicatifs, et répartir les requêtes entrantes. Dans cette architecture serveur, il est important que le code applicatif soit conçu d'une manière telle que deux requêtes successives qui auraient une dépendance aux données puissent être traitées sur n'importe quel instance de l'application, faute de quoi il y a un risque de perte de cohérence au niveau des données. Heureusement, l'utilisation d'une base de données permet assez naturellement de contourner ce problème sans même y penser (mais pas toujours !).