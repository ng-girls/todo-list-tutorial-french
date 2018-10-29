# Nouveau composant: todo-item

Nous allons créer un nouveau composant qui sera utilisé pour chaque élément de la todo liste. Ce sera un composant simple pour commencer, que nous allons étoffer par la suite. L'important c'est qu'**il prendra l'élément comme input depuis son composant parent**. Ainsi ce composant sera réutilisable et ne reposera pas directement sur les données et l'état de l'application.

Créer un nouveau composant nommé `todo-item`:

```text
ng g c todo-item
```
Comme vous pouvez le voir, un nouveau dossier se créer - `src/app/todo-item`, contenant les fichiers du composant.

Utilisez le nouveau composant dans le template du composant `app-root` - dans l'élément `<li>`:

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```markup
<ul>
  <li *ngFor="let item of todoList">
    <app-todo-item></app-todo-item>
  </li>
</ul>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Regardez le résultat dans le navigateur. Que voyez-vous? Pourquoi?

## @Input\(\)

Nous souhaitons afficher le titre de chaque élément de la liste dans le composant `todo-item`. Nous avons besoin de passer l'élément courant dans la boucle au composant `todo-item`.

Encore une fois, Angular nous facilite la tâche en nous fournissant le décorateur `Input`.

Dans la classe `TodoItemComponent` nouvellement générée dans `todo-item.component.ts`, ajoutez la ligne:

{% code-tabs %}
{% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```typescript
@Input() item;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Ce code dit au composant de s'attendre à un input et de l'assigner à l'attribut `item` de la classe. Assurez-vous que `Input` soit ajouté à l'`import` dans la première ligne du fichier. Nous pouvons maintenant l'utiliser dans le template de `todo-item` et extraire le titre de l'élément en utilisant: `{{ item.title }}`

Le composant devrait maintenant ressembler à ça:

{% code-tabs %}
{% code-tabs-item title="src/app/todo-item/todo-item.component.ts" %}
```typescript
import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'app-todo-item',
  template: `
    {{ item.title }}
  `,
  styleUrls: ['./todo-item.component.css']
})
export class TodoItemComponent implements OnInit {
  @Input() item;

  constructor() { }

  ngOnInit() {
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Nous devons maintenant passer un élément où nous utilisons le composant. Retournez dans le composant `app-root` et passez le titre de l'élément à `todo-item`:

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```markup
<ul>
  <li *ngFor="let todoItem of todoList">
    <app-todo-item [item]="todoItem"></app-todo-item>
  </li>
</ul>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

L'`item` ici entre crochet est le même que celui déclaré avec `@Input` dans le composant.

Nous avons utilisé les propriétés de binding sur un élément que nous avons crée nous-même! Nous pouvons maintenant voir et comprendre que cette propriété binding est liée à une propriété du composant. Nous allons bientôt voir comment cette liste peut être dynamique.