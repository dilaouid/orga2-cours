# WebFonts

Les webfonts sont des polices de caractères qui peuvent être utilisées sur des sites web. Elles permettent aux concepteurs de sites web d’utiliser des polices personnalisées qui ne sont pas nécessairement installées sur l’ordinateur de l’utilisateur.

À une certaine époque, l'utilisation de polices était encore très limitée. Mais les standarts du web ont évolué ainsi que les navigateurs web, qui permettent de prendre en charge l'utilisation de fichiers de police personnalisés pour le Web.

## La règle `@font-face`

La règle `@font-face` en CSS permet de définir une police personnalisée à utiliser sur un site web.

Voici la syntaxe générale de cette règle :

```css
@font-face {
  font-family: '<NOM>';
  src: url('<CHEMIN>') format('<FORMAT>');
}
```

Dans cet exemple, on utilise les éléments suivants :

- **`font-family`** :
  Indique le nom donné à la police personnalisée. Il est totalement libre et s'utilise plus tard dans le code CSS pour appliquer cette police à des éléments de la page.

- **`src`** :
  Correspond au fichier de police à utiliser. Ce fichier contient les informations sur les glyphes de la police.

- **`format`** :
  Indique le format du fichier de police fourni via `src`. Les formats couramment utilisés pour le Web sont `eot`, `woff`, `woff2`, `truetype` et `svg`.

Voici un exemple simple d'utilisation de la règle `@font-face` pour définir une police personnalisée :

```css
/* Déclaration d'une nouvelle police nommée "Open Sans" */
@font-face {
  font-family: 'Open Sans';
  src: url('fonts/OpenSans-Regular.ttf') format('ttf');
}

/* Utilisation de la police personnalisée dans le CSS */
body {
  font-family: 'Open Sans', sans-serif;
}
```

> **Note**
> On peut trouver le fichier de police **_Open Sans_** (qui est open-source) à l'adresse suivante : https://github.com/googlefonts/opensans/blob/main/fonts/ttf/OpenSans-Regular.ttf
> Conformément à l'exemple ci-dessus, il faudrait placer ce fichier dans le dossier `/fonts/`

La règle `@font-face` permet l'utilisation d'autres descripteurs, pour préciser la **graisse** ou le **style** de la police.

Par exemple, il existe pour la police "_Open Sans_" des fichiers spécifiques pour de l'italique ou du gras.

On doit alors utiliser les descripteurs dans des règles `@font-face` spécifiques pour chaque fichier :

```css
@font-face {
  font-family: 'Open Sans';
  font-weight: 600; /* 600 correspond à "semi-bold" */
  font-style: normal;
  src: url('fonts/OpenSans-SemiBold.ttf') format('ttf');
}

@font-face {
  font-family: 'Open Sans';
  font-weight: 400; /* 400 correspond à "regular" */
  font-style: italic;
  src: url('fonts/OpenSans-Italic.ttf') format('ttf');
}

@font-face {
  font-family: 'Open Sans';
  font-weight: 700; /* 700 correspond à "bold" */
  font-style: italic;
  src: url('fonts/OpenSans-BoldItalic.ttf') format('ttf');
}
```

Ainsi, lorsqu'on utilisera par exemple la règle suivante dans le CSS, le navigateur utilisera le fichier police correspondant à la graisse et au style demandés, à savoir ici `OpenSans-BoldItalic.ttf` :

```css
body {
  font-family: 'Open Sans', sans-serif;
  font-weight: 700;
  font-style: italic;
}
```

### Formats de fichiers de police

Il existe plusieurs formats de fichiers pour les webfonts, notamment `eot`, `woff`, `woff2`, `ttf` et `svg`.

- **EOT** (Embedded OpenType) : Ce format a été développé par Microsoft et est principalement utilisé pour les versions antérieures d'Internet Explorer, jusqu'à la version 6. Il n'est supporté par aucun autre navigateur.

```css
@font-face {
  font-family: 'MaFont';
  src: url('font.eot');
}
```

> **Warning**
> Ne pas confondre `Internet Explorer` et `Microsoft Edge`. Ce dernier est un excellent navigateur qui prend notamment en charge tous les formats de fichiers de police.

- **WOFF** (Web Open Font Format) : Ce format a été développé pour le web et est pris en charge par tous les navigateurs modernes. Il offre une compression des données, ce qui permet un chargement plus rapide des polices. Il est compatible à partir d'Internet Explorer 9.

```css
@font-face {
  font-family: 'MaFont';
  src: url('font.woff') format('woff');
}
```

- **WOFF2** : C'est la deuxième version du format WOFF, qui offre une meilleure compression des données et un chargement encore plus rapide des polices. Il n'est cependant pas compatible avec Internet Explorer (toutes versions confondues).

