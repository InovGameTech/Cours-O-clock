# Exercice : installer et utiliser un bundle externe

## Bundle sélectionné pour l'exercice : Liip Imagine, manipulation d'image avancée

1. Pourquoi ce bundle ?
2. Libraire GD à installer
3. Configuration minimale
4. Droits sur les répertoires
5. Gestion du cache

## Pourquoi ce bundle ?

Bien souvent vous aurez à manipuler des images, à devoir les redimensionner à différents endroits de votre application, dans des dimensions différentes. Bien sûr vous ne pouvez pas vous permettre d'utiliser la même image "source" partout (surtout si celle-ci a une taille de plusieurs Mo !).

Voir : [Documentation sur site Symfony](http://symfony.com/doc/current/bundles/LiipImagineBundle/index.html)

Le bundle étant assez "complexe" dans sa globalité, je vous demande donc de lire et de suivre en priorité :

- Installation Steps 1 à 3
- Basic usage > Create thumbnails

> Note: Avec l'arrivée de symfony 4, les contributeurs de ce bundle l'on mis à jour pour que les configurations soient compatibles. 
> - Mettre l'option *y* (yes) lorsque composer vous le proposera.


<details>
    
```
    Symfony operations: 1 recipe (701fb581cdd5306824684107653dc9cf)
  -  WARNING  liip/imagine-bundle (>=1.8): From github.com/symfony/recipes-contrib:master
    The recipe for this package comes from the "contrib" repository, which is open to community contributions.
    Review the recipe at https://github.com/symfony/recipes-contrib/tree/master/liip/imagine-bundle/1.8

    Do you want to execute this recipe?
    [y] Yes
    [n] No
    [a] Yes for all packages, only for the current installation session
    [p] Yes permanently, never ask again for this project
    (defaults to n): 
    Executing script cache:clear [OK]
    Executing script assets:install public [OK]
```

</details>

> - La documentation officielle n'étant pas à jour sur la partie installation, le bundle est a rajouter dans config > bundles.php

<details>
    
```
<?php

return [
    .....
    Liip\ImagineBundle\LiipImagineBundle::class => ['all' => true],
];

```

</details>

## Libraire GD

Vérifiez la présence de la libraire GD dans votre `phpinfo()`.

Si vous avez une erreur 500 ou une image non trouvée, veuillez installer la librairie GD sur votre TP, c'est elle qui gère les manipulations d'image en PHP (il en existe d'autres mais celle-ci est suffisante pour la plupart des besoins).

`sudo apt-get install php7.0-gd`

Rédémarrer le serveur web Apache

`sudo service apache2 restart`

## Configuration minimale

Utiliser le début du fichier de config proposé par le bundle :

```yml
# app/config/config.yml
liip_imagine:

    resolvers:
        default:
            web_path: ~

    filter_sets:
        cache: ~
```
Dans cet exemple...

```php
<img src="{{ asset('/images/mon_image.jpg') | imagine_filter('my_thumb') }}" />
```
...les images à traiter se situent dans le répertoire `web/images`.

:hand: **Attention** : le `/` en début de `asset('/images/mon_image.jpg')` est capital sinon ça plante ¯\_(ツ)_/¯

## Droits sur les répertoires

Les répertoires utilisés en écriture par le bundle doivent avoir les droits suffisants, [voir la commande setfacl](symfony-basics.md#donner-le-droit-au-serveur-web-décrire-dans-le-dossier-var) à appliquer sur le dossier `web/media`.

Si ce répertoire n'existe pas, créez-le _ou bien_ éxécuter la ligne de commande suivante pour éxécuter la mise en cache d'une image en particulier : `php bin/console liip:imagine:cache:resolve images/mon_image.jpg`.

## Gestion du cache

`php bin/console liip:imagine:cache:remove`

**Attention au cache de Imagine ET au cache de Chrome quand vous modifiez vos thumbs**