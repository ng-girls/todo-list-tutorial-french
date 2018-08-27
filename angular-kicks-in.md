# Démarrage

Avant de commencer le développement de notre application, parlons d'abord du projet et de l'intérêt d'Angular. Tous les fichiers que nous allons manipuler à ce stade, se trouvent dans le répertoire `src`.  
Voir plus de détails sur les fichiers générés par le CLI d'Angular dans l'[Appendix 1: Générer un nouveau projet.](https://ng-girls.gitbook.io/todo-list-tutorial/generating_a_new_project.html)

Si vous avez hâte de commencer la partie technique, vous pouvez passer ce chapitre et y revenir ultérieurement pour mieux comprendre la structure du projet.

Ouvrir le fichier `index.html`. Le contenu qui est affiché dans la fenêtre de votre navigateur est celui de la balise HTML `<body>` .Tout ce que vous pouvez y apercevoir pour le moment est un autre élément ne faisant pas partie du standard HTML : `<app-root></app-root>`. Cet élément est en fait un composant Angular, définit dans le fichier `app/app.component.ts` grâce à la classe **AppComponent**. \(Nous y reviendrons dans le prochain chapitre\).

> Angular peut être utilisé de plusieures manières. Par exemple, grâce à du code JavaScript qui s'exécutera lorsque l'application est interprété par le navigateur. Tout le code que vous allez écrire — composants, modules, services, etc... sera reconnu puis traité par Angular. Par exemple, les composants que vous allez coder et utiliser seront compilés en des fonctions JavaScript. Ces fonctions vont pouvoir insérer le contenu du composant Angular dans le DOM \(Document Object Model\) — qui est la représentation de la structure de votre page dans la mémoire de l'ordinateur et que le navigateur utilise pour afficher \(rendre\) votre application. Voilà comment vous allez visualiser les composants que vous allez créer.

Donc comme dit précédemment,  `<app-root>` n'est pas un élément HTML mais plutôt un composant Angular. Lorsque l'application est prête, le contenu du composant sera inséré à l'intérieur de la balise `<app-root>`, et vous le verrez ainsi dans votre navigateur :

![Application initiale](https://github.com/ng-girls/todo-list-tutorial/raw/master/assets/initial-app.png)

Passons maintenant à l'étape suivante et découvrons une des notions élémentaires d'Angular : les modules.

## NgModule

Angular a besoin que nous lui disions quels sont les éléments qu'il doit traiter et compiler. Pour cela, nous utilisons les Modules, au appelés **NgModules**, qui sont en quelque sorte un package dans lequel nous mettons les choses ayant la même utilité ! Ces packages peuvent inclure des composants, des services, des directives, des pipes ainsi que d'autres NgModules. Nous avons déjà un NgModule racine définit dans le fichier `app/app.module.ts`. Analysons ce fichier.

La dernière ligne de ce fichier est une class JavaScript :

```typescript
export class AppModule { }
```

`export` est un mot clé réservé en JavaScript. Cette instruction indique au moteur JavaScript que tout ce qui est déclaré après elle, doit être rendu public \(rendu accessible\) aux autres fichiers JavaScript. Pour utiliser ce qui est exporté dans un autre fichier, il suffit de l'importer avec l'instruction `import`. Vous pouvez d'ailleurs noter des instructions d'import de classes et fonctions \(déclarés dans d'autres fichiers\) tout en haut de ce fichier. Le fait d'importer ces classes et fonctions permettra de les utiliser au sein du fichier courant.

La class `AppModule` est vide.Ne vous inquiétez pas, cette classe sera correctement traitée et enrichie par Angular. En effet, Angular est capable d'identifier le rôle de cette classe grâce à cette instruction`@NgModule({`.

Chaque entité dans Angular \(NgModules, composants, services, directives et pipes\) est une simple **classe avec un décorateur**. C'est ce décorateur qui indique à Angular le rôle de la classe en question.

`@NgModule({...})` est un décorateur. Un décorateur est une simple fonction que l'on invoque avec le symbole `@` préfixant son nom. De cette manière, cette fonction devient un décorateur : Il analyse ce qui vient après l'appel du décorateur et le reçoit en tant qu'argument. Les décorateurs on souvent tendance à manipuler ce qu'ils décorent. Dans notre exemple, `NgModule` recevra la classe `AppModule` puis l'enrichit avec ses méthodes et membres qui seront exploités ultérieurement par Angular. De cette manière, Angular saura que cette classe est en fait un NgModule.

Les informations passées au fonction décorateur sont utilisées par Angular pour décorer \(enrichir\) la classe en question. Vous pouvez constater que nous passons un objet JavaScript avec des propriétés particulières, chaque propriété représente une liste de classes. Nous expliquerons le rôle de chaque propriété.

**declarations** : une liste de composants, directives ou pipe Angular requis par ce module. Dans notre exemple, nous passons juste un composant : `AppComponent`, parce que c'est tout ce que nous avons pour le moment. C'est la seule dépendance de notre NgModule.

**imports** : une liste d'autres NgModules requis par ce module. Par exemple, dans le composant `AppComponent` nous pourrions dépendre de certaines directives voire composants fournis par le module officiel `FormsModule` . Dans ce cas, nous devons lister `FormsModule` dans la liste des imports du module racine `AppModule`.

**bootstrap** : cette propriété n'est utilisée que dans le cas du NgModule racine. Vous ne la trouverez dans aucun autre module. Cette propriété indique à Angular quel composant est le composant racine \(parent\) de l'application. En effet, une application Angular peut être décrite comme **un arbre de composants**; avec donc un composant racine qui est responsable d'accueillir toute la structure de l'application. Dans notre exemple, le composant racine est `AppComponent` \(avec le sélecteur `todo-root`\). Rappelez-vous, il est déclaré dans le fichier `index.html` en tant que seule élément de `<body>`.

Comment Angular sait-il que `AppModule` est le NgModule racine ? Cette information est définie dans le fichier`main.ts` :

{% code-tabs %}
{% code-tabs-item title="src/main.ts" %}
```typescript
platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.log(err));
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We bootstrap our root NgModule to a renderer. This way we tell Angular what NgModule to use as the starting point of our application. And we also choose a renderer: `platformBrowserDynamic`. It knows how to take our code and add the relevant data \(elements, attributes, etc.\) to the browser's DOM.

If there's an error, it is caught and logged in the browser's console \(seen only when the browser's dev-tools are open\).

We can use a different renderer at this point, for example one that renders to Android or iOS native elements! We just need a renderer that knows how to take our templates \(which use HTML notations\) and JavaScript code, and create native mobile application elements. An example to such a renderer is [NativeScript](https://www.nativescript.org/) by Telerik.

There are even renderers to Arduino, with which you can connect sensors, buttons, LEDs and other hardware to your application! You can see a great example for this here: [Building Simon with Angular2-IoT](https://medium.com/@urish/building-simon-with-angular2-iot-fceb78bb18e5#.430qu216w).

We've seen how we tell Angular where and how to start its work, how we define the root module and the root component, and how we use the root component.

In the next chapter we'll see how a component is defined in Angular.

