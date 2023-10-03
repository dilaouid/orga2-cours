# 05 - Collaboration

## Introduction au travail collaboratif sur Git
Comme vu précedemment, l'une des principales forces de Git réside dans sa capacité à faciliter le travail collaboratif entre développeurs. En utilisant des branches, des _PR_ et d'autres fonctionnalités, Git permet à plusieurs contributeurs de travailler simultanément sur un projet sans entrer en conflit. Comprendre comment travailler ensemble de manière efficace est essentiel pour une collaboration réussie, et donc un projet solide.

## Les branches
Les branches sont des copies isolées du code qui permettent aux développeurs de travailler sur des fonctionnalités, des correctifs ou des tâches spécifiques sans perturber le code principal. 

Imaginez la branche comme un univers alternatif de votre code principal où vous pouvez y faire ce que vous voulez, avant de fusionner cet univers avec le code principal.

Pour créer une nouvelle branche et basculer dessus, utilisez la commande suivante:
```shell
git checkout -b <nom-de-la-branche>
```

Ou alors:

```shell
git branch <nom-de-la-branche>
```

Si vous voulez basculer dans une branche existante, la commande suivante suffit:
```shell
git checkout <nom-de-la-branche>
```

## Pour fusionner les modifications

Une fois que vous avez terminé de travailler sur la branche, vous pouvez fusionner les changements dans la branche principale `main` (autrefois appelée `master`) avec une _PR_ (Pull Request).

Ou alors, depuis la branche `main`, si vous êtes un administrateur du projet, utiliser la commande
```shell
git merge <nom-de-la-branche>
```

`git merge` est une commande qui fusionne les modifications de une ou plusieurs branches dans la branche actuellement active. Elle combine les commits des branches différentes en un seul historique de commit. En cas de conflit de modifications sur les mêmes fichiers, `git merge` demandera une résolution manuelle des conflits.

### Théoriquement:

- Avec `git merge`, les commits de différentes branches sont combinés dans un nouvel "commit de fusion", qui a deux parents.
- Les branches originales restent intactes, et leurs historiques de commits restent séparés dans le graphe de commit.

### En Pratique:

1. Vous avez une branche principale (`main`) et une branche de fonctionnalité (`feature`). Vous avez effectué des commits sur les deux branches.
2. Vous voulez intégrer les changements de la branche `feature` dans la branche `main`.
3. Vous basculez vers la branche `main` avec `git checkout main`.
4. Vous exécutez `git merge feature` pour fusionner les changements de `feature` dans `main`.
5. Si des conflits se produisent, Git vous demandera de les résoudre avant de terminer l'opération de fusion.

## Avantages de Git Merge:

- **Historique Complet**: `git merge` conserve l'historique complet, y compris les commits de fusion, ce qui donne un aperçu complet de la chronologie du projet.
- **Plus Simple pour les Débutants**: Les conflits sont généralement plus simples à résoudre avec `merge` qu'avec `rebase`.

## Inconvénients de Git Merge:
- **Historique Complexe**: `git merge` peut rendre l'historique des commits visuellement plus complexe, surtout si beaucoup de branches sont fusionnées fréquemment.

## Exemple:

Imaginons un arbre de projet où la branche `main` a deux commits (`A` et `B`), et une branche `feature` a un commit (`C`).

```
main:    A---B
            \
feature:     C
```

Vous voulez intégrer les changements de `feature` dans `main`. Si vous utilisez `git merge feature` sur la branche `main`, l'arbre de projet ressemblera à ceci:

```
main:    A---B---D
            \ /
feature:     C
```

Un nouveau commit de fusion (`D`) est créé sur `main`, qui a deux parents (`B` et `C`). L'historique des deux branches reste visible dans le graphe de commit.

Attention toutefois, il est important de discuter avec les autres collaborateurs des modifications que vous apportez à la branche principale.

Il y a aussi la commande `git rebase` qui est une commande Git qui intègre les changements d'une branche dans une autre. C'est une alternative à `git merge`. Bien que les deux opérations aient le même objectif (combiner les changements de différentes branches), elles le font de différentes manières, ce qui peut avoir des conséquences différentes pour l'historique du projet.

## Qu'est-ce que Git Rebase?

### Théoriquement:
- `git rebase` prend tous les commits de la branche actuelle qui ne sont pas dans la branche sur laquelle vous rebasisez, et les applique à la branche de destination.
- Cela peut être utile pour assurer un historique de projet linéaire, où les commits de différentes branches sont intégrés les uns dans les autres plutôt que placés côte à côte.

### En Pratique:
1. Supposons que vous ayez une branche principale (`main`) et une branche de fonctionnalité (`feature`). Vous avez effectué des commits sur les deux branches.
2. Vous voulez intégrer les changements de la branche `main` dans la branche `feature`, donc vous exécutez `git rebase main` alors que `feature` est la branche active.
3. Git prend tous les commits de la branche `feature` qui ne sont pas dans `main`, et les applique un par un sur `main`.
4. Si des conflits se produisent, Git vous demandera de les résoudre avant de continuer.

## Avantages de Git Rebase:

- **Historique Linéaire**: `git rebase` crée un historique de commit plus propre et plus linéaire.
- **Évite les commits de fusion**: Contrairement à `git merge`, `rebase` évite les commits de fusion en intégrant les commits directement dans la branche de base.

## Inconvénients de Git Rebase:

- **Complexe à gérer**: Les conflits sont généralement plus complexes à gérer avec `rebase` qu'avec `merge`.
- **Historique modifié**: `rebase` réécrit l'historique des commits, ce qui peut être problématique si d'autres personnes travaillent sur la même branche.

## Exemple:

Imaginons un arbre de projet où la branche `main` a deux commits (`A` et `B`), et une branche `feature` a un commit (`C`).

```
main:    A---B
            \
feature:     C
```

Vous voulez intégrer les changements de `main` dans `feature`. Si vous utilisez `git rebase main` sur la branche `feature`, l'arbre de projet ressemblera à ceci:

```
main:    A---B
              \
feature:       C
```

Le commit `C` est déplacé pour se baser sur le dernier commit de `main` (`B`). Maintenant, l'historique du projet est linéaire et propre.

Utilisez donc `git rebase` avec précaution. Il est particulièrement utile lors de la collaboration sur des projets d'équipe pour maintenir un historique de commits propre et linéaire. Assurez-vous de comprendre les implications avant de l'utiliser, et évitez de rebaser les commits qui ont déjà été poussés sur un dépôt distant partagé.

## Les Pull Requests (ou _PR_)
Une Pull Request (_PR_) est une demande d'intégration de vos modifications dans la branche principale (`main`) du projet. Elle permet aux autres membres de l'équipe d'examiner, commenter et discuter des changements avant de les fusionner. Les _Pull Requests_ sont couramment utilisées pour effectuer des révisions de code et garantir que les modifications sont de haute qualité et n'entre pas en dehors des directives du projet avant d'être fusionnées.

Cela encourage un processus transparent et collaboratif où les membres de l'équipe travaillent ensemble pour améliorer le projet.