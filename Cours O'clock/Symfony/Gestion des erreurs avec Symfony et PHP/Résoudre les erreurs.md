# Résoudre les erreurs dans Symfony

Cette page vise à vous donner des conseils quant à la façon de résoudre des erreurs, dans Symfony et plus généralement avec PHP.

## Les linters

Dans Atom, on vous a déjà indiqué les packages de type _linter_, qui permettent de détecter les erreurs de syntaxe lors de l'édition du code. [Voir la fiche réacp' Atom Linters](../../atom/linters.md).

## Types d'erreurs rencontrés avec Symfony

Nous avons recensé les types d'erreurs potentielles :

+ **Syntaxe**
    - **PHP** : oubli d'un point-virgule, des accolades, parenthèses ou crochets mal fermés, des noms de variable ou de fonctions mal écrits, cela se traduit souvent par `syntax error` ou `undefined variable`.
    - **Objet _null_** : si vous voyez l'erreur `try to access property on a null object`, l'objet auquel fait référence la dite propriété est _null_, il n'existe donc pas, vous devez remonter en amont du code pour trouver pourquoi **l'objet** est vide (et non la propriété).
    - **Namespace** : erreur de syntaxe dans un namespace de vos classes, ou oublie d'import (`use`) de la dite classe dans une autre, se traduit souvent par `did you forget to add a 'use' statement ?`.
    - **Annotation**
        - **Routes** : vérifier l'import de la classe `Sensio\Bundle\FrameworkExtraBundle\Configuration\Route` ou tout type d'annotation gérée par un bundle.
        - **ORM** : vérifier l'import de la classe `Doctrine\ORM\Mapping as ORM;` mais également, si vous faites des copier-coller depuis le site Doctrine, n'oubliez pas de rajouter `ORM\` devant les annotations `@Column` pour obtenir `@ORM\Column` par exemple.

+ **Structurelle**
    - **Modèle** : vérifier les getters and setters notamment, ou la présence des champs en erreur. Vérifier que votre User implémente bien des bonnes classes pour l'utilisation avec le module Security.
    - **Vue** : assurez-vous du bon passage des paramètres attendus, d'un héritage correct des templates, de la bonne localisation des fichiers de templates dans les répertoires des vues, ne pas hésiter à utiliser `{{ dump(ma_variable) }}`
    - **Contrôleur**
        - Routes : assurez-vous bien sûr que les routes saisies dans le navigateur correspondent bien aux routes existantes. Il y a possiblité de doublons de routes, en cas de doute utiliser la commande `php bin/console debug:router` pour afficher les routes du projet (ou passer par le `Profiler > Routing`).

+ **Fonctionnalités**
    - **Forms** : toujours avoir la doc des forms sous la main en support :)
    - **User provider** : idem, la doc vous sauvera pour tout ce qui est de la création d'un User provider. Les étapes sont simples mais rigoureuses, ne pas hésitez à les relire/refaire depuis zéro en cas de doute.
    - **Bundle** : si vous avez installé un bundle à la main, assurez-vous qu'il est bien présent dans `app/AppKernel.php`.
    - **Upload** : avec l'upload, les URL d'affichage, les chemins d'accès physiques et les droits d'écriture dans les répertoires sont des causes fréquentes d'erreur. Aussi, La librairie GD doit être installée pour les manipulations d'images.

+ **Système**
    - **Service** : s'assurer de la bonne configuration de `services.yml` et avoir la doc à portée de main.
    - **Profiler** : ne pas hésiter à utiliser le Profiler de la web debug toolbar pour inspecter l'environnement d'éxécution de l'application qui plante : route trouvée ou non, erreur de formulaire, le ROLE attendu au niveau du User est-il présent, les requêtes SQL éxécutées correspondent-elles à ce qui est attendu ?, etc. Une balise `<body>` doit être présente dans votre HTML pour afficher la toolbar.
    - **Command** : la ligne de commande `php bin/console debug` vous donne des infos sur l'environnement de votre application.

## Trouver la source d'erreur dans la trace

Lorsque Symfony affiche la trace des erreurs, essayez dans la mesure du possible de remonter à l'erreur qui se situe dans **votre code source** et non celui d'un composant du framework ou d'un bundle tiers. Il faut parfois ouvrir la trace et la remonter jusqu'à trouver l'origine de l'erreur, par exemple dans un contrôleur.

## En cas d'erreur 500 brute (aucune info !)

Il peut arriver qu'une page blanche s'affiche avec comme seule information "Erreur 500". Dans ce cas et dans tous les autres cas, vous pouvez toujours vous référez aux logs d'erreur d'Apache, qui se situent dans `/var/log/apache2/error.log`.

Pour lire ces logs depuis la fin (la queue), utiliser : `tail -f /var/log/apache2/error.log`

Vous verrez ainsi les dernières erreurs loggées et en temps réel les erreurs s'afficher.