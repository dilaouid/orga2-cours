# npm

## Introduction à npm (Node Package Manager)
Nous avons vu hier que l'opensource permettait également de partager des librairies (des morceaux de codes) ré-utilisables dans d'autres projets, et donc potentiellement les votres.

Comme bibliothèque de librairies Javascript, nous avons **npm**, abréviation de "Node Package Manager". **npm** est le gestionnaire de paquets pour l'écosystème _Node.js_. Il permet aux développeurs de JavaScript d'installer, partager et gérer des packages, des bibliothèques et des dépendances pour leurs projets. npm est livré avec l'installation de Node.js et offre un moyen efficace de gérer les modules externes et les outils nécessaires à vos applications.

Vous pouvez installer **npm** sur votre poste de travail en suivant des courtes étapes en fonction de votre système d'exploitation :
- **Windows**: https://treehouse.github.io/installation-guides/windows/node-windows.html
- **Ubuntu**:
```shell
sudo apt-get update
sudo apt-get install nodejs npm
```
- **MacOS**:
```shell
brew update
brew install node
```

Une fois les étapes réalisées, vous pouvez voir si tout est bien installé en saississant dans un terminal la commande suivante:
```shell
node -v
```

## La force de npm
**npm** facilite la gestion des dépendances de vos projets. Vous pouvez spécifier les bibliothèques et les modules dont votre application a besoin dans le fichier `package.json`.

Grâce à **npm**, vous pouvez facilement accéder à des milliers de packages opensource créés par la communauté, ce qui permet de réutiliser efficacement du code, et permet de mettre à jour rapidement vos packages et de gérer les versions pour maintenir votre application à jour.

**npm** peut également être intégré dans votre flux de travail de développement (workflow), permettant une installation et une gestion de packages transparentes.

## package.json

### Introduction au fichier package.json

Le fichier `package.json` est un élément central dans les projets utilisant **npm**. Il s'agit d'un fichier de configuration au format _JSON_ qui contient des métadonnées sur votre projet, ainsi que la liste des dépendances et des scripts utilisés. Comprendre et configurer correctement ce fichier est essentiel pour gérer les dépendances et automatiser les tâches dans vos projets JavaScript.

### Métadonnées du projet

Le fichier `package.json` contient des métadonnées sur votre projet ainsi que la liste de toutes les dépendances utilisées. Créez-le en utilisant la commande suivante:
```shell
npm init
```

A l'intérieur de ce fichier, vous retrouverez des métadonnées, notamment les suivante:

- **Nom du projet (name):** Le nom unique du projet.
- **Version:** La version actuelle du projet, généralement dans le format "0.1.2".
- **Description:** Une description brève du projet.
- **Auteur (author):** Le nom de l'auteur ou de l'équipe derrière le projet.
- **Licence (license):** La licence sous laquelle le projet est distribué.


### Dépendances

Une section importante du fichier `package.json` est la liste des dépendances. Ces dépendances sont les packages externes nécessaires au bon fonctionnement de votre projet. Il existe deux types de dépendances:
- Les **dépendances "normales"** nécessaires pour le fonctionnement de l'application en production. Par exemple, une dépendance JavaScript pour la gestion des dates, pour du parsing, sont des dépendances normales.
- Les **dépendances de développement** utilisées uniquement lors du développement. Elles comprennent généralement des outils tels que des frameworks de test, des linters, ou des outils de construction. Les dépendances de développement ne sont pas incluses dans la version finale de l'application en production.

Voici comment les dépendances sont spécifiées dans le fichier:
```json
"dependencies": {
  "librarie": "version"
},
"devDependencies": {
  "librarie-de-developpement": "version"
}
```
Le fichier `package.json` permet de spécifier les versions des dépendances utilisées. Vous pouvez utiliser des caractères spéciaux pour indiquer la plage de versions autorisée, comme `^` pour les mises à jour mineures compatibles.
Par exemple:
```json
"dependencies": {
  "librarie": "^1.1.0"
}
```

#### Installer une dépendance

Pour installer une dépendance dans le projet auquel le `package.json` est rattaché, lancez simplement la commande
```shell
npm install nom-de-la-librarie
```

Vous pouvez également faire plus court avec
```shell
npm i nom-de-la-librarie
```

Lorsque vous installez des dépendances à l'aide de `npm install`, les packages sont téléchargés et stockés dans le dossier `node_modules` à la racine de votre projet.

