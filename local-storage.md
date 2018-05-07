# Local storage

We would like to persist the todo list on our computer, so that when accessing or reloading the app we'll see the list with the changes we've made. Ideally the list would be saved in a database, but we will implement a simple version using the browser's own storage. 

## What is local storage?

Local storage, as its name implies, is a tool for storing data locally. Similar to cookies, local storage stores the data on the user's computer, and gives us, as developers, a quick way to access this data for both reading and writing.

> There are libraries you can use that give you a wider range, more generic, robust methods to manage the data in the local storage. Here we will implement a simple solution.

## Browser support

As local storage was first introduced to us along with HTML5, all browsers that support HTML5 standard will also support local storage.  
Basically, it's supported by most modern web browsers, including IE 8.

## We want to see some code!

First, in order to use local storage, we can simply access a `localStorage` instance which is exposed to us globally. That means that we can call all available methods in this interface by simply using this instance.

Local storage stores data as keys and values, and the interface is quite simple. It has two main methods: `getItem` and `setItem`. Here's an example of using them:

{% code-tabs %}
{% code-tabs-item title="code for example" %}
```typescript
localStorage.setItem('name', 'Angular');

let name = localStorage.getItem('name'); 
alert(`Hello ${ name }!`);
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Another useful method is `clear`. It's used to clear all the data from local storage:

{% code-tabs %}
{% code-tabs-item title="code for example" %}
```typescript
localStorage.clear();
```
{% endcode-tabs-item %}
{% endcode-tabs %}

There are a few more wonderful methods you can use, as described in the [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/API/Storage).

## Angular time \(back to our app\)

In the following section, we will build a local storage service that will be used to store our todo list items. It will be a generic service for lists of objects. We'll need to tell it the name of data we're looking for \(a key\), so we can use it to store other lists as well. 

As in earlier chapters, we will generate the service using the Angular CLI. We will name the new service  `storage`

```bash
ng g s services/storage
```

The new file, `storage.service.ts`, will be created with the following code:

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class StorageService {

  constructor() { }

}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

If something looks unfamiliar or odd to you, please refer to the [Creating a Service chapter](service.md) for more detailed information about services.

We need to provide the service in our NgModule. Open `app.module.ts` and add the new class to the `providers` list:

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
providers: [
  TodoListService, 
  StorageService
],
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Make sure the class is also imported into the file:

{% code-tabs %}
{% code-tabs-item title="src/app/app.module.ts" %}
```typescript
import { StorageService } from './services/storage.service';
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Since we cannot access an item on the list directly in the local storage, we'll implement only two methods: getting the data and setting the data. Changing the list will be done by the TodoListService. To each method we'll pass the key \(name\) of the data we want. 

### getData

