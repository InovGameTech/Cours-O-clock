# PairProgramming

Le développement en _PairProgramming_ ou en binôme permet d'avoir 2 cerveaux en réflexion sur un seul code. On obtient un code plus propre et plus abouti.

Pour plus de détails sur cette technique de développement très utile en apprentissage mais très peu utilisé dans le monde du travail, direction [Wikipédia](https://fr.wikipedia.org/wiki/Programmation_en_bin%C3%B4me).

## Les rôles

- _Driver_ qui écrit le code
- _Observer_ qui lit le code et vérifie son exactitude, sa cohérence et son optimisation
- Dans nos ateliers en Pair-Programming, l' _Observer_ pourra aussi écrire du code. Le but est principalement d'avoir 2 cerveaux pour résoudre les problèmes

## Mise en place

Pour travailler en téléprésentiel sur le même code, il faut :
- partager le _LiveShare_ du repo du _Driver_
- accéder au serveur Web du _Driver_
- pouvoir discuter ensemble

### Partager le _LiveShare_

- si elle n'est pas encore installée, installer l'extension _LiveShare_ dans VSCode : https://github.com/O-clock-Alumni/fiches-recap/blob/master/vscode/packages.md#base
- le _Driver_ lance VSCode sur son projet comme d'habitude (`code .` depuis le dossier du repo)
- dans l'onglet _LiveShare_, _Démmarrer la session de collaboration_
- VSCode ouvrira peut-être une page sur le navigateur afin de s'authentifier => s'authnetifier via GitHub
- le lien du _LiveShare_ sera automatiquement copié dans le clipboard
- il suffit ensuite de le coller dans la conversation Slack avec le ou les _Observer(s)_

![Liveshare Screenshot](img/liveshare.png)

### Accéder au serveur Web du _Driver_

- toute l'équipe doit être connectée sur le VPN O'clock
- chaque VM/Téléporteur est accessible grâce à un nom de domaine interne :
  - `http://prenom-nom.vpnuser.lan`
  - il faut remplacer "prenom" et "nom" par le prénom et nom du _Driver_
- si tu n'arrive pas à te connecter
  - relancer le VPN (le couper)
  - attendre 5 minutes
  - réessayer
  - si toujours impossible de se connecter, contacter un prof/helper

### Pouvoir discuter ensemble

- pour cela, déjà, il faut un micro
- à deux, on peut lancer un appel avec Slack, mais il sera limiter à 2 personnes (prof/helper ne pourra rejoindre pour aider)
- le mieux, c'est d'utiliser **Discord**
  - soit online, sur le navigateur
  - soit en installant l'application
- une fois **Discord** lancé, il faut aller dans le **Discord** d'O'clock (un lien d'invitation et un "mot de passe" ont été envoyé en S00)
- rejoindre tous le même Salon de discussion
- renseigner le nom du Salon dans le document des groupes d'atelier

**Salons et paramètres**

![Salons et paramètres](img/discord1.png)

- il faudra ensuite paramétrer le micro et sa détection
- tout se trouve dans "Voix & Vidéo" (screenshot plus bas)
- sélectionner le micro dans "Périphérique d'entrée"
- bien régler la "Sensibilité de la détection de la voix", sinon les débuts et fins de phrase ne seront pas détectés et donc pas "diffusés"
- enfin, régler le "Volume d'entrée" pour que le niveau sonore soit suffisant

**Voix et Vidéo**

![Voix et Vidéo](img/discord2.png)

### Solutions de rechange

#### Tokbox

La [démo de tokbox](https://opentokdemo.tokbox.com/) permet de tester la visioconférence proposée par Tokbox.  
Le partage d'écran est possible en passant par une extension à installer.  
Il n'y a pas de limitation connue à ce jour.

=> solution de rechange pour :
- Accéder au serveur Web du _Driver_
- Pouvoir discuter ensemble

#### Hangouts

[Hangouts](https://hangouts.google.com) permet de faire des visioconférences gratuitement.  
On n'a pas encore constaté de limitation dans le partage d'écran.

=> solution de rechange pour :
- Accéder au serveur Web du _Driver_
- Pouvoir discuter ensemble

#### Appear.in

[Appear.in](https://appear.in/) permet de faire des visioconférences gratuitement jusqu'à 4 personnes.  
Le partage d'écran est possible en passant par une extension à installer.  
Cependant, le partage d'écran est limité à 20 minutes...

=> solution de rechange pour :
- Accéder au serveur Web du _Driver_
- Pouvoir discuter ensemble