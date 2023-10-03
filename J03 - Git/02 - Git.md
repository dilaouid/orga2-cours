# 02 - Git, outil de versioning

## Qu'est ce qu'est Git ?
Git est un système de gestion de version distribué qui joue un rôle crucial dans la collaboration et le suivi des changements dans le développement informatique. Il a été créé par Linus Torvalds en 2005 pour gérer le développement du noyau Linux. Depuis lors, Git est devenu le système de gestion de version le plus populaire des développeurs du monde entier.

Chaque développeur peut travailler sur sa propre copie du projet, faire des modifications, puis les fusionner avec le projet principal. Git garde un historique de toutes les modifications, donc si quelque chose se passe mal, il est facile de revenir en arrière et de comprendre ce qui s'est passé.


## A quoi ça sert ?
L'introduction de Git a résolu plusieurs problématiques majeures auxquelles les développeurs étaient confrontés dans le passé. Voici quelques-unes de ces problématiques et comment Git les a abordées :
- **Suivi des changements apportés au code:** Avant Git, il était difficile de suivre et de gérer les modifications apportées au code. Git permet de conserver un historique complet des modifications, de la création d'un fichier à sa suppression, en passant par toutes les modifications intermédiaires.
- **Collaboration:** Travailler en équipe sur un même code source était compliqué, car il était difficile de fusionner les modifications apportées par différentes personnes. Git facilite la collaboration en permettant aux développeurs de travailler sur leurs propres "branches", puis de fusionner ces même "branches" de manière ordonné et organisé.
- **Récupération facilitée:** En cas de problème ou de perte de code, récupérer une version précédente était complexe, parfois même impossible. Git permet de revenir à n'importe quelle version antérieure du code de manière simple et rapide.
- **Isolation:** Les développeurs avaient du mal à isoler leurs modifications pour des fonctionnalités spécifiques. Git encourage la création de branches distinctes pour chaque fonctionnalité ou correction de bug, ce qui facilite l'isolation et la gestion des modifications. Ainsi, il est possible d'avoir plusieurs versions de son code, et ne pas casser la branche principale pendant que vous travaillez sur une fonctionnalité annexe.

## Repositories Git

Un projet Git est appelé un "référentiel" (ou "repo" en abrégé). Chaque repo contient tous les fichiers du projet ainsi que l'historique des modifications. Vous pouvez avoir un repo sur votre propre ordinateur, mais souvent les repos sont hébergés sur des plateformes en ligne comme GitHub, GitLab ou Bitbucket pour faciliter la collaboration.

## Les branches

Git utilise également la notion de "branches". Imaginez que vous travaillez sur une nouvelle fonctionnalité pour votre projet, mais vous ne voulez pas perturber le code principal tant que cette fonctionnalité n'est pas terminée et testée. Vous pouvez créer une nouvelle branche pour travailler sur cette fonctionnalité. Une fois que tout fonctionne correctement, vous pouvez "fusionner" cette branche avec la branche principale.

![Branch git](branch.png)

## Et Github là dedans ?
_Github_ est une plateforme en ligne qui héberge des dépôts Git et facilite la collaboration autour du développement logiciel. Il en existe d'autre, comme _Bitbucket_ ou même _Gitlab_.
Cependant, _Github_ propose des outils intéressant, comme un marketplace riche, une facilité de _CI/CD_ ainsi que de nombreux autres fonctionnalités que vous verrez dans la suite de votre formation.

## Ressources supplémentaires:
- [**Documentation de Git en Français**](https://www.w3.org/WAI/standards-guidelines/wcag)
- [**Utilisez Git par Fireship**](https://youtube.com/watch?v=HkdAHXoRtos/)
