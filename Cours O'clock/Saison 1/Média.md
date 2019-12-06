# Médias

## Image [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/img)

L'élément HTML de type `inline` `<img>` permet d'afficher des fichiers image d'extension `.jpg`, `.png`, `.gif`, etc... grâce à l'attribut `src`.

`src` peut contenir une URL relative ou absolue ( voir [syntaxe.md > Liens](syntaxe.md) ) vers le fichier à utiliser

Il est vivement recommandé d'ajouter un texte alternatif `alt` décrivant l'image pour assurer une certaine accessibilité des images.

Toujours dans un souci d'accessibilité et de référencement, il est conseillé de nommer les fichiers images de manière **explicite**. 
Par exemple, `564A-SD5-SF8545A-qwecfg.jpg`, manque un peu de clarté... 

```html
<img src="../images/tour-eiffel.jpg" alt="Illustration de la tour Eiffel">
```

## Audio [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/audio)

Intégration de contenu audio

Quelques attributs bien utiles

- `controls` offre une interface pour gérer la lecture et le volume
- `autoplay` permet de lancer la lecture automatiquement
- `loop` lit le fichier en boucle

L'élément `<source>` et son attribut `src` permet de spécifier une source, `type` précise de quel type  MIME est le fichier.

```html
<audio controls="controls">
  <source src="podcast-eiffel.mp3" type="audio/mp3">
  L'audio n'est pas pris en charge <!--Message en cas de fonctionnalité non supportée-->
</audio>
```

Plusieurs `<source>` peuvent être ajoutées pour maximiser la compatibilité avec les différents navigateurs

> Plus d'informations sur [les formats pris en charge](https://developer.mozilla.org/fr/docs/Web/HTML/Formats_pour_audio_video) et un [guide d'utilisation](https://developer.mozilla.org/fr/docs/Web/HTML/Utilisation_d'audio_et_video_en_HTML5) complet sont disponibles sur MDN

## Video [MDN](https://developer.mozilla.org/fr/docs/Web/HTML/Element/video)

Intégration de contenu vidéo

Quelques attributs bien utiles

- `controls` offre une interface pour gérer la lecture et le volume
- `autoplay` permet de lancer la lecture automatiquement
- `loop` lit le fichier en boucle
- `poster` permet de préciser une vignette pour la vidéo

L'élément `<source>` et son attribut `src` permet de spécifier une source, `type` précise de quel type  MIME est le fichier.

```html
<video controls="controls">
  <source src="podcast-eiffel.mp4" type="video/mp4">
  La vidéo n'est pas prise en charge <!--Message en cas de fonctionnalité non supportée-->
</video>
```

Plusieurs `<source>` peuvent être ajoutées pour maximiser la compatibilité avec les différents navigateurs

> Plus d'informations sur [les formats pris en charge](https://developer.mozilla.org/fr/docs/Web/HTML/Formats_pour_audio_video) et un [guide d'utilisation](https://developer.mozilla.org/fr/docs/Web/HTML/Utilisation_d'audio_et_video_en_HTML5) complet sont disponibles sur MDN