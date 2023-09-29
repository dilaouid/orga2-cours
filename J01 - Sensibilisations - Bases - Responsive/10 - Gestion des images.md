# Gestion des images

Des images optimisées sont essentielles pour une bonne expérience utilisateur, pour des raisons de **performance**, mais aussi pour des raisons de **confort visuel**.

En fonction de la nature de l'image et de sa signification (si elle a pour vocation à en avoir une), on peut choisir de l'optimiser différemment.

Quelle utilité par exemple pour une image de fond d'avoir une résolution de 3000x1500 alors que la fenêtre du navigateur Web ne fait que 1200px de large ?

De plus, des pages HTML peuvent demander à charger de nombreuses images, dont la plupart ne seront pas visibles immédiatement par l'utilisateur (qui ne voit que le haut de la page lors du chargement).

Sans compter la complixité de gestion de la qualité en fonction des différents écrans et densités de pixels (Rétina, OLED, …) sur tous les devices (ordinateurs, tablettes, smartphones, …).

Aujourd'hui, HTML propose des solutions natives et faciles à mettre-en-place pour gérer ces problématiques.

Cela passe par de nouveaux **attributs** permettant de trouver le paramètrage optimal pour chaque image.

## Lazy-loading natif

L'attribut `loading` de la balise `<img>` permet de définir le comportement de chargement de l'image :

```html
<img src="/image.jpg" loading="lazy">
```

Cet attribut indique au navigateur de **ne pas charger l'image tant qu'elle n'est pas visible dans la viewport**.

Il s'agit d'une fonctionnalité native, ne nécessitant aucun script JS et [compatible avec tous les navigateurs modernes](https://caniuse.com/loading-lazy-attr) !

## Trouver les dimensions optimales

### Attribut `srcset`

À moins de travailler avec des SVG, il est aujourd'hui nécessaire de fournir à l'élément `<img>` les dimensions d'affichage optimales d'une image.

La dimension optimale va dépendre de la taille de la viewport, mais aussi de la densité de pixels de l'écran du visiteur.

L'attribut `srcset` va permettre de définir une image adaptée au terminal de consultation en ciblant à la fois **la taille de l'écran** et **la densité de pixels**.

Cet attribut se base sur l'utilisation des **"descripteurs de source"**. Il en existe 2 :

- `w` : descripteur de largeur
- `x` : descripteur de densité de pixels

On les utilise comme suit :

```html
<!--
  Admettons que nous disposons d'une même image en 2 tailles différentes :
  - 300px de large
  - 600px de large
-->

<img
  srcset="/image-300.jpg 300w,
          /image-600.jpg 600w"
  …
>
```
> **Note :** La valeur de `srcset` a été mise sur plusieurs lignes pour une meilleure lisibilité, mais on l'écrit généralement sur une seule ligne.

Ici, on indique explicitement au navigateur que l'on dispose de deux images (300px et 600px grâce au descripteur `w`) et que l'on souhaite qu'il choisisse la plus adaptée en fonction de la taille de la viewport (qu'il connaît).

C'est ensuite au navigateur de faire le choix de la meilleure image à charger.

Par exemple, un vieil iPhone 3 (disposant d'une taille d'écran de 320px) **va charger l'image de 300px de large**.

