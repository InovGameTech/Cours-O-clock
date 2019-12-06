# Dictionnaire de données

A partir des infos disponibles (maquettes, cahier des charges, descriptions fonctionnelles), nous allons **lister toutes les informations nécessaires au fonctionnement** de l'application dans un _dictionnaire de données_, selon cette méthode :

- **Nommer chaque information**, la décrire si besoin.
- **Indiquer son type** (nombre, texte, booléen, calculé à partir d'autres informations).
- Ajouter un commentaire si besoin.

Une fois la liste créée, on doit **la trier** afin de :

- Décomposer les données : **chaque ligne doit contenir une information unique**, indivisible (pas de champ _Adresse_ qui incluerait _Adresse + Ville + Code postal_ par ex.).

Une fois ceci fait nous pouvons **identifier les entités** et y rattacher les données. Selon le contexte cette étape peut même être faite avant l'identification des données.

> Certaines informations ne seront pas rattachées qu'à une seule entité, par ex. le rôle d'un acteur dans un film - entité _Film_ et _Acteur_. Ces informations vont nous aider à construire les relations.

## Exemple de dictionnaire avec nos livres

Nom|Description|Type|Commentaire|Entité|
-|-|-|-|-|
Titre|Titre du livre|texte court|-|Livre|
Année|Année de première parution|date|Année sur 4 chiffres|Livre|
Nom|Nom de l'auteur|texte court|-|Auteur|
Prénom|Prénom de l'auteur|texte court|-|Auteur|
Nom|Nom du genre|texte court|-|Genre|

Nous avons identifié 3 entités. Le nom et le prénom de l'auteur ont été décomposés.

---

> [Retour au sommaire](./README.md)