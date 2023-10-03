### Introduction

Le DOM (Document Object Model) est une représentation structurée de documents HTML ou XML sous forme "d'arbres". Lorsque vous chargez une page web dans un navigateur, celui-ci crée un modèle du contenu de cette page. JavaScript peut être utilisé pour interagir avec cette structure, vous permettant de manipuler le contenu, la structure et le style d'une page web en temps réel.

---

### Qu'est-ce que le DOM ?

- Le DOM n'est **pas** une partie de JS. C'est une API (_Interface de Programmation d'Application_) pour les documents HTML et XML. Le JS, c'est sa manipulation.
- Il représente la page de manière à ce que les programmes puissent la modifier (changer le contenu, la structure, le style.......).
- Chaque élément HTML est considéré comme un objet "noeud" du DOM que vous pouvez sélectionner et manipuler.

---

### Structure du DOM

Imaginez le DOM comme un arbre d'objets avec des branches et des feuilles. Par exemple, pour le code HTML assez simple suivant :

```html
<html>
  <head>
    <title>Mon titre</title>
  </head>
  <body>
    <h1>Mon titre principal</h1>
    <p>Ceci est un paragraphe.</p>
  </body>
</html>
```

Le modèle DOM ressemblera à :

```
DOCUMENT
│
├── HTML
│   ├── HEAD
│   │   └── TITLE
│   │
│   └── BODY
│       ├── H1
│       └── P
```

---

### Sélectionner des éléments du DOM avec JavaScript

Pour manipuler le DOM, vous devez d'abord sélectionner l'élément (ou les éléments) avec lequel vous souhaitez travailler. Voici quelques méthodes courantes pour sélectionner des éléments :

1. **getElementById()** : Sélectionne un élément par son attribut `id`.

    ```js
    const titre = document.getElementById("monTitre"); // retourne null ou un élément, comme il ne doit y avoir qu'une fois un même id dans une page
    ```

2. **getElementsByClassName()** : Sélectionne tous les éléments avec une classe spécifique.

    ```js
    const multipleElements = document.getElementsByClassName("maClasse"); // pareil, retourne plusieurs éléments ou rien
    ```

3. **getElementsByTagName()** : Sélectionne tous les éléments avec un nom de balise spécifique.

    ```js
    const paragraphes = document.getElementsByTagName("p"); // de même
    ```

4. **querySelector()** : Sélectionne le premier élément qui correspond à un sélecteur CSS spécifié.

    ```js
    const premierItem = document.querySelector(".maClasse"); // sélectionne seulement un seul élément
    ```

5. **querySelectorAll()** : Sélectionne tous les éléments qui correspondent à un sélecteur CSS spécifié.

    ```js
    const tousLesItems = document.querySelectorAll(".maClasse"); // sélectionne du coup tout les éléments correspondant au sélecteur
    ```

> Note
>
> Notez que parfois, Element est au pluriel, ou au singulier. Lorsqu'il est au pluriel, il retournera null ou un tableau d'Elements, tandis que s'il est au singulier, il retournera null ou un Element.

---

### Manipuler le DOM

Une fois que vous avez sélectionné un ou plusieurs éléments, vous pouvez les manipuler. Voici quelques opérations courantes :

- **Changer le contenu** :

    ```js
    const paragraphe = document.getElementById("monParagraphe"); // il y a un seul id "monParagraphe" dans la page: ca ne retourne que un seul élément
    paragraphe.textContent = "Bonjour je suis du nouveau contenu!";
    ```

- **Changer le style** :

    ```js
    const titre = document.getElementById("monTitre");
    titre.style.color = "red";
    ```

- **Ajouter ou supprimer des classes** :

    ```js
    const element = document.querySelector(".maClasse");
    element.classList.add("uneAutreClasse"); // ajoute une classe à l'élément sélectionné
    element.classList.remove("maClasse"); // supprime une classe de l'élément sélectionné
    ```

- **Créer, ajouter ou supprimer des éléments** :

    ```js
    const nouveauParagraphe = document.createElement("p");
    nouveauParagraphe.textContent = "Un paragraphe ajouté!";
    document.body.appendChild(nouveauParagraphe); // j'ajoute l'élement <p> tout juste crée à mon body (document.body)

    const ancienParagraphe = document.getElementById("aSupprimer");
    document.body.removeChild(ancienParagraphe); // je supprime mon élément avec un id "
    ```

    Ici, on ajoute et supprime des éléments directement dans le body. Mais il est possible d'utiliser la méthode `.appendChild()` sur un autre élément que vous aurez identifié au préalable, par exemple:

    ```js
    const box = document.getElementById("box"); // j'identifie l'élément auquel je veux ajouter un paragraphe

    const paragraph = document.createElement("p"); // je crée l'élément que je veux ajouter

    box.appendChild(paragraph); // ... et je l'append ! Du coup, mon paragraphe s'ajoute à mon élement avec un id="box"
    ```