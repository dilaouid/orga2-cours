# Positionnement moderne avec le module _Flexbox_

## Introduction au Flexbox

Le positionnement des éléments dans une mise en page web peut parfois être un défi. Heureusement, avec l'introduction du module _Flexbox_ (Flexible Box), nous disposons d'un outil puissant pour gérer le positionnement des éléments de manière efficace et flexible.

Le module _Flexbox_ introduit un modèle de disposition unidimensionnel, ce qui signifie qu'il est particulièrement bien adapté à l'alignement et à la distribution des éléments dans une seule direction (horizontale ou verticale) le long d'un axe principal.

## Avantages du _Flexbox_

Le _Flexbox_ offre plusieurs avantages pour le positionnement moderne des éléments :

1. **Alignement simple :** Le _Flexbox_ permet d'aligner facilement les éléments le long de l'axe principal et secondaire, ce qui simplifie grandement les mises en page complexes.

2. **Distribution équitable :** Avec le _Flexbox_, vous pouvez répartir l'espace disponible entre les éléments de manière équitable, ce qui est particulièrement utile pour créer des barres de navigation, des pieds de page et d'autres éléments de mise en page.

3. **Réorganisation facile :** Les éléments _Flexbox_ peuvent être réorganisés en fonction de la taille de l'écran ou d'autres critères, ce qui facilite la création de mises en page réactives.

4. **Gestion automatique de la taille des éléments :** Le _Flexbox_ gère automatiquement la taille des éléments en fonction de leur contenu ou des contraintes de mise en page, réduisant ainsi le besoin de calculer les dimensions manuellement.

## Utilisation du _Flexbox_

Le _Flexbox_ est utilisé en appliquant la propriété CSS `display: flex` à un conteneur parent. Une fois que cette propriété est définie, les éléments enfants du conteneur deviennent automatiquement des éléments _Flexbox_ et obéissent aux règles de mise en page spécifiées.

Le _Flexbox_ utilise un ensemble de propriétés qui contrôlent le comportement des éléments enfants, y compris :

- `flex-direction` : Détermine la direction de l'axe principal (horizontal ou vertical).
    1. **`row` (par défaut) :**
    Cette valeur aligne les éléments horizontalement, de gauche à droite.

    ```css
    .container {
        display: flex;
        flex-direction: row;
    }
    ```

    2. **`row-reverse` :**
    Cette valeur aligne les éléments horizontalement, de droite à gauche.

    ```css
    .container {
        display: flex;
        flex-direction: row-reverse;
    }
    ```

    3. **`column` :**
    Cette valeur aligne les éléments verticalement, de haut en bas.

    ```css
    .container {
        display: flex;
        flex-direction: column;
    }
    ```

    4. **`column-reverse` :**
    Cette valeur aligne les éléments verticalement, de bas en haut.

    ```css
    .container {
        display: flex;
        flex-direction: column-reverse;
    }
    ```
    Lorsque vous modifiez la valeur de `flex-direction` dans le conteneur parent, tous les éléments enfants adoptent la nouvelle disposition en fonction de la direction spécifiée. Cela vous permet de créer des mises en page flexibles en ajustant simplement cette propriété.
- `justify-content` permet de contrôler l'alignement horizontal des éléments au sein du conteneur flex.
    1. **`flex-start` (par défaut) :**
    Les éléments sont alignés au début de l'axe principal.

    ```css
    .container {
        display: flex;
        justify-content: flex-start;
    }
    ```

    2. **`flex-end` :**
    Les éléments sont alignés à la fin de l'axe principal.

    ```css
    .container {
        display: flex;
        justify-content: flex-end;
    }
    ```

    3. **`center` :**
    Les éléments sont centrés le long de l'axe principal.

    ```css
    .container {
        display: flex;
        justify-content: center;
    }
    ```

    4. **`space-between` :**
    Les éléments sont répartis également avec un espace entre eux.

    ```css
    .container {
        display: flex;
        justify-content: space-between;
    }
    ```

    5. **`space-around` :**
    Les éléments sont répartis également avec un espace autour d'eux.

    ```css
    .container {
        display: flex;
        justify-content: space-around;
    }
    ```
- `align-items` permet de contrôler l'alignement vertical des éléments au sein du conteneur flex.
    1. **`flex-start` (par défaut) :**
    Les éléments sont alignés au début de l'axe secondaire.

    ```css
    .container {
        display: flex;
        align-items: flex-start;
    }
    ```

    2. **`flex-end` :**
    Les éléments sont alignés à la fin de l'axe secondaire.

    ```css
    .container {
        display: flex;
        align-items: flex-end;
    }
    ```

    3. **`center` :**
    Les éléments sont centrés le long de l'axe secondaire.

    ```css
    .container {
        display: flex;
        align-items: center;
    }
    ```

    4. **`baseline` :**
    Les éléments sont alignés en fonction de leur ligne de base (si applicable).

    ```css
    .container {
        display: flex;
        align-items: baseline;
    }
    ```

    5. **`stretch` :**
    Les éléments sont étirés pour occuper toute la hauteur de l'axe secondaire.

    ```css
    .container {
        display: flex;
        align-items: stretch;
    }
    ```
- `flex-grow`, `flex-shrink`, `flex-basis` : Contrôlent la flexibilité des éléments.
    1. **`flex-grow` :**
    La propriété `flex-grow` détermine comment l'espace disponible est distribué entre les éléments flexibles. Plus la valeur est élevée, plus l'élément grossira par rapport aux autres.

    ```css
    .item {
        flex-grow: 1; /* ou toute autre valeur numérique */
    }
    ```

    2. **`flex-shrink` :**
    La propriété `flex-shrink` définit la capacité d'un élément à rétrécir par rapport aux autres lorsqu'il y a un manque d'espace disponible.

    ```css
    .item {
        flex-shrink: 1; /* ou toute autre valeur numérique */
    }
    ```

    3. **`flex-basis` :**
    La propriété `flex-basis` détermine la taille de base d'un élément flexible avant que l'espace restant ne soit distribué.

    ```css
    .item {
        flex-basis: auto; /* ou toute autre valeur */
    }
    ```

    Vous pouvez également combiner ces trois propriétés en une seule propriété `flex` :

    ```css
    .item {
        flex: [flex-grow] [flex-shrink] [flex-basis];
    }
    ```

    Par exemple :
    ```css
    .item {
        flex: 1 1 auto;
    }
    ```
    L'utilisation de ces propriétés vous permet de contrôler la manière dont les éléments flexibles se développent, rétrécissent et se basent sur l'espace disponible dans le conteneur _Flexbox_.

## Entraînement avec _Flexbox Froggy_
[_Flexbox Froggy_](https://flexboxfroggy.com/#fr)

## Ressources supplémentaires
- [**Documentation complète sur les FlexBox**](css-tricks.com/snippets/css/a-guide-to-flexbox/)
