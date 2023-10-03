### 1. Script Inline

Il s'agit d'écrire directement le code JavaScript dans votre document HTML à l'aide de la balise `<script>`. C'est la méthode la plus simple, mais elle n'est pas recommandée pour de grands scripts ou pour réutiliser le même script sur plusieurs pages.

**Exemple :**

```html
<!DOCTYPE html>
<html>
<head>
    <title>Il faut cliquer!</title>
</head>
<body>

<h1>Un titre</h1>
<button onclick="showAlert()">Cliquez-moi !</button>

<script>
    function showAlert() {
        alert('Hello World!');
    }
</script>

</body>
</html>
```

---

### 2. Script Externe

Cette méthode consiste à placer votre code JavaScript dans un fichier séparé (généralement avec l'extension `.js`) et à le référencer dans votre document HTML. C'est la méthode recommandée car elle permet de séparer le contenu (HTML), la présentation (CSS) et la logique (JavaScript).

**Exemple :**

Supposons que vous ayez un fichier nommé `script.js` contenant :

```javascript
function showAlert() {
    alert('Hello World');
}
```

Vous pouvez l'intégrer dans votre document HTML comme suit :

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page avec bouton inutile</title>
</head>
<body>

<h1>Un titre</h1>
<button onclick="showAlert()">Cliquez-moi !</button>

<!-- Intégration du script externe -->
<script src="script.js"></script>

</body>
</html>
```

---

### A savoir !

- Placez généralement la balise `<script>` juste avant la balise de fermeture `</body>` pour éviter de bloquer le rendu de la page.
- Si vous utilisez plusieurs scripts externes, l'ordre dans lequel vous les intégrez peut être important, surtout si un script dépend d'un autre.
- Un seul fichier JS, si vous n'utilisez pas de bundler comme Webpack peut se trouver rapidement trop gros. Pensez à bien décomposez en passant par plusieurs fichiers JS si vous n'utilisez pas de bundler.