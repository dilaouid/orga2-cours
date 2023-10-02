# Les Media Queries

## Introduction aux _Media Queries_
Les _Media Queries_ sont une fonctionnalité CSS très utiles qui permettent de rendre une page Web réactive en adaptant la mise en page et le style en fonction des caractéristiques de l'appareil et de l'écran sur lequel le contenu est affiché (responsive)
Les _Media Queries_ sont couramment utilisées pour créer des sites Web qui s'ajustent automatiquement à différentes tailles d'écran, comme les smartphones, les tablettes et les ordinateurs de bureau.

## Syntaxe de base
Les Media Queries utilisent une syntaxe qui commence par le mot-clé `@media`, suivi de conditions spécifiques pour appliquer le style à certaines caractéristiques de l'écran.

Voici la structure de base d'une _Media Query_ :
```css
@media (condition) {
  /* Styles à appliquer en fonction de la condition */
}
```

## Exemples d'utilisation
### _Media Query_ pour les petits écrans
Supposons que nous voulions appliquer un style différent lorsque l'écran a une largeur maximale de 768 pixels, typiquement adapté aux smartphones en mode portrait. Voici comment vous pourriez le faire :

```css
@media (max-width: 768px) {
  body {
    background-color: black;
  }
}
```

### Media Query pour les écrans de taille moyenne
Si nous voulons appliquer un style différent aux écrans de taille moyenne, comme les tablettes, voici comment nous pourrions procéder :

```css
@media (min-width: 769px) and (max-width: 1024px) {
  body {
    background-color: blue;
  }
}
```

### _Media Query_ pour les écrans haute résolution
Pour cibler les écrans haute résolution (Retina), vous pouvez utiliser la propriété `min-resolution` :

```css
@media (min-resolution: 192dpi) {
  /* Styles pour les écrans haute résolution */
}
```

## _Media Queries_ avec d'autres caractéristiques
Outre les dimensions de l'écran, les _Media Queries_ peuvent également être utilisées pour cibler d'autres caractéristiques, telles que l'orientation de l'appareil, les modes d'affichage, etc............

Voici un exemple de _Media Query_ pour cibler les appareils en mode paysage :
```css
@media (orientation: landscape) {
  /* Styles pour les appareils en mode paysage */
}
```

## Ressource supplémentaires
- [**Documentation MDN sur les Media Queries**](https://developer.mozilla.org/fr/docs/Web/CSS/@media)
- [**Using Media Queries MDN**](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries)
