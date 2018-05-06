# Refactor App Component

We're going to perform a small refactoring. The `app-root` shouldn't have such a large template and all this logic. It should just call another component that will deal with that.

* Create a new component called `list-manager`: 

`ng g c list-manager`

* Move all the code from `app-root` to `list-manager`. \(Be careful not to change the list manager component's class name!\)
* Call the new component from the `app-root` template:

```markup
  template: `
    <app-list-manager></app-list-manager>
  `,
```

That's it! Now we can go on.

