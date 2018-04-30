# Service

In Angular, a service is (typically) a JavaScript class that's responsible for performing a specific task needed by your application. In our todo-list application, we'll use a service to save all the tasks, and use it by injecting it into the components.

## Create the service

```text
ng g s todoList
```

This command will generate the service and put it under src/app/todo-list.service.ts

## Make the service a provider

To start using the service, we first need to *provide* it in an ngModule. Start by adding this code in `/src/app/app.module.ts`:

```ts
import { TodoListService } from './todo-list.service';
```

Next, add the service to the `providers` array, so that the ngModule looks like this:

```ts
@NgModule({
  declarations: [
    AppComponent,
    InputComponent,
    ItemComponent,
    ListManagerComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [TodoListService],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

This tells Angular to provide (that is, create and inject) an instance of our service when we ask for it anywhere in our application.

## Move the todo list from component to service

We now need to move the `todoList` array from `ListManagerComponent` to our new service. Go to the generated service file, `src/app/todo-list.service.ts`, and add this code just above the constructor:

```ts
  private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];
```

## Create a method to return the list

Now add a `getTodoList` method that will return the `todoList` array. The service will look like this:

```ts
import { Injectable } from '@angular/core';

@Injectable()
export class TodoListService {

  private todoList = [
    { title: 'install NodeJS' },
    { title: 'install Angular CLI' },
    { title: 'create new app' },
    { title: 'serve app' },
    { title: 'develop app' },
    { title: 'deploy app' },
  ];

  constructor() { }

  getTodoList() {
    return this.todoList;
  }
}
```

## Inject and use the service

After creating the service, we can inject it into our list-manager component. Go to `src/app/list-manager/list-manager.component.ts` and add the following import code:

```ts
import { TodoListService } from '../todo-list.service';
```

Now remove the `todoList` array, but keep the `todoList` member:

```ts
  todoList;
```

Change the constructor to be:

```ts
constructor(private todoListService:TodoListService) { }
```

And now use the service to assign the `todoList` array inside the `ngOnInit` method:

```ts
ngOnInit() {
  this.todoList = this.todoListService.getTodoList();
}
```

