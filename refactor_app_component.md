# Refactor App Component

We're going to perform a small refactoring. The `todo-root` shouldn't have such a large template and all this logic. It should just call another component that will deal with that.

* Create a new component called `list-manager` and configure inline-template.
* Move the code from `AppComponent` to `ListManagerComponent`. (Be careful not to change the list manager component's class name!)

* Call the new component from the `AppComponent` template:

```html
  template: `
    <todo-list-manager></todo-list-manager>
  `,
```

That's it! Now we can go on.

[See the results on StackBlitz](https://stackblitz.com/github/angularbootcamp/todo-list-tutorial-steps/tree/step-12_Refactor_App_Component)
