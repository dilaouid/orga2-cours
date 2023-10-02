# CSS : Révisions et concepts avancés

## Retour sur les bases

CSS signifie « _Cascading Style Sheets_ » (feuilles de style en cascade). C'est un langage de style qui permet de définir l'apparence d'un document HTML. Il est utilisé pour définir la mise en page, les polices, les couleurs, les marges, etc.

On l'inclus dans une page HTML avec la balise `<link>` dans l'en-tête de la page :

```html
<!DOCTYPE html>
<html lang="fr">
  <head>
    …

    <link rel="stylesheet" href="style.css">
  </head>

…
```

Dans le fichier `.css`, on définit les règles de style en sélectionnant des éléments HTML avec des sélecteurs, puis en leur appliquant des propriétés CSS :

<p align="center">
  <img src="./images/css.png" width="400">
</p>

Un sélecteur permet de **cibler un groupe de balises HTML afin de leur attribuer du style.**

#### Sélecteur de balise HTML simple

```css
p {
  color: red;
}
```

Cible toutes les balises `<p>` de la page HTML et leur applique la couleur de texte rouge.

#### Sélecteur de parenté indirect

```css
header a {
  background-color: white;
}
```

Cible toutes les balises HTML `<a>` se trouvant à l'intérieur d'un `<header>`, à quelque niveau que ce soit :

```html
<header>
  <a href="index.html">Accueil</a> <!-- ✅ ciblé -->
</header>

<header>
  <p>
    <a href="index.html">Accueil</a> <!-- ✅ ciblé -->
  </p>
</header>

<a href="http://google.fr">Google</a> <!-- ❌ non ciblé -->
```

#### Sélecteur de parenté direct : `>`

```css
section > p {
  border: thin solid silver;
}
```

Cible toutes les balises HTML `<p>` se trouvant **directement** à l'intérieur d'une `<section>`

```html
<section>
  <div class="inner">
    <p>Lorem ipsum dolor sit amet.</p> <!-- ❌ non ciblé -->
  </div>
</section>

<div>
  <p>Lorem ipsum dolor sit amet.</p> <!-- ❌ non ciblé -->
</div>

<section>
  <p>Lorem ipsum dolor sit amet.</p><!-- ✅ ciblé, car <p> est un enfant direct de <section> -->
</section>
```

#### Sélecteur d'adjacence directe : `+`

```css
header + section {
  font-size: 20px;
}
```

Cible uniquement une balise `<section>` se trouvant **juste après** une balise `<header>` :

```html
<header>Entête</header>
<section>Lorem ipsum dolor.</section><!-- ✅ ciblé -->
<section>Ab quasi, dolorum.</section><!-- ❌ non ciblé -->
<section>Eum, omnis, velit.</section><!-- ❌ non ciblé -->
```

#### Sélecteur d'adjacence indirecte : `~`

```css
header ~ section {
  font-size: 20px;
}
```

Cible **toutes** les balises `<section>` se trouvant après une balise `<header>` et qui partagent le même parent :

```html
<section>Lorem ipsum dolor.</section><!-- ❌ non ciblé -->
<header>Entête</header>
<section>Lorem ipsum dolor.</section><!-- ✅ ciblé -->
<section>Ab quasi, dolorum.</section><!-- ✅ ciblé -->
<p>Lorem ipsum dolor sit amet.</p>
<section>Eum, omnis, velit.</section><!-- ✅ ciblé -->
```

#### Sélection par classe : `.class`

```css
.button-danger {
  background-color: red;
}
```

Cible tous les éléments HTML qui **implémentent la classe nommée `button-danger`**

```html
<a href="#" class="button-danger">Fail !</a>
<button class="button-danger">Alert !</button>
```

> **Note**
>
> Une classe a pour vocation d'être **réutilisable** et **modulaire**.

> **Warning**
>
> Evitez les noms de classe du style `.partie1` ou `.rouge`

#### Sélection par ID : `#id`

