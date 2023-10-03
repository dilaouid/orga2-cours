| Caractéristique       | `var` | `let` | `const` |
|-----------------------|-------|-------|---------|
| **Portée**            | Fonction | Bloc | Bloc   |
| **Hoisting**          | Oui   | Oui   | Oui     |
| **Redéclaration**     | Oui   | Non   | Non     |
| **Réassignation**     | Oui   | Oui   | Non     |

**Explications :**

- **Portée** :
  - `var` est limité à la portée de la fonction dans laquelle il est déclaré, ou à la portée globale si déclaré en dehors d'une fonction.
  - `let` et `const` sont limités à la portée du bloc dans lequel ils sont déclarés (par exemple, à l'intérieur d'une boucle ou d'une condition). 

- **Hoisting** :
  Toutes les déclarations (`var`, `let`, `const`) sont "hoistées" (ou "remontées") au sommet de leur portée, mais seulement la déclaration, pas l'initialisation. Cela signifie que vous pouvez accéder à une variable avant sa déclaration avec `var`, mais elle sera `undefined`. Avec `let` et `const`, cela générera une erreur.

- **Redéclaration** :
  Dans une même portée, vous pouvez redéclarer une variable déclarée avec `var`, mais pas avec `let` ou `const`.

- **Réassignation** :
  Vous pouvez réassigner une nouvelle valeur à une variable déclarée avec `var` ou `let`, mais pas à une variable déclarée avec `const`.

---

**A savoir: portée globale :**

Si `let` et `const` sont déclarés en dehors d'une boucle, d'une fonction, ou d'une condition (c'est-à-dire au niveau le plus élevé du script ou d'un module), ils ont une **portée globale**. Cependant, il y a une nuance importante à comprendre par rapport à `var` lorsqu'on parle de portée globale.

Lorsque vous déclarez une variable avec `var` au niveau global, elle devient une propriété de l'objet global (`window` dans un navigateur, `global` en Node.js).

Par contre, une variable déclarée avec `let` ou `const` au niveau global ne devient pas une propriété de l'objet global. Elle reste dans le "global lexical scope" et n'est pas attachée à l'objet `window` (ou `global` dans Node.js).

**Exemple :**

Dans un navigateur :

```javascript
var maVariableVar = "Je suis var";
let maVariableLet = "Je suis let";
const maVariableConst = "Je suis const";

console.log(window.maVariableVar);  // Affiche "Je suis var"
console.log(window.maVariableLet);  // Affiche undefined
console.log(window.maVariableConst); // Affiche undefined
```

En conclusion, même si `let` et `const` peuvent avoir une portée globale lorsqu'ils sont déclarés en dehors de tout bloc, ils ne polluent pas l'objet global comme le fait `var`.

---

**Pourquoi `const` est généralement mieux ?**

1. **Immutabilité** : L'utilisation de `const` indique clairement qu'une variable ne sera pas réassignée, ce qui aide à prévenir les erreurs accidentelles.
2. **Lisibilité** : Lorsqu'on voit `const`, on sait immédiatement que la variable ne changera pas, ce qui facilite la compréhension du code.
3. **Portée de bloc** : Comme `let`, `const` a une portée de bloc, ce qui évite les erreurs courantes associées à la portée de fonction de `var`.

Cependant, il est important de noter que `const` ne rend pas l'objet auquel il fait référence immuable, seulement la référence elle-même. Par exemple, si vous avez un objet déclaré avec `const`, vous pouvez toujours modifier ses propriétés.