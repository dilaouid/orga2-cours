# 06 - Conflits

## Qu'est ce qu'un conflit
Lorsque plusieurs contributeurs modifient le même fichier ou des parties similaires du code, des conflits peuvent survenir lors de la fusion des branches. 


## Identifier les conflits
Les conflits apparaîtront sous forme de blocs de code entourés de balises spéciales `<<<<<<<`, `=======` et `>>>>>>>`.

Vous pouvez identifier la listes des fichiers en conflit en utilisant la commande `git status`.

Git vous avertira des conflits et vous devrez les résoudre manuellement en choisissant quelles modifications conserver. Utilisez un éditeur de code (comme _Visual Studio Code_) ou une interface Git (comme _GitKraken_) pour résoudre ces conflits.

## Résolution du conflit
Pour résoudre un conflit sur un éditeur de code par exemple, vous devrez manuellement choisir quelles lignes de code garder. Supprimez les balises spéciales `<<<<<<<`, `=======` et `>>>>>>>`, ainsi que les sections de code que vous ne souhaitez pas conserver.

Une fois que vous avez résolu les conflits, enregistrez les modifications dans les fichiers. Utilisez ensuite la commande `git add` pour marquer les fichiers comme résolus.

Après avoir résolu tous les conflits et marqué les fichiers comme résolus, vous pouvez finaliser la fusion en effectuant un commit avec 
```shell
git commit -m "nom du commit
```

Git considérera alors les conflits comme résolus et le code des deux branches sera intégré.

Après que les commentaires ont été adressés et que le code a été examiné dans la _PR_, la branche peut être fusionnée dans la `main`. Cela se fait généralement en approuvant la _PR_ et en effectuant une fusion (`merge`).