```css
#about-us {
  color: black;
}
```

Cible **l'unique** élément HTML qui portera l'identifiant `about-us` :

```html
<section id="our-job">[...]</section>
<section id="about-us">[...]</section>
<section id="contact-us">[...]</section><!-- ✅ ciblé -->
```

> **Note**
>
> Un ID a pour vocation d'être **unique** et **explicite**.

> **Warning**
>
> Evitez les identifiants du style `#section1 `ou `#partieB`

#### Sélection par attribut : `[attr]`

```css
img[alt] {
  border: thick solid gray;
}
```

Cible exclusivement les balises `<img>` qui **possèdent un attribut `alt`**

```css
a[href='#'] {
  font-size: 14px;
}
```

Cible exclusivement les balises `<a>` qui **possèdent un attribut href valant exactement `#`**

Il existe aussi des sélecteurs d'attributs plus complexes. On peut par exemple cibler les liens dont l'attribut `href` **commence par** `http` :

> ```css
> a[href^='http'] { /* … */ }
> ```
> ```html
> <a href="http://google.fr">Google</a>
> <a href="https://google.fr">Google</a>
> ```


Tous les liens dont l'attribut `href` **se termine par** `.pdf` :

> ```css
> a[href$='.pdf'] { /* … */ }
> ```
> ```html
> <a href="http://google.fr/mon-document.pdf">Mon document</a>
> ```


Tous les liens dont l'attribut `href` **contient** `google` :

> ```css
> a[href*='google'] { /* … */ }
> ```
> ```html
> <a href="http://google.fr">Google</a>
> <a href="/?search=google">Google</a>
> ```


Toutes les images dont l'attribut `alt` contient une **liste d'éléments séparés par des espaces**, et dont l'un d'entre eux est `google` :

> ```css
> img[alt~='google'] { /* … */ }
> ```
> ```html
> <img … alt="illustration google exemple" />
> ```


Toutes les images dont l'attribut `alt` contient une **liste d'éléments séparés par des tirets**, et dont l'un d'entre eux est `google` :

> ```css
> img[alt|='google'] { /* … */ }
> ```
> ```html
> <img … alt="illustration-google-exemple" />
> ```


#### Sélection répétitive : `:is()`

Il arrive parfois que l'on veuille cibler plusieurs éléments ayants le même parent :

```css
.active a,
.active button,
.active label {
  …
}
```

Avec la pseudo-classe `:is()`, on peut cibler ces plusieurs éléments en une seule ligne :

```css
/* Attention à ne pas oublier l'espace « » entre le sélecteur et :is() */
.active :is (a, button, label) {
  …
}
```

Compatibilité sur tous les navigateurs modernes : https://caniuse.com/?search=%3Ais

#### Sélection relationnelle : `:has()`