Le modèle au dessus (iPhone 4) dispose lui d'une taille d'écran de 640px (soit une densite 2x supérieure à l'iPhone 3 car physiquement, les deux devices font la même taille) et **va donc plutôt charger l'image de 600px de large**.

### Attribut `sizes`

Cet attribut vient en complément de `srcset`, est **n'est uniquement valable si on a choisi le descripteur `w`**.

Il permet d'indiquer au navigateur différentes **tailles de viewport** pour lesquelles on dispose d'une image adaptée.

Voici un exemple :

```html
<img
  srcset="/image-300.jpg 300w,
          /image-600.jpg 600w"
  sizes="(max-width: 400px) 200px,
         (max-width: 800px) 100vw,
         50vw"
  …	
>
```

Dans cet exemple, le navigateur est informé que :

- pour une taille de viewport inférieure ou égale à 400px, l'image devra s'afficher en 200px de large. Il prendra donc la valeur la plus proche, à savoir : `image-300.jpg`. Cependant, si la densité de pixels vaut 3 (= écrans super Rétina), alors il multipliera les 200px attendus par 3, et prendra donc l'image de 600px de large pour une meilleure qualité d'affichage.

- pour une taille de viewport inférieure ou égale à 800px, l'image devra s'afficher à 100% de la largeur de la viewport (c'est-à-dire 800px). Il choisira donc systématiquement `image-600.jpg`.

- si aucune des conditions précédentes n'est remplie, l'image devra s'afficher à 50% de la largeur de la viewport. C'est-à-dire que si on dispose d'une viewport faisant 820px, l'image s'affichera à 410px de large (= 50% de la viewport). Le navigateur choisira donc l'image de 300px de large car c'est la valeur la plus proche de 410px (pour un écran de 1x).

## Trouver le format optimal

Le format d'une image correspond à la **compression** utilisée pour stocker les données de l'image.

Il existe de nombreux formats d'images, mais les plus utilisés sont :

- **JPEG** : format de compression **perte**. Il est idéal pour les images contenant des couleurs vives et des dégradés. Il est également très utilisé pour les photos.
- **PNG** : format de compression **sans perte**. Il est idéal pour les images contenant des dégradés de transparence, des ombres, des contours et graphiques, etc.
- **GIF** : format de compression **sans perte**. Il est idéal pour les animations mais ne dispose que d'une palette de 256 couleurs.
- **SVG** : format vectoriel. Il est idéal pour les images contenant des formes géométriques, des textes, etc.
- **WebP** : format de compression **perte**. Il est idéal pour les images contenant des couleurs vives et des dégradés. Il est également très utilisé pour les photos. Il est plus performant que le JPEG et le PNG.
- **AVIF** : format de compression **perte**. Il s'agit d'un format plus récent que le WebP et gère plus de chose, mais est pour l'instant moins supporté par les navigateurs que WebP.

> Pour plus d'infos, lire l'article suivant : [AVIF vs WEBP](https://afosto.com/blog/avif-vs-webp-format/)

Avec [la nouvelle balise `<picture>`](https://developer.mozilla.org/fr/docs/Web/HTML/Element/picture), il est possible de définir **différents formats d'image** pour un même fichier (un peu de la même façon que pour une `<video>`) :

```html
<picture>
  <source type="image/avif" srcset="/image-450.avif 450w, /image-900.avif 900w">
  <source type="image/webp" srcset="/image-450.webp 450w, /image-900.webp 900w">
  <source type="image/jpeg" srcset="/image-450.jpg 450w, /image-900.jpg 900w">

  <img src="/image-450.jpg"
      srcset="/image-450.jpg 450w, /image-900.jpg 900w"
      alt="Texte alternatif">
</picture>
```

Ici, le navigateur est informé qu'il existe 3 formats d'image pour le même fichier :

- AVIF
- WebP
- JPEG

Il va donc choisir le format le plus adapté en fonction de la compatibilité du navigateur, et en tenant compte de l'attribut `srcset` défini sur la balise `<source>`.

Si le navigateur ne prend pas en charge `<picture>`, il va alors simplement charger la balise `<img>`.

## Décodage asynchrone

Il est aussi possible de demander le chargement d'une image **de manière asynchrone** au navigateur grâce à [l'attribut `decoding`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/decoding) :

```html
<img … decoding="async">
```

Il est recommandé par le MDN de le faire pour les images qui ne sont pas visibles immédiatement à l'écran, et ce en complément de `loading="lazy"`.

## Définir une priorité

Il est possible de définir une **priorité** à une image grâce à [l'attribut `fetchpriority`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/fetchPriority) :

```html
<img … fetchpriority="high">
```

Les valeurs possibles sont : `high`, `low` et `auto`.

---

Il est important de comprendre que toutes ces possibilités ont pour but de donner un maximum d'information au navigateur pour qu'il puisse charger les images de la meilleure façon possible, mais **le navigateur est libre de choisir la méthode qu'il souhaite** et vous ne serez pas forcément sûr de voir les images charger de la manière que vous avez définie.

L'article suivant reprend en détails les notions vues dans ce chapitre : [Optimal Images in HTML](https://www.builder.io/blog/fast-images#async-image-decoding).
