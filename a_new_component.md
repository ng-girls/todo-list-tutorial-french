# A new component

In this chapter we will write a whole new component. It will allow us adding an item to the todo list. It will be composed of the HTML elements `input` and `button`.

We'll use Angular-CLI to generate all the needed files and boilerplate for us. Angular-CLI takes commands in a terminal window. This doesn't mean that we have to stop the process `ng serve`. Instead, we can open another terminal window or tab and run the additional commands from there. The changes will be reflected immediately in the browser.
Open another terminal tab and run:

```cmd
ng g c input
```

As we've seen before, `ng` is the command for using Angular-CLI. `g` is a shorthand for `generate`. `c` is a shorthand for `component`. `input` is the name we give to the component.

So the long version of the command is (don't run it):

```
ng generate component input --inline-template
```

> Don't worry about the component name `input`. It will not replace HTMLs `input` element. That's thanks to the prefix that Angular-CLI gives to our components. The default prefix is `app`, so the component selector would be `app-input`. You can create a project stating the prefix of your choice, or change it afterwards in the file `.angular-cli.json`.

Let's take a look of what Angular-CLI created for us.

It created a new folder called `src/app/input`. There are four files there (or three if you're using inline template):

* `input.component.css` - this is where the style that's specific to the component will be placed.
* `input.component.spec.ts` - this is a file for testing the component. We will not deal with it in this tutorial.
* `input.component.ts` - this is the component file where we will define its logic.
* `input.component.html` - this is the HTML template file.


Open the file `input.component.html`. You can see that Angular-CLI has generated a default template for us:

```html
<!-- src/app/input/input.component.html -->

<p>
  input Works!
</p>
```

In the file `input.component.ts` we can see the component's configuration, including its selector, which is the name we gave preceded by the prefix:

```js
// src/app/input/input.component.ts

selector: 'todo-input',
```

We can use this component as is and see the result!

Open the root component file, `app.component.ts` and add the todo-input tag anywhere inside the template (remember we refactored the root component to have an inline template):

```js
// src/app/app.component.ts

template: `
  <h1>
    {{title}}
  </h1>

  <app-input></app-input>
`,
```

Check what's new in the browser!

Let's add some content in our new component. First, add a `title` member which we will use as the todo item's title:

```ts
export class InputComponent implements OnInit {
  title: string = 'Hello World';
  ...
```

It will not interfere with the `app-root` component's `title`, since each component's content is encapsulated within it.

Next, add some content and an interpolation of the title member in the template:

```html
<!-- src/app/input/input.component.ts -->

<p>The title is: {{ title }}</p>
```

Check out the result!

This component doesn't do much at this point. In the next chapters we will learn about the component class, and then implement the component's logic.

