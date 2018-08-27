# Element ref - \#

In the last chapter, we ended with our input component able to display and change the title of our todo item. `input.component.ts` should look like this:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-input-button-unit',
  template: `
    <p>
      input-button-unit works!
      The title is: {{ title }}
    </p>

    <input [value]="title"
           (keyup.enter)="changeTitle($event.target.value)">

    <button (click)="changeTitle('Button Clicked!')">
      Save
    </button>
  `,  
  styleUrls: ['./input-button-unit.component.css']  
})    
export class InputButtonUnitComponent implements OnInit {
  title = 'Hello World';

  constructor() { }                     

  ngOnInit() {
  }

  changeTitle(newTitle: string) {
    this.title = newTitle;
  }
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

First let's remove a bit of the template that we don't need. Remove these lines:

{% code-tabs %}
{% code-tabs-item title="remove this from src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
<p>
  input-button-unit works!
  The title is: {{ title }}
</p>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now we want to take the value of the input \(that the user typed\) and change the title when we press the `Save` button.

We already know how to create a button and react to clicking on it. We now need to pass to the method some data from a different element. We want to use the `input` element's value from inside the `button` element.

Angular helps us do exactly that. **We can store a reference to the element we want in a variable with the name we choose,** for example `inputElementRef`, **using a simple syntax - a hash.** Add `#inputElementRef` to the `input` element, and use it in the `click` event of the button:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
template: `
  <input #inputElementRef
         [value]="title"
         (keyup.enter)="changeTitle($event.target.value)">

  <button (click)="changeTitle(inputElementRef.value)">
    Save
  </button>
`,
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now we can use the value that the user entered in the `input` element in the method called when clicking the `Save` button!

### What is that `#` we see?

Angular lets us define a new local variable named `inputElementRef` \(or any name you choose\) that holds a reference to the element we defined it on, and then use it any way we want. In our case, we use it to access the `value` property of the `input`.

Instead of hunting down the elements via a DOM query \(which is bad practice, as we discussed\), we now can put element references in the template and access each element we want declaratively.

Next, we'll build the list of todo items.

## Explore the element reference

Just like we did in the previous chapter, when we logged $event, you can do the same with `#inputElementRef`.

![lab-icon](.gitbook/assets/lab-3.jpg) **Playground:** Change the method `changeTitle` so it will receive the whole element reference and log it to the console:

{% code-tabs %}
{% code-tabs-item title="src/app/input-button-unit/input-button-unit.component.ts" %}
```markup
<input #inputElementRef
       [value]="title"              
       (keyup.enter)="changeTitle(inputElementRef)">

<button (click)="changeTitle(inputElementRef)">
  Save
</button>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

```typescript
changeTitle(inputElementReference) {
  console.log(inputElementReference);
  this.title = inputElementReference.value;
}
```

Don't forget to put the code back the way it was after you're finished experimenting! It's best to pass to a method exactly the value it needs, instead of the whole object.

## Resources

[Angular Template Reference Variables](https://angular.io/guide/template-syntax#template-reference-variables--var-)

