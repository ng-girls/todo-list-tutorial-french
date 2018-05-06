# New component: todo-item

We will create a new component which will be used for each todo item that is displayed on the list. It will be a simple component at first, but it will grow later on. What's important is that **it will get the todo item as an input from its parent component**. This way it can be a reusable component, and not rely directly on the application's data and state.

Create a new component called `todo-item`:

```text
ng g c todo-item
```

You can see a new folder was created - `src/app/todo-item`, with the component files inside.

Use the new component in the template of `app-root` component - inside the `<li>` element:

{% code-tabs %}
{% code-tabs-item, title="src/app/app.component.ts" %}
```markup
<ul>
  <li *ngFor="let item of todoList">
    <app-todo-item></app-todo-item>
  </li>
</ul>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Check out the result in the browser. What do you see? Why?

## @Input\(\)

We want to display the title of each item within the `todo-item` component. We need to pass the title of the current item (or the whole item) in the loop to the `todo-item` component.

Again, Angular makes it really easy for us, by providing the `Input` decorator.

Inside the newly generated `TodoItemComponent` class in `todo-item.component.ts` add the line:

{% code-tabs %}
{% code-tabs-item, title="src/app/todo-item/todo-item.component.ts" %}
```typescript
@Input() itemTitle: string;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

It tells the component to expect an input of type string and to assign it to the class member called `itemTitle`. Make sure that `Input` is added to the import statement in the first line in the file. Now we can use it inside the `todo-item` template with interpolation: `{{ itemTitle }}`

The component should look like this now:

{% code-tabs %}
{% code-tabs-item, title="src/app/todo-item/todo-item.component.ts" %}
```typescript
import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'app-todo-item',
  template: `
    {{ itemTitle }}
  `,
  styleUrls: ['./todo-item.component.css']
})
export class TodoItemComponent implements OnInit {
  @Input() itemTitle: string;

  constructor() { }

  ngOnInit() {
  }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now we need to pass a string, which is the item's title, where we use the component. Go back to `app-root` component and pass the item title to the `todo-item`:

{% code-tabs %}
{% code-tabs-item, title="src/app/app.component.ts" %}
```markup
<ul>
  <li *ngFor="let item of todoList">
    <app-todo-item [itemTitle]="item.title"></app-todo-item>
  </li>
</ul>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The `itemTitle` here in square brackets is the same as declared as the component's `@Input`.

We used property binding on an element we created ourselves! And now we can actually see and understand that property binding binds to an actual property of the component.

## Passing the whole item

We will refactor our code a bit so we can easily implement more functionality in the `todo-item` component, for example editing and removing the item. Instead of passing just the title to the component, we will pass the whole item, and let the component extract the title where needed.

In `todo-item.component.ts` change the interpolation in the template to:

{% code-tabs %}
{% code-tabs-item, title="src/app/todo-item/todo-item.component.ts" %}
```typescript
template: `
  {{ todoItem.title }}
`,
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Rename the Input member and change its type:

{% code-tabs %}
{% code-tabs-item, title="src/app/todo-item/todo-item.component.ts" %}
```typescript
@Input() todoItem: any;
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now, in `app.component.ts` , in the component template, rename the bound property and pass the whole item \(remove the `.title`\):

{% code-tabs %}
{% code-tabs-item, title="src/app/app.component.ts" %}
```markup
<ul>
  <li *ngFor="let item of todoList">
    <app-todo-item [todoItem]="item"></app-todo-item>
  </li>
</ul>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We now have a list of components, and each component received its data from the loop in the parent component. Next we'll see how this list can be dynamic.
