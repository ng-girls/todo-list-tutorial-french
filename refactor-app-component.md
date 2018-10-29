# Refactor App Component

Nous allons faire un petit refactoring. Le `app-root` ne devrait pas avoir un aussi gros template ni toute cette logique métier. Il devrait juste appeler un autre composant qui devrait s'en occuper.

* Création d'un nouveau composant appelé `list-manager`:

```bash
ng g c list-manager
```

* Déplacer tout le code de `app-root` dans `list-manager`
* Vous pouvez garder la variable `title` dans `app-root` et lui attribuer une valeur
* Faites attention de ne pas changer le nom de la classe du composant list manager!

% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```typescript
@Component({
  selector: 'app-root',
  template: `
    <h1>
      Welcome to {{ title }}!
    </h1>
  `,
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  title = 'My To Do List APP';
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="src/app/list-manager/list-manager.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';
import { TodoItem } from '../interfaces/todo-item';

@Component({
  selector: 'app-list-manager',
  template: `
    <app-input-button-unit (submit)="addItem($event)"></app-input-button-unit>

    <ul>
      <li *ngFor="let todoItem of todoList">
        <app-todo-item [item]="todoItem"></app-todo-item>
      </li>
    </ul>
  `,
  styleUrls: ['./list-manager.component.css']
})
export class ListManagerComponent implements OnInit {
  todoList: TodoItem[] = [
    {title: 'install NodeJS'},
    {title: 'install Angular CLI'},
    {title: 'create new app'},
    {title: 'serve app'},
    {title: 'develop app'},
    {title: 'deploy app'},
  ];

  constructor() { }

  ngOnInit() {
  }

  addItem(title: string) {    
    this.todoList.push({ title });
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Appelez le nouveau composant depuis le template `app-root`:

{% code-tabs %}
{% code-tabs-item title="src/app/app.component.ts" %}
```markup
  template: `
    <h1>
      Welcome to {{ title }}!
    </h1>

    <app-list-manager></app-list-manager>
  `,
```
{% endcode-tabs-item %}
{% endcode-tabs %}

C'est tout! Maintenant nous pouvons passer à la suite.