This method will get and return the data \(object, list, etc.\) stored in the service under the given key:

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
  getData(key: string): any {
    return JSON.parse(localStorage.getItem(key));  
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Wait! Wait! why `JSON.parse`? The answer is simple: As described above, local storage stores data as key-value pairs, and the values are stored as **strings**. So, if we want to have a real object \(or list\) to work with, we must parse the string into a valid JavaScript object.

### setData

This method will save the given data \(object, list, etc.\) under the given key. 

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
  setData(key: string, data: any) {
    localStorage.setItem(key, JSON.stringify(data));
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

That's it! Let's use this service in our `ToDoListService`.

> As mentioned above, this service could have a wider API with more robust methods. When you write a service for accessing a database you will have other methods for adding, modifying and deleting specific items.





Here we use the `localStorage` method `setItem`, which takes a key \(the first argument\) and a string value \(the second argument\) and stores it in local storage. First we fetch the list we have in storage. It's already parsed in the method `getList`. We push an item to the list. Then we replace the list we had in the storage with the modified one.

### updateItem

Here we want to update an existing item. We'll assume that we know the index of the item. \(Other implementations may use an item ID to search the list.\)

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
  updateItem(key, index, changes) {
    const list = this.getList(key);
    const item = list[index];
    const newItem = {...item, ...changes};
    list[index] = newItem;
    localStorage.setItem(key, JSON.stringify(list));
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

So what is going on here?  
Once again, we fetch the current list from the local storage. We modify the item located in the `index` with the `changes`. The spread operator is used here within an object. A new object is constructed, composed of the original set of keys and values \(`...item`\) which are overridden by the keys and values of `changes`. \(If a key in the `changes` object doesn't exist in `item`, it is added.\)

### DRY - Don't Repeat Yourself

You may have noticed that we have the same line of code both in `pushItem` and in `updateItem`:

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
localStorage.setItem(key, JSON.stringify(list));
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We'd like to reduce code repetition, and extract the repeated code into a method:

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
setList(key, list) {
    localStorage.setItem(key, JSON.stringify(list));
}
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We can use this method from within the service and from outside. Refactor the `pushItem` and `updateItem` methods to use `setList`.

### deleteItem

This method will remove an item from the list. Again, we assume we know the item's index:

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
  deleteItem(key, index) {
    const list = this.getList(key);
    this.todoList.splice(index, 1);
    this.setList(key, list);
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

`splice(i, n)` removes `n` items starting from index `i`.  
In our code, we remove only one item \(that's why we use 1 as the second parameter\).

### Final result

After refactoring, reducing some more lines of code \(in updateItem\) and adding parameters types, the service should look like this:

{% code-tabs %}
{% code-tabs-item title="src/app/services/list-storage.service.ts" %}
```typescript
import { Injectable } from '@angular/core';

@Injectable()
export class ListStorageService {

  constructor() {
  }

  getList(key: string): any[] {
    return JSON.parse(localStorage.getItem(key));
  }
  
  setList(key: string, list: any[]) {
    localStorage.setItem(key, JSON.stringify(list));
  }

  pushItem(key: string, item: any) {
    const list = this.getList(key);
    list.push(item);
    this.setList(key, list);
  }

  updateItem(key: string, index: number, changes: any) {
    const list = this.getList(key);
    list[index] = { ...list[index], ...changes };
    localStorage.setItem(key, JSON.stringify(list));
  }

}

```
{% endcode-tabs-item %}
{% endcode-tabs %}

## Use the ListStorageService

We'd like to use the newly created service from within `TodoListService`. First we'll inject the `ListStorageService` into the `TodoListService`, just like we injected the latter into `ListManagerComponent`. We'll ask for an instance in the constructor, and make sure the Class is imported. We'll move the default todo list outside the class. We'll also add a constant with the key of our storage.

> A better practice is to use the environments files for storing keys. This way you can manage different keys for each environment - development, production, staging, etc.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
import { Injectable } from '@angular/core';
import { TodoItem } from '../interfaces/todo-item';
import { ListStorageService } from './list-storage.service';

const todoListStorageKey = 'Todo_List';

const defaultTodoList = [
  {title: 'install NodeJS'},
  {title: 'install Angular CLI'},
  {title: 'create new app'},
  {title: 'serve app'},
  {title: 'develop app'},
  {title: 'deploy app'},
];

@Injectable()
export class TodoListService {
  todoList: TodoItem[];

  constructor(private listStorageService: ListStorageService) { }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

We'll keep a runtime version of the todo list in the service to help us manage it in the app - the todoList property. We'll initialize it in the constructor with either the list in the local storage, if exists, or the default one.

{% code-tabs %}
{% code-tabs-item title="src/app/services/todo-list.service.ts" %}
```typescript
constructor() {
    this.todoList = JSON.parse(localStorage.getItem(storageName)) || defaultList;
  }
```
{% endcode-tabs-item %}
{% endcode-tabs %}

The above will make sure that if data was not yet stored in `localStorage`, our service will still have some default data to return. This also means you can completely remove the `todoList` array from `TodoListService`, since now the default list is handled here.

## Almost done!

Our service is now ready for work!

Now for our app to use the new local storage service, let's open up `todo-list.service.ts` and modify it.

First we need to import the new service:

```typescript
import { TodoListStorageService } from './todo-list-storage.service';
```

Then, we need to inject it in the constructor so we will have an instance to work with:

```text
constructor(private storage:TodoListStorageService) {
}
```

This will let us use `this.storage` across the todo-list service.

Let's also modify the current methods:

**Before**

```text
getTodoList() {
    return this.todoList;
}

addItem(item) {
    this.todoList.push(item);
}
```

**After**

```text
getTodoList() {
    return this.storage.get();
}

addItem(item) {
    return this.storage.post(item);
}
```

Now we have one last modification to make. Open up `list-manager.component.ts` and modify the `addItem` method this way:

```text
addItem(title:string) {
    this.todoList = this.todoListService.addItem({ title });
}
```

The above change will make sure that when we add a new item, our list will also be updated visually.

## Summary

In this tutorial we learned what local storage is and how to use it. We saw that `localStorage` is a great and a pretty straight-forward tool for developers to store data locally on the users' computers/devices. We then implemented a new service that uses `localStorage` to store the todo-list items, and updated the rest of the components to support this new service.