```css
@font-face {
  font-family: 'MaFont';
  src: url('font.woff2') format('woff2');
}
```

- **TTF** (TrueType Font) : Ce format est largement utilisé pour les polices de caractères sur les ordinateurs et les appareils mobiles. Il est pris en charge par tous les navigateurs modernes.

```css
@font-face {
  font-family: 'MaFont';
  src: url('font.ttf') format('truetype');
}
```

- **SVG** (Scalable Vector Graphics) : Ce format est utilisé pour les polices vectorielles, qui peuvent être redimensionnées sans perte de qualité. Il est principalement utilisé pour les appareils mobiles avec des écrans haute résolution.

```css
@font-face {
  font-family: 'MaFont';
  src: url('font.svg#font-id') format('svg');
}
```

> **Note**
> Un fichier de police SVG peut contenir des tracés pour **plusieurs polices**, qui sont alors identifiées avec un ID unique au sein du fichier `.svg`. Le symbole hashtag **`#`** permet de cibler le tracé à utiliser pour cette déclaration.

À noter que l'on peut définir plusieurs formats pour une même police en les séparant par une virgule, pour maximiser la compatibilité. Le navigateur choisira alors le premier format qu'il prend en charge :

```css
@font-face {
  font-family: 'MaFont';
  src: url('font.eot'),
       url('font.woff') format('woff'),
       url('font.ttf') format('truetype'),
       url('font.svg#font-id') format('svg');
}
```

Il faut bien sûr disposer des fichiers de police dans les différents formats pour pouvoir les utiliser.

Le service gratuit [Font Squirrel](https://www.fontsquirrel.com/) propose un outil en ligne pour convertir des fichiers de police dans différents formats, à partir d'un fichier source :

> **[Font Squirrel - Webfont Generator](https://www.fontsquirrel.com/tools/webfont-generator)**

Ainsi, si l'on dispose d'un fichier de police au format `.ttf`, on peut générer les fichiers de police dans les différents formats, et les télécharger ensuite.

> **Note**
>
> Le site **[DaFont](https://www.dafont.com/)** répertorie de nombreux fichiers de police, dont certains sont disponibles en téléchargement gratuit.

### OpenType et les polices variables

OpenType est un format de police développé conjointement par Microsoft et Adobe. Il prend en charge un large éventail de fonctionnalités avancées, telles que les ligatures, les petites capitales et les variantes contextuelles.

Une fonctionnalité intéressante d'OpenType est la prise en charge des polices variables. Les polices variables permettent de modifier dynamiquement l'apparence d'une police en utilisant des axes prédéfinis, tels que la **largeur**, la **graisse** et l'**inclinaison**.

Pour utiliser une police variable en CSS, on utilise la propriété `font-variation-settings`. Cette propriété prend une liste de paires clé-valeur, où la clé est l'identifiant de l'axe et la valeur est la valeur à utiliser pour cet axe.

```css
/* Déclare une police truetype nommée "PoliceVariable" */
@font-face {
  font-family: 'PoliceVariable';
  src: url('fonts/police-variable.ttf') format('truetype');
}

h1 {
  font-family: 'PoliceVariable';

  font-variation-settings: 'wght' 700, 'wdth' 80, 'ital' 0.5;
  /* Modification de l'apparence de la police :
      - graisse : 700
      - largeur : 80
      - inclinaison : 0.5
    */
}
```

Le site **[Variable Fonts](https://v-fonts.com/)** propose une liste de polices variables disponibles sur le web.

## Le service _Google Fonts_

Il n'est parfois pas très pratique de devoir télécharger des fichiers de police pour les intégrer dans un site web, surtout s'il s'agit de polices open-source connues comme _Open Sans_ ou _Roboto_.

Il existe différents services qui permettent d'utiliser des webfonts sans avoir à télécharger les fichiers de police, et sans avoir à les héberger sur son propre serveur.

Le plus populaire est **[Google Fonts](https://fonts.google.com/)**. Ce service offre une grande variété de polices gratuites et faciles à intégrer dans un site web.

On peut choisir une ou plusieurs polices parmi la liste proposée, puis intégrer simplement le code HTML et CSS fourni par Google Fonts dans la page HTML.

Par exemple, pour intégrer la police _Open Sans_ dans une page HTML, on peut utiliser le code suivant :

```html
<link href="https://fonts.googleapis.com/css?family=Open+Sans" rel="stylesheet" />
```

On peut ensuite utiliser cette police dans le CSS de la page :

```css
body {
  font-family: 'Open Sans', sans-serif;
}
```
