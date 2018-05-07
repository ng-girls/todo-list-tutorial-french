# Add more abilities to service

Let's improve our service by adding more abilities that will be used by our components.

## Adding an item

We'll add a new method to the service, called `addItem`, like so:

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
addItem(item: TodoItem) { 
  this.todoList.push(item);
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now we can change our code in `app/list-manager/list-manager.component.ts` to call the `addItem` method directly from the service:

{% code-tabs %}
{% code-tabs-item title="src/app/list-manager/list-manager.component.css" %}
```typescript
addItem(title: string) {
    this.todoListService.addItem({ title });
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* Note that the service's method expects the whole item, while the component's method expects only the title and constructs the item. \(You may decide to let the service construct the item from the title.\)
* There may be additional logic when calling these methods, i.e. saving the changes in a database \(which we'll implement later\).
* A better way to handle data is using _immutable objects_, but that's a bigger topic than we can cover in this tutorial at the moment.

