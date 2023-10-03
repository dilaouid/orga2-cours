# 03 - Bases de Git

## Introduction aux concepts de base de Git
Pour bien maîtriser Git, il est essentiel de comprendre les concepts de base qui sous-tendent son fonctionnement. Ces concepts vous permettront de gérer efficacement les versions de votre code, de collaborer en équipe et de suivre les changements de manière transparente.

### Clonage d'un dépôt (repository)
Lorsque vous démarrez un projet, vous devez d'abord obtenir une copie du dépôt distant. Pour ce faire, vous utilisez la commande git clone. Cela télécharge tout le contenu du dépôt distant sur votre ordinateur local. Par exemple :

```shell
git clone <URL du dépôt>
```

### Création d'un nouveau dépôt local
Parfois, plutôt que de cloner un dépôt, vous pouvez l'initialiser directement depuis votre machine avec la commande suivante:

```shell
git init
```

### Vérification de l'état du dépôt
Après avoir apporté des modifications à vos fichiers, vous pouvez vérifier l'état de votre dépôt.. Cela vous montrera les fichiers modifiés, ajoutés ou supprimés et vous aidera à suivre les changements :

```shell
git status
```

### Visualiser l'historique des commits
Il est possible de voir les commits effectués par les collaborateurs d'un projet, les messages associés ainsi que les informations temporaires avec la commande suivante:

```shell
git log
```

### Ajout de modifications
Après avoir apporté des modifications à vos fichiers, vous devez les préparer pour un commit en les ajoutant à l'index (zone de préparation). Cela se fait avec la commande `git add`. Par exemple, pour ajouter tous les fichiers modifiés :

```shell
git add .
```

Cependant, si vous ne souhaitez modifier qu'un seul fichier, disons, `app.js`, la commande à saisir est la suivante:

```shell
git add app.js
```

Vous pouvez également utiliser `git add` pour plusieurs fichiers, comme ceci:

```shell
git add app.js index.html styles.css dist/index.js
```

### Annuler une modification
Si vous avez, par erreur, utilisé `git add` sur un fichier et que vous souhaitez annuler les modifications sur ce fichier, vous pouvez executer la commande suivante:

```shell
git checkout nom-du-fichier
```

### Supprimer un fichier du suivi
Il peut parfois être nécessaire de supprimer un fichier de votre dépôt. Dans ce cas utilisez la commande suivante:
```shell
git rm nom-du-fichier
```

### Validation des modifications
Une fois vos modifications ajoutées à l'index, vous pouvez les enregistrer dans l'historique du dépôt en effectuant un commit. Chaque commit est accompagné d'un message expliquant les changements effectués. Utilisez la commande git commit pour cela :
```shell
git commit -m "Message de commit explicatif"
```
Il va de soi que **votre message doit être le plus explicite possible**. Si vous mettez un message de commit incompréhensible comme `aaaaaa`, vos collaborateurs seront confus sur la nature de ce commit, et vous même lorsque vous recherchez un commit spécifique dans l'historique de git.

### Déplacement des modifications non validées
Lorsque vous travaillez sur un projet, il peut arriver que vous ayez des modifications en cours dans vos fichiers, mais que vous ayez besoin de basculer vers une autre tâche ou une autre branche.
Du coup, pour éviter de perdre des modifications sans les perdre, vous pouvez utiliser la commande suivante:
```shell
git stash
```
Cela va déplacer temporairement vos modifications non validées dans une zone de stockage appelée _stash_.

Pour voir la liste des stashes, vous pouvez saisir la commande suivante:
```shell
git stash list
```

Désormais, vous êtes prêt à revenir à vos modifications enregistrées dans le _stash_, vous pouvez utiliser la commande `git stash apply` suivie du nom du _stash_ (qui est généralement *stash@{0}* pour le dernier stash créé) :
```shell
git stash apply stash@{0}
```

Cela appliquera les modifications enregistrées dans le _stash_ à votre répertoire de travail actuel. Si vous souhaitez supprimer le _stash_ après l'avoir appliqué, vous pouvez utiliser la commande suivante:

```shell
git stash pop
```

Si vous souhaitez supprimer seulement un _stash_ spécifique, vous pouvez utiliser la commande  `git stash drop` suivi du nom du stash :
```shell
git stash drop stash@{0}
```

Pour supprimer tout les stashes, vous pouvez utiliser :

```shell
git stash clear
```


### Publication des modifications
Après avoir effectué des commits locaux, vous pouvez les publier sur le dépôt distant en utilisant git push. Cela met à jour le dépôt distant avec vos derniers changements. Par exemple :
```shell
git push origin <nom de la branche>
```

La branche par défaut s'appelle `main` (autrefois `master`). Si vous êtes sur la branche `main` et que vous êtes un collaborateur du dépôt, et que vous souhaitez push sur la branche local (qui est `main`), vous pouvez simplement saisir la commande:
```shell
git push
```

### Créer une branche
Une des principales forces de git, ce sont ses branches. Pour en créer une, utilisez la commande suivante:
```shell
git branch nom-de-la-branche
```

### Changer de branche
Pour changer de branche, pensez à d'abord valider les modifications sur le branche courante, et ensuite, utilisez la commande suivante:
```shell
git checkout nom-de-la-branche
```

### Supprimer une branche
Pour supprimer une branche (soyez sûr de votre action, bien entendu), utilisez la commande suivante:
```shell
git branch -d  nom-de-la-branche
```

### Récupération des modifications
Si d'autres développeurs ont effectué des modifications sur le dépôt distant, vous pouvez récupérer ces changements en utilisant git pull. Cela fusionne les modifications distantes avec votre copie locale. Par exemple:
```shell
git pull origin <nom de la branche>
```
Notez que pour `pull` des modifications sur la branche courante, cette commande suffit:
```shell
git pull
```

### Ignorer des fichiers
Le fichier `.gitignore` est un simple fichier texte placé à la racine de votre projet Git. Il contient une liste de motifs qui correspondent aux noms de fichiers et de répertoires que vous souhaitez ignorer.
Ces motifs peuvent inclure des noms de fichiers, des extensions, des répertoires, ou même des expressions régulières.

_Github_ vous fournit des templates de `.gitignore` à la création d'un dépôt git par exemple.

Par exemple, si vous ne souhaitez pas inclure le répertoire `node_modules` et le répertoire `build` dans votre système de contrôle de version, vous pouvez ajouter les lignes suivantes à votre fichier `.gitignore` :

```shell
node_modules/
build/
```

Il existe des règles de correspondance dans ce fichier pour vous faciliter la tâche. Par exemple:
- `node_modules/` : Ignore le répertoire `node_modules` et son contenu.
- `*.log` : Ignore tous les fichiers ayant l'extension `.log`.
- `/build/` : Ignore le répertoire build à la racine du projet.
- `secret*.txt` : Ignore tous les fichiers commençant par "secret" et ayant l'extension .txt.

Vous pouvez même inclure des expressions régulières dans ces règles de correspondances.

Ce fichier est extrêmement important. Cela peut accélérer les opérations Git et éviter que des informations confidentielles ne soient accidentellement exposées (par exemple fichier `.env` où sont stockées tout vos identifiants).

Cependant, assurez-vous de ne pas ignorer des fichiers importants nécessaires au fonctionnement de votre application. Par exemple, si vous ignorez des fichiers de configuration nécessaires pour que votre projet fonctionne correctement, cela pourrait poser des problèmes lors de la collaboration.

Si vous avez déjà suivi des fichiers dans Git avant d'ajouter une règle à `.gitignore`, ces fichiers continueront d'être suivis même après l'ajout de la règle. Pour arrêter de suivre ces fichiers, vous devrez utiliser la commande `git rm --cached` suivie des noms de fichiers que vous souhaitez arrêter de suivre.

Par exemple :
```shell
git rm --cached .env
```
Cette commande supprimera le suivi du fichier `.env` dans Git, mais conservera une copie locale du fichier sur votre système.

Vous n'avez plus qu'à confirmer les changements en effectuant un commit:
```shell
git commit -m "stop tracking env file"
```
