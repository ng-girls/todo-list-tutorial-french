# Installations

Bien qu'il est tout à fait possible de développer des applications Web avec uniquement un simple éditeur de text, dans notre quotidien nous utilisons un ensemble d'outils permettant de simplifier certaines tâches de notre travail pour le rendre beaucoup plus agréable. Nous allons avoir besoin d'un navigateur pour visualiser nos modifications, de NodeJs pour exécuter les scripts sur notre machine de développement, et de NPM pour récupérer et installer les librairies JavaScript depuis le Web. Grâce à NPM, nous allons installer Angular CLl qui va, à son tour, utiliser NodeJs pour exécuter un script capable de créer un squelette de projet Angular pour nous. Angular CLI utilisera NPM également pour installer toutes les dépendances \(les librairies JavaScript\) nécessaires pour notre projet \(comme Angular\). Nous allons également avoir besoin d'un IDE \(éditeur de code\) pour écrire notre code et gérer notre projet.

De plus, il est fortement recommandé d'utiliser Git gérer le versionning de votre projet, et GitHub pour partager les sources de votre projet avec la communauté \(si vous le souhaitez\).

## Navigateur

Notre premier outil est le **navigateur**. Nous allons l'utiliser pour voir et interagir avec notre application pendant la phase de développement ; et surtout, nous allons pouvoir la déboguer. Nous recommandons [Google Chrome,](https://www.google.com/chrome/browser/desktop/) qui possède tout un ensemble d'outils pour développeurs intégrés. Vous pouvez aussi utiliser [Firefox](https://www.mozilla.org/en-US/firefox/new/). Si vous n'avez aucun des deux navigateurs installé, cliquez simplement sur les liens et suivez les instructions pour installer l'un des deux sur votre machine.

## IDE

Notre prochain outil est l'**IDE**, aussi appelé : Environnement de Développement Intégré \(EDI\). C'est un programme qui vous permettra d'écrire le code de votre application. Les IDEs sont capables d'effectuer plusieurs tâches, telles que :

* colorer votre code source pour le rendre plus lisible
* proposer de l'auto-complétion
* vous aider à naviguer facilement dans les sources, fichiers et répertoires de votre projet
* et beaucoup plus...

[Webstorm](https://www.jetbrains.com/webstorm/download/) de JetBrains est l'un des IDEs les plus répandus sur le marché. Vous avez le premier mois gratuit. Si vous êtes étudiant\(e\), JetBrains vous offre la licence.

[Visual Studio Code](https://code.visualstudio.com/) \(VS Code\) de Microsoft est également un très bon programme qui est de plus en plus utilisé. Il est gratuit pour les développeurs.

Choisissez votre IDE préféré puis suivez les instructions d'installation sur leurs sites web.

### **Plugins**

Les Plugins permettent entre autre à l'IDE de mieux comprendre et manipuler le code source que nous écrivons. Webstorm est livré avec les plugins nécessaires pour les projets Angular. Si vous choisissez VS Code, nous vous recommandons d'installer les plugins suivants :

* [Angular.ng-template](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)
* [natewallace.angular2-inline](https://marketplace.visualstudio.com/items?itemName=natewallace.angular2-inline)

![VS Code Plugins for Angular](https://github.com/ng-girls/todo-list-tutorial/raw/master/assets/VS-Code-Plugins.png)

## NodeJs et NPM

**Merci de lire la** [**documentation officielle du Angular CLI**](https://github.com/angular/angular-cli#prerequisites) **pour les informations à jour concernant les versions de NodeJs et NPM à installer.**

En tant que développeurs Web, vous allez avoir besoin d'installer **NodeJs**. Une fois installé, vous aurez aussi accès à **NPM**, le gestionnaire des dépendances de NodeJs.

NodeJs vous permet d'exécuter JavaScript sur votre machine, en dehors de votre navigateur. Dans notre cas, NodeJs démarre un serveur Web local, de développement, permettant ainsi d'envoyer les fichiers de notre projet au navigateur \(faisant office de client Web\) ; ceci donnera l'impression que notre application tourne sur un vrai serveur Web de production. 

Quant à NPM, il nous permet de télécharger puis installer les dépendances de notre projet, directement depuis Internet.

**Téléchargez NodeJs** [**depuis ce lien**](https://nodejs.org/en/)**.**

Si vous avez déjà NodeJs installé, veuillez vous assurer que la version installée correspond bien à celle requise par Angular CLI. Pour vérifier la version de NodeJs installée, lancez la commande suivante dans votre terminal / ligne de commande :

```text
node -v
```

\('-v' est l'alias de 'version'.\)

Si la version installée est inférieure à celle requise, vous devez installer la bonne version. Si vous avez d'autres projets qui dépendent d'une version de NodeJs différente de celle demandée pour ce projet, nous vous recommandons d'utiliser NVM \(Node Version Manager\) qui vous permettra d'installer puis utiliser différentes versions de NodeJs sur une même machine. Veuillez lire cette [question sur Stack Overflow](https://stackoverflow.com/questions/8191459/how-do-i-update-node-js) pour savoir la procédure à suivre.

Une fois la bonne version de NodeJs installée, vous devriez également avoir NPM installée. Vérifiez la version de NPM en exécutant :

```
npm -v
```

## Git

[Git](https://git-scm.com/book/fr/v1/D%C3%A9marrage-rapide-%C3%80-propos-de-la-gestion-de-version) est un système de gestion des versions de votre code source. Il vous permet de tracer toutes les modifications effectuées à votre code source, et pouvoir éventuellement revenir à une version antérieure en cas de problème. Git est un outil assez puissant, nous n'allons profitez de toutes les fonctionnalités, mais simplement certaines commandes basiques.

Vous pouvez télécharger Git en suivant la procédure sur le site officiel.

**Attention : Lorsqu'on vous demandera si vous voulez installer git bash, répondez "yes".**

## GitHub

[GitHub](https://github.com/) est une plateforme collaborative autour des projets, principalement open sources. La majorité des code sources des différents outils, librairies et frameworks que nous utilisons dans notre quotidien de développeurs \(NodeJs, VS Code, Angular...etc\) sont hébergés et accessibles librement sur GitHub. Tous les projets distribués sur GitHub ont un point commun : Ils utilisent tous Git.

Afin que vous puissiez publier également votre projet sur GitHub, il vous suffit de créer simplement un compte \(c'est gratuit, bien évidement\).

## Angular CLI

[Angular CLI](https://github.com/angular/angular-cli) est un outil assez puissant qui simplifie énormément le processus de développement des projets Angular. De la création de squelettes de projet Angular pré-configurés, jusqu'au packaging et déploiement, en passant par l'exécution des tests et la génération de code. Pour l'installer, nous allons utiliser NPM, en exécutant la commande suivante :

```
npm i -g @angular/cli
```

Cette commande utilise NPM pour télécharger et installer la dépendance Angular CLI, dont le nom du  projet est _@angular/cli_. Dans le monde NPM, ces dépendance s'appellent également des **packages** NPM. Le paramètre `i` est un alias de la commande `install` demandant à NPM d'installer un package. Le paramètre `-g` est un alias de l'option `global`, indiquant à NPM que nous souhaitons installer le package globalement sur notre machine afin que l'on puisse l'utiliser, en tant que ligne de commande, depuis n'importe quel endroit de notre système.

Veuillez lire plus de détails concernant Angular CLI dans la section suivante.

### Création d'un project Angular

Tout d'abord, créez un répertoire pour y stocker tous vos projets, par exemple _myProjects,_ puis accédez à ce répertoire en utilisant le terminal :

```
cd chemin-vers-votre-répertoire-de-travail/myProjects
```

Ensuite, en utilisant le CLI d'Angular, générez un nouveau projet Angular dans votre répertoire _myProjects_, nommez-le _todo-list_. Pour cela, exécutez la commande suivante :

```
ng new todo-list
```

Cette création peut prendre du temps, car NPM doit télécharger et installer toutes les dépendances requise par le projet Angular qui est sur le point d'être créé par le CLI d'Angular.

Une fois la génération du projet terminée avec succès, positionnez-vous dans le nouveau répertoire créé, ce sera la racine de votre application Angular :

```text
cd todo-list
```

Une fois à la racine de votre nouveau projet, nous allons démarrer l'application générée par le CLI d'Angular en utilisant la commande suivante :

```text
ng serve -o
```

La commande `ng` représente le CLI d'Angular, installé globalement. L'option `-o` est un alias de `--open`, indiquant au CLI d'ouvrir automatiquement une fenêtre du navigateur \(par défaut\) sur l'URL de notre projet : [`localhost:4200`](http://localhost:4200)

_Note : Cette commande lance un serveur Web de développement en local afin de traiter et envoyer les sources de votre application au navigateur \(le client\)._ 

Vous devriez voir cette page s'afficher dans votre navigateur :

![Initial App](https://github.com/ng-girls/todo-list-tutorial/raw/master/assets/initial-app.png)

**N'oubliez surtout pas de laisser votre terminal ouvert tant que vous travaillez sur votre application, autrement cela arrêtera le serveur et votre application ne sera plus accessible en local !** Vous pouvez ouvrir un autre terminal si vous souhaitez exécuter d'autres commandes.

Pendant toute la phase de développement, toutes les modifications apportées au code source de votre application entraînera systématiquement un rafraîchissement automatique de votre application dans le navigateur ; ce qui vous permettra de voir directement les dernières modifications.

Pour arrêter l'application, appuyez sur `Ctrl+C` dans le terminal où vous avez lancé la commande précedente, ou fermez-le simplement.

## Félicitations!

Vous venez de lancer votre première application Angular ! Maintenant nous sommes prêts pour commencer le développement.