> **Warning**
>
> Cette fonctionnalité n'est pas encore supportée par tous les navigateurs (ex: Firefox)
> (https://caniuse.com/?search=%3Ahas)

Ce sélecteur permet de sélectionner un élément qui **contient** un autre élément.

> ```css
> a {
>   text-decoration: underline;
> }
> 
> a:has(img, video) {
>   text-decoration: none;
> }
> ```
> ```html
> <a href="https://google.fr">Google</a><!-- Lien souligné -->
> <a href="https://google.fr"><img … /></a>  <!-- Lien non souligné -->
> <a href="https://google.fr"><video … /></a>  <!-- Lien non souligné -->
> ```

Une bonne ressource à lire sur ces deux derniers sélecteurs : [Simpler CSS Selectors With :is()](https://www.builder.io/blog/css-is), sur le blog de [Builder.io](https://www.builder.io/).

### Poids des sélecteurs

Les sélecteurs sont classés par ordre de **poids**. Le poids d'un sélecteur est déterminé par le nombre de sélecteurs qu'il contient.

Soit le HTML suivant :

```html
<div class="container" id="careers">
  <h1>Join Us!</h1>
  <p>We need you!</p>
</div>
```

Et les sélecteurs CSS suivants :

```css
.container h1 {
  color: orange;
}

#careers h1 {
  color: blue;
}

div h1 {
  color: red;
}
```

> <details>
  > <summary>Tous ces sélecteurs ciblent bien le titre `&lt;h1&gt;`, mais quelle couleur ce dernier se verra t-il appliqué ?</summary>
  >
  > Réponse : `color: blue;` car le sélecteur `#careers h1` est le plus **spécifique**.
  > 
> </details>

(Annexe : [Poids des sélecteurs CSS](https://developer.mozilla.org/fr/docs/Web/CSS/Specificity) sur le MDN)


### Pseudo-classes

Il existe également de nombreuses pseudo-classes qui permettent de cibler des éléments HTML en fonction de leur **état** :

```css
:root
:nth-child(n)
:nth-last-child(n)
:nth-of-type(n)
:nth-last-of-type(n)
:first-child
:last-child
:first-of-type
:last-of-type
:only-child
:only-of-type
:empty
:not(…)
:target
:lang(…)
```

#### Pseudo-classes de formulaires

```css
:valid
:invalid
:required
:optional
:enabled
:disabled
:checked
:in-range
:out-of-range
:read-only
:read-write
:default
```

### Pseudo-éléments

Les pseudo-classes sélectionnent des éléments **qui existent déjà**.

Les pseudo-éléments **créent des "faux" éléments** que l'on peut personnaliser.

```css
::first-line
::first-letter
::before
::after
::selection
::cue
::slotted
```

## Jouer avec les sélecteurs :

### [CSS Diner](http://flukeout.github.io/)
<p align="center">
  <a href="https://flukeout.github.io/">
    <img src="./images/cssdiner.jpg" width="600" />

  </a>
</p>

---

## Unités de mesures

Il existe plusieurs unités de mesures pour les tailles, les marges, les paddings, etc.

Nous allons ici nous concentrer sur les unités relatives.

#### `em`

L'unité `em` est relative à la taille de la police de l'élément parent.

> ```css
> p { font-size: 1.5em; }
> p > span { font-size: 2em; }
> ```
> ```html
> <p>
>   Lorem ipsum dolor sit amet, consectetur adipiscing elit.
>   <span>
>     Lorem ipsum dolor sit amet, consectetur adipiscing elit.
>   </span>
> </p>
> ```

La taille du `<span>` sera donc égale à **2 fois la taille de la police du `<p>`**, à savoir **2 fois 1.5em**.

#### `rem`

L'unité `rem` signifie « root em » et est relative à la taille de la police de la **racine du document**.

> ```css
> html { font-size: 16px; }
> p { font-size: 1.5rem; }
> p > span { font-size: 2rem; }
> ```
> ```html
> <p>
>   Lorem ipsum dolor sit amet, consectetur adipiscing elit.
>   <span>
>     Lorem ipsum dolor sit amet, consectetur adipiscing elit.
>   </span>
> </p>
> ```

La taille du `<span>` sera donc égale à **2 fois la taille de la police définie à la racine `html`**, à savoir **2 fois 16px**.

#### `vw` / `vh`

L'unité `vw` signifie « viewport width » et est relative à la largeur de la fenêtre du navigateur.

L'unité `vh` signifie « viewport height » et est relative à la hauteur de la fenêtre du navigateur.

> ```css
> .container {
>   background-color: yellow;
>   width: 75vw;
>   height: 50vh;
> }
> ```
> ```html
> <div class="container"></div>
> ```

La largeur du `.container` sera donc égale à **75% de la largeur de la fenêtre du navigateur** et sa hauteur à **50% de la hauteur de la fenêtre du navigateur**.

Il existe de nombreuses autres unités en CSS, qui sont toutes détaillées de manière exhaustive sur le [MDN : Valeurs et unités CSS](https://developer.mozilla.org/fr/docs/Web/CSS/CSS_Values_and_Units).