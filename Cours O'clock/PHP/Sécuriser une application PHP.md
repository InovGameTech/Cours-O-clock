# Sécuriser une application PHP

##### Quand?
Dès lors qu'on veut pouvoir identifier nos visiteurs, restreindre l'accès à certaines données ou fonctionnalités d'une application.  
*exemples: jeu en ligne, blog, fil de commentaires, boutique, administration...*  

##### Comment?   
- Enregistrement d'un utilisateur
- Authentification d'un utilisateur
- Gestion des autorisations

## Authentification   
Pour "reconnaître" un utilisateur:  
- Il faut qu'on ait <a href="#signup">collecté les informations qui l'identifient dans notre base de données</a>  
- Pour être reconnu, l'utilisateur doit <a href="#signup">s'identifier</a>, avec un identifiant (généralement un username ou adresse email) et son **mot de passe**.  
- Une base de données peut être compromise. Les mots de passe ne doivent donc pas être stockés "en clair", on stocke plutôt un <a href="#passhash">hash</a>.
- On doit fournir à l'utilisateur une méthode de récupération de son mot de passe.

### <span id="passhash">Hachage de mot de passe en PHP</span>
- Un **hash** est une chaîne de caractères, générée par calcul à partir d'un mot de passe (ou tout autre type de données).
- Il ne permet pas de retrouver la valeur d'origine du mot de passe, on va pouvoir le stocker sans risque, mais on peut vérifier si un mot de passe fourni correspond ou non à un hash.

Pour *hacher* un mot de passe, on lui concatène souvent un *salt* (qui complexifie le hachage) puis on applique un algorithme de cryptage qui génère le **hash**.
Cette opération se faisait directement avec PHP auparavant, par exemple avec `md5()` ou `sha1()` qui sont des fonctions de cryptage.  
Ces méthodes ne sont plus garanties comme étant sécurisées.    
Dorénavant il est recommandé d'utiliser :  
  `password_hash($password, PASSWORD_DEFAULT)`  
Et pour vérifier un mot de passe on utilise la fonction associée :  
  `password_verify($typedPassword, $dbPassword)`

Avec ces fonctions, le choix de l'algorithme et du *salt* utilisés sont fait de façon interne par PHP. C'est une garantie de sécurité supplémentaire.  

Pour en savoir plus: [documentation PHP a propos des mots de passe](http://php.net/manual/fr/faq.passwords.php)



### Inscription d'un nouvel utilisateur : <span id="signup">*signup*</span>
L'inscription d'un nouvel utilisateur dans l'application va se faire à l'aide d'un formulaire.
C'est `password_hash()` qui est utilisé pour stocker le hash du mot de passe saisi.

![img/SIGNUP.png](img/SIGNUP.png)



### Authentification : <span id="login">*login*</span>
Ensemble des opérations qui permettront à l'application de reconnaître **qui** est l'utilisateur qui vient d'effectuer la requête.  
Lorsqu'un utilisateur souhaite s'identifier, on doit :  
a. vérifier s'il existe en base de données   
b. vérifier que son mot de passe est correct   
c. créer une session pour cet utilisateur (pour ne pas avoir à le réidentifier à chaque requête)  

![img/LOGIN.png](img/LOGIN.png)


### Déconnexion

##### volontaire
pour déconnecter un utilisateur, il suffit de détruire sa session avec `session_destroy()`.

##### automatique (inactivité de l'utilisateur)
Tant que l'utilisateur ne fait pas de nouvelle requête, il est considéré comme "inactif".
Si sa durée d'inactivité dépasse 30 minutes (cette valeur par défaut peut être modifiée dans la configuration - fichier `php.ini`,  - du serveur) sa session est supprimée, et lors de la prochaine requête l'appication ne le reconnaîtra pas.  

### Mot de passe oublié

Pour mettre à disposition de vos utilisateurs un système de "Mot de passe oublié", vous devez impérativement avoir accès à leur adresse mail.  
En effet c'est par ce biais que vous allez communiquer à votre utilisateur le lien qui lui permettra d'enregistrer un nouveau mot de passe, de façon sûre (si sa boite mail n'est pas corrompue).

La modification du mot de passe se fait en plusieurs étapes:  
1. l'utilisateur signale la perte de son mot de passe et fournit son adresse email. C'est ce qui va nous permettre de le retrouver dans la BD.  
2. si l'utilisateur existe bien en base de données:
  - on génère un **token** (*jeton*), qui doit être une chaîne de caractères unique, suffisamment longue
    `$token = bin2hex(random_bytes(16));`
  - on lie en base de données le token avec l'email de l'utilisateur
  - on envoie à l'utilisateur par email (fonction `mail()`) un lien vers la page de saisie du nouveau mot de passe.   
    Ce lien inclut comme paramètres `$_GET` l'identifiant de l'utilisateur, et le token.  
3. l'utilisateur clique sur le lien reçu par mail  
  - saisit son nouveau mot de passe
  - on vérifie que le token (paramètre GET) existe bien en base et correspond à l'id d'utilisateur (paramètre GET).
  - on enregistre le nouveau mot de passe en BD pour l'utilisateur concerné.

Grâce à cette méthode, on est sûr que l'utilisateur qui essaiera de changer son mot de passe est bien celui qui a accès à la boite mail concernée.

![img/FORGOT_PASSWORD.png](img/FORGOT_PASSWORD.png)