Ce dossier contient les bibliothèques et les modules externes nécessaires à votre application.


Notez que certaines dépendances peuvent être installées globalement pour être utilisées en dehors d'un projet spécifique. Utilisez la commande suivante pour ce cas d'usage:
```shell
npm i -g nom-de-la-librarie
```

#### Mettre à jour une dépendance

Dans le processus de développement, il est important de maintenir vos dépendances à jour pour bénéficier des dernières fonctionnalités, des corrections de bugs et des améliorations de sécurité. **npm** offre des moyens simples pour vérifier et mettre à jour vos dépendances.

Pour vérifier les mises à jour disponibles pour vos dépendances, vous pouvez utiliser la commande `npm outdated`. Cette commande affiche une liste des packages actuellement installés, leurs versions actuelles, ainsi que les versions les plus récentes disponibles.

```shell
npm outdated
```

Une fois que vous avez identifié les packages qui nécessitent une mise à jour, vous pouvez utiliser la commande `npm update` pour mettre à jour les dépendances.

```shell
npm update nom-de-la-librairie
```

Si vous souhaitez mettre à jour toutes les dépendances, exécutez simplement la commande sans spécifier de nom de package :

```shell
npm update
```

Notez que la mise à jour de certaines dépendances peut entraîner des changements de comportement dans votre application. Il est recommandé de vérifier la documentation des mises à jour et de tester soigneusement votre application après la mise à jour.

#### Désinstaller une dépendance
Au cours du développement, vous pourriez constater que certaines dépendances ne sont plus nécessaires ou qu'elles ont été remplacées par d'autres solutions. Dans de tels cas, il est important de désinstaller proprement les dépendances inutiles de votre projet.

Pour désinstaller une dépendance spécifique, utilisez la commande `npm uninstall` suivie du nom de la dépendance que vous souhaitez supprimer.

Par exemple:
```shell
npm uninstall nom-de-la-librairie
```

Disons que vous souhaitez supprimer la dépendance **lodash** de votre projet, vous saissirez donc la commande suivante:
```shell
npm uninstall lodash
```

Notez également qu'il est possible de désinstaller des dépendances de développement.
Lorsque vous désinstallez une dépendance, **npm** supprime également toutes les références et les fichiers associés à cette dépendance. Si vous souhaitez désinstaller une dépendance de développement spécifique, ajoutez simplement l'option `--save-dev` ou `-D` :

```shell
npm uninstall nom-de-la-librairie-de-developpement --save-dev
```

Par exemple, pour désinstaller un outil de test comme **jest** de vos dépendances de développement :

```shell
npm uninstall jest --save-dev
```

#### Nettoyer les dépendances
Après avoir désinstallé des dépendances, il peut y avoir des fichiers résiduels ou des dossiers non utilisés liés à ces dépendances. Vous pouvez nettoyer votre projet en utilisant la commande `npm prune`. Cette commande supprime toutes les dépendances non référencées dans votre `package.json`. Cela contribue à réduire la taille de votre application en éliminant les fichiers inutilisés.

```shell
npm prune
```

#### Verrouillage des Versions

Parfois, il peut être nécessaire de verrouiller explicitement les versions de vos dépendances pour garantir la stabilité et la reproductibilité de votre application. Pour cela, vous pouvez spécifier la version exacte d'une dépendance dans le fichier `package.json`.

```json
"dependencies": {
  "librarie": "1.2.3"
}
```

Cela empêchera npm d'installer automatiquement les nouvelles versions majeures ou mineures de la dépendance lors de futures mises à jour.

En gardant vos dépendances à jour tout en surveillant les changements de comportement, vous pouvez maintenir la qualité et la sécurité de votre application tout au long du développement. Cependant, soyez prudent lors de la mise à jour de dépendances critiques et effectuez toujours des tests approfondis pour vous assurer qu'elles n'ont pas d'effets indésirables sur votre projet.

### Scripts personnalisés
Le fichier package.json permet également de définir des scripts personnalisés qui peuvent être exécutés via la commande suivante:
```shell
npm run nom-du-script
```
Cela simplifie l'exécution de tâches courantes, comme le lancement du serveur de développement, la compilation de fichiers, les tests, etc.
Voici à quoi ressemble votre liste de scripts à l'intérieur de votre fichier `package.json`:
```json
"scripts": {
  "start": "node server.js",
  "build": "webpack --mode production",
  "random": "echo 'hello'"
}
```

