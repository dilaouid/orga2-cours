# Positionnement avancé avec Grid Layout module

## Introduction au Grid Layout

Le _Grid Layout module_ est une technologie de positionnement avancée en CSS qui permet de créer des mises en page complexes et réactives en utilisant une grille bidimensionnelle. Contrairement à _Flexbox_ qui se concentre principalement sur un seul axe (ligne ou colonne), _Grid Layout_ permet de contrôler la disposition des éléments sur les deux axes (lignes et colonnes) en même temps.

Le _Grid Layout_ est particulièrement utile pour les mises en page structurées, comme les tableaux, les grilles de produits et les mises en page de type magazine........ Il offre un contrôle précis sur la position des éléments, tout en permettant une grande flexibilité.

## Création d'une grille

Pour créer une grille en utilisant le _Grid Layout_, vous devez d'abord définir un container parent en tant que "grille" en appliquant la propriété `display: grid;`. Ensuite, vous spécifiez le nombre de lignes et de colonnes que vous souhaitez dans la grille à l'aide des propriétés `grid-template-rows` et `grid-template-columns`.

Par exemple, le code CSS suivant crée une grille avec trois lignes et trois colonnes de largeurs égales :

```css
.container {
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: repeat(3, 1fr);
}
```

- `grid-template-rows: repeat(3, 1fr);` : Cette ligne détermine les lignes de la grille. Elle crée trois lignes de largeur égale. La fonction `repeat(3, 1fr)` indique que nous voulons répéter la valeur "1fr" (une *fraction flexible*) trois fois pour créer trois lignes.

- `grid-template-columns: repeat(3, 1fr);` : Cette ligne détermine les colonnes de la grille. Elle crée trois colonnes de largeur égale, tout comme pour les lignes.

Cette grille a trois lignes et trois colonnes de largeur égale, formant ainsi une grille 3x3. 

## Placement des éléments dans la grille

Une fois que la grille est définie, vous pouvez placer les éléments dans les cellules de la grille en utilisant les propriétés `grid-row` et `grid-column`. Vous pouvez spécifier le numéro de ligne ou de colonne pour positionner l'élément.

Par exemple, pour placer un élément à la deuxième ligne et la troisième colonne :

```css
.item {
  grid-row: 2;
  grid-column: 3;
}
```

## Gestion de l'espace

_Grid Layout_ offre également des fonctionnalités puissantes pour gérer l'espace entre les éléments et autour d'eux. Vous pouvez utiliser les propriétés `grid-gap`, `grid-row-gap` et `grid-column-gap` pour contrôler les espaces entre les lignes et les colonnes.

Par exemple, pour créer un espacement de 20 pixels entre les lignes et les colonnes :

```css
.container {
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
}
```

## Création de mises en page responsives

L'un des avantages majeurs de _Grid Layout_ est sa capacité à créer des mises en page responsives sans avoir à recourir à des médias queries complexes. En utilisant les unités de mesure flexibles comme `fr` (fraction) et `auto`, vous pouvez créer des mises en page qui sont facilement responsives.

## Entraînement avec _Grid Garden_

Pour pratiquer et approfondir vos compétences en _Grid Layout_, vous pouvez utiliser des ressources en ligne interactives telles que le jeu [Grid Garden](https://cssgridgarden.com/) 