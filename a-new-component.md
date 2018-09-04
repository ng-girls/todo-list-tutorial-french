# Un nouveau composant

Dans ce chapitre, nous allons écrire notre premier composant Angular. Le rôle de ce composant sera de nous permettre d'ajouter des entrées dans notre liste des choses à faire. Ce composant contiendra les éléments HTML `input` et `button`. Nous l'appellerons Input-Button-Unit.

Nous utiliserons le CLI d'Angular pour générer automatiquement le squelette des fichiers nécessaires. Si votre terminal est déjà ouvert et que la commande `ng serve` est déjà lancée, il vous suffit d'ouvrir une nouvelle fenêtre du terminal pour lancer la commande qui va générer le composant. Les changements apportés par le CLI seront reflétés immédiatement dans le navigateur.

Ouvrez un nouvel onglet dans votre terminal puis exécutez :

```text
ng g c input-button-unit
```

Comme mentionné précédement, `ng` est la commande utilisée par le CLI d'Angular :
* `g` est une option et est le raccourci de `generate`.
* `c` est une autre option et est le raccourci de `component`.
* `input-button-unit` est le nom de notre future composant.

Cette commande est la version raccourci de (ne l'exécutez pas !):

```text
ng generate component input-button-unit
```

Regardons maintenant ce que le CLI d'Angular a généré.

Le CLI a créé un nouveau répertoire nommé `src/app/input-button-unit`. Il y a trois fichiers \(ou quatres si vous n'utilisez pas les templates intégrées "inline-template"\):

* `input-button-unit.component.css` - ceci est le fichier contenant les styles CSS dédiés au composant.
* `input-button-unit.component.spec.ts` - ce fichier contient le squelette des tests unitaires du composnat généré. Nous n'allons couvrir les tests unitaires dans ce tutoriel.
* `input-button-unit.component.ts` - ce fichier contient la logique du composant.
* `input-button-unit.component.html` - ceci est le template HTML (la vue) du composant, si vous n'utilisez pas les templates intégrées "inline-template".

Ouvrez le fichier `input-button-unit.component.ts`. Vous pouvez constater que le CLI d'Angular a généré la configuration du composant, y compris son sélecteur, qui correspond au nom que nous avons donné à notre composant, préfixé par `app`; le CLI a également généré un template par défaut :

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
@Component({
  selector: 'app-input-button-unit',
  template: `
    <p>
      input-button-unit works!
    </p>
  `,
  styleUrls: ['./input-button-unit.component.css']
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

> Le préfixe `app` sera ajouté à tous les sélecteurs de tous les composants que vous allez générer. Cela est dans le but d'éviter des conflits de nommage avec d'autres composants ou éléments HTML. Par exemple, si vous générez un composant nommé "input", cela ne rentrera pas en conflit avec l'élément HTML standard `<input />`, car le composant sera appelé `app-input`.

>
> `app` est est le préfixe par défaut, ce qui est suffisant pour une simple application Angular. Cependant, si vous développez une librairie de composants Angular destinés à être utilisés au sein d'autres projets, nous vous recommandons d'utiliser un autre préfixe. Par exemple, la librairie [Angular Material](https://material.angular.io/) utilise le préfix `mat`. Vous pouvez soit définir un préfixe dès la création d'un projet Angular (avec le CLI) en utilisant l'option `--prefix`, ou bien vous pouvez changer le préfixe dans le fichier de configuration du CLI `angular-cli.json`.

Utilisons le composant tel quel et regardons le résultat.


Ouvrez le composant racine, `app.component.ts` et ajoutez dans son template l'élément `app-input-button-unit` \(rappelez-vous que nous avions modifié le composant racine en y intégrant directement le template, aussi appelé "inline template"\) :


{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```markup
template: `
  <h1>
    Welcome to {{ title }}!
  </h1>

  <app-input-button-unit></app-input-button-unit>
`,
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Vérifiez les nouvelles modifications dans le navigateur !

Ajoutons maintenant un peu de contenu dans notre nouveau composant. D'abord, ajoutez une propriété `title` qui va représenter le titre de l'élément de notre liste :


{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
export class InputButtonUnitComponent implements OnInit {
  title = 'Hello World';
```
{% endcode-tabs-item %}
{% endcode-tabs %}


Cette nouvelle propriété `title` n'interfèrera pas avec celle du composant `app-root` puisque le contenu de chaque composant est encapsulé (renfermé) au sein de ce dernier.

Ensuite, ajoutez une evalution de `title` dans le template. Ce processus est appelé "interpolation" dans le jargon Angular : 

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
template: `
  <p>
    input-button-unit works!
    The title is: {{ title }}
  </p>
`,
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Vérifiez le résultat !


Ce composant ne fait rien de spécial pour le moment. Dans les chapitres suivants, nous allons introduire la notion de classe et coder la logique de notre composant.
