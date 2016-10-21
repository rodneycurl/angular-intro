## Angular Intro, Controllers, and Directives

- Describe the benefits of using a front end framework
- Differentiate between directives, modules, and controllers in Angular
- Render and bind controller data in the view.
- Explain what an Angular directive is and how we use them
- Use `ng-repeat` to iterate over data.
- Use `ng-hide`/`ng-show` to hide and show elements.
- Use `ng-model` to bind user input to model data
- Use `ng-click` to respond to user events

## Framing

Today we are transitioning into a new unit, as we begin to focus on building out bigger and bigger applications. As our applications grows in size and complexity, it can become increasingly difficult to manage all of our data, rendering logic, and view code from a code maintainability perspective without some sort of structure or guidelines. Luckily, the field of web development is evolving to rapidly produce solutions to this problem, and today we will look at one particular solution - Angular.js

<details>
<summary>**Q**: What is a Front End Framework?</summary>

- a library that attempts to move some or all application logic to the browser, while providing a simple interface for keeping the front-end in sync with the back-end
- applications can run completely in the browser, minimizing server load since the server is only accessed when the front end needs to synchronize data with the backend
- server sends over the app in the initial request (HTML/CSS/JS) then JS makes all subsequent requests with AJAX
- provides more fluid user experience
- loads everything from the database on page load (data and templates) then renders/updates the page content based on user interaction.

</details>

<details>
<summary>**Q**: What is Angular?</summary>

- its a structural front end framework for dynamic web apps
- uses `HTML` as your template language and lets you extend `HTML`'s syntax to express your application's functionality
- allows you to utilize `HTML` attributes to add behavior through JS. (directives)
- utilizes two-way data binding so that changes are reflected in various areas and persisted immediately without page refresh
- Angular is different and blurs a lot of the lines of traditional front-end dev
  - there'll be a lot of logic in the `DOM`
</details>

## I Do: Building a Angular App

Angular excels at providing a powerful framework to build apps that **dynamically render data** in the browser. In order to get oriented to some of the new conventions and features of working with Angular, we are going to build a simple todo application.

### Setup

To start working with Angular, all we need is an `html` file, a `js` file, and a link to the Angular CDN.

Let's hop into our terminal and create those files…

```bash
$ mkdir angularTodos
$ cd angularTodos
$ touch index.html app.js
```

Great, now let's fill our `index.html` with some boilerplate and the necessary script tags.

```html
<!-- index.html -->
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="UTF-8">
 <title>Angular Todos</title>

 <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.5.6/angular.min.js"></script>
 <script src="app.js"></script>
</head>
<body>

</body>
</html>
```

> **Note**: make sure to link to the Angular CDN **before** your custom JS file

### The Data

To start, let's represent some important goals from WDI as todos in our application.

```js
// app.js
let todoData = [
  { name: 'Build an app with Rails', completed: true },
  { name: 'Project 2', completed: true },
  { name: 'Build an app with Angular', completed: false },
  { name: 'Project 3', completed: false },
  { name: 'Build an app with Express', completed: false },
  { name: 'Build an app with Mongo', completed: false },
  { name: 'Build an app with React', completed: false },
  { name: 'Project 4', completed: false },
  { name: 'Become a Rockstar', completed: true }
]
```

> For now, we'll just keep it simple as we'll store our data as an array of hard-coded JS objects - with each `todo` having a `name` and `completed` property.

Great, now that we have some data to play with, let's begin to work on rendering it meaningfully in the browser.

### Bootstrapping Angular

Building an Angular app is a lot like playing with Legos, in that we will mostly just be putting together a bunch of special pieces to construct a complex structure.

Since we already have loaded Angular into our app, we now have access to the global `angular` object, which we will use to define our app's [module](https://docs.angularjs.org/api/ng/function/angular.module),.

```js
// app.js
angular.module("todoApp", [])
```

> **Note**: here we are defining a new [module](https://docs.angularjs.org/api/ng/function/angular.module), `angular.module`, with **two** arguments. The first argument is the **name** of the Angular module. The second argument is an **array of dependencies**, or other modules on which the current module will depend.

Now that we have our app's module defined, we need to tell Angular to actually use it. To do this, we will need to use one of Angular's many built in directives.

## [Directives](https://docs.angularjs.org/guide/directive)

Directives are markers on a DOM element (tags and attributes) that tell AngularJS's HTML compiler to attach a specified behavior to that DOM element.

Directives are Angular's way of letting you add behavior to elements and attributes. DOM elements already have behavior we would want for displaying and linking documents, the original utility of the web. Angular directives add behaviors we would want for building applications.

### [`ng-app`](https://docs.angularjs.org/api/ng/directive/ngApp).
Let's add our very first directive. In the `index.html`:

```html
<html lang='en' ng-app='todoApp'>
```

> `ng-app` designates the entry point of our application and is usually place near the root element of the page (i.e. the `<html>` or `<body>` tags). The argument to `ngApp` should correspond with the **name** of your app module. In this case, we're adding it to the `<html>`. The domain of the directive begins and ends with the opening and closing tags of the html element on which the directive is defined.

In essence, linking `ng-app` with our module tell Angular that this `html` file is now an Angular app, and anything inside those tags can use Angular's features / syntax.

## [Angular Expressions](https://docs.angularjs.org/guide/expression)

Now that we have successfully bootstrapped our Angular app, let's begin to focus on displaying our todos in the browser.

In order to display dynamic data, Angular uses its own templating syntax that we can use in our `html` files, much like how we used `erb` files in Ruby.

In Angular, any Javascript that we want to execute and print to the screen can be placed in an **expression**. Expressions are denoted with double curly brackets `{{ }}`, and will evaluate anything placed between.

For example, adding `{{5 + 5}} ` to the `body` of our `index.html` file, would print `10` to the screen.

## You Do: Setup Grumblr Application (5 mins)

For the rest of this morning, you will be working on building Grumblr, a one-model application that will allow users to post their `grumbles`.

To start:
- Create a directory called `grumblr`
- Inside that directory, create two files - a `html` file, and a `js` file
- Add some boilerplate `html` and make sure to link to your `js` file and the **Angular CDN**
- Create and store to a variable, an array of hard-coded data that contains at least 5 objects with the following properties:
  - `title`
  - `author`
  - `content`
  - `photo_url`
- Define you application's initial module and use a directive to bootstrap your Angular application
- Use Angular Expressions to get the product of `5 x 5` to display in the browser

## [Angular Controllers](https://docs.angularjs.org/guide/controller) (10/80)

Great, so we now have a way to write javascript in our `html`, now we just have to figure out how to render those todos we defined earlier!

In order to pass data into the view, in Angular we need a **controller**. Controllers are the go-between for views (our HTML) and our data.

Let's add a new controller definition to `app.js`:

```js
// app.js
angular
  .module("todoApp", [])
  .controller("todosCtrl", [ todoController ])

function todoController () {
  this.todos = todoData
}
```

> Here we've instantiated a new controller for our app. This is where all the logic and CRUD functionality will be contained.

> **Note** In our controller definition, the first argument is the **name** of the controller. The second argument is an **array of dependencies** for the controller, and **must include a function** that encloses all the functionality of the controller.

 As in Rails, the controller is an interface between our data and our view. Just like how in Rails, to make data show up in a view, we'd make it an instance variable, as in `@variable = "Some data"`. To do the same in Angular, we attach it to `this`, as in `this.variable = "Some data"`. Here we are attaching all of our hard-coded todo objects as a property on our controller called `todos`

### Initializing the View Model

Now that we have defined our controller, we need to actually tell Angular where we want to use it.
We can invoke our controller by using another Angular directive, `ng-controller`.

In `index.html`, let's add this directive to our `body` element:

```html
<body ng-controller='todosCtrl as vm'>

</body>
```

> We used the [`ng-controller` directive](https://docs.angularjs.org/api/ng/directive/ngController) here in order to instantiate our controller in the DOM. In the same way that `ng-app` established the domain of the js functionality in the html element, the `ng-controller` establishes the domain in this div.

> `vm` is an instance of our controller. `ng-controller` gives the whole div access to all the values and methods defined in that controller. This instance of a controller is called a "ViewModel".

The `todosCtrl as vm` syntax is important here. In essence, we are creating a new instance of our controller that we defined earlier, and are saving it to a variable we are calling `vm`. This is significant because now, any property that we defined in our controller, is available in the view as a property on our instance.

Therefore, we now have all the pieces necessary to print a todo to the page...

Let's add some code inside the `body` to display a single todo:

```html
<body ng-controller='todosCtrl as vm'>
  <p>First todo: {{vm.todos[0]}}</p>
</body>
```

Now, when we open our `index.html` file in the browser, we can see our data rendered in the browser!

## `ng-repeat`

Where we left off, we could only render one todo at a time. We could continue this pattern and hard code each todo out, but as you might have guessed, there is a better way that will allow us to iterate over every todo in our data to generate duplicative UI.

This is a great opportunity to take advantage of Angular's `ng-repeat` directive...

In `index.html`:

```html
<body ng-controller='todosCtrl as vm'>
  <h2>Todos</h2>
  <div ng-repeat="todo in vm.todos">
    <p>{{$index + 1}}. {{todo.name}} - {{todo.completed}}</p>
  </div>
</body>
```

> All we've done here, is print each todo with it corresponding index value + 1. It is important to note that `$index` is the index value for each iteration of the `ng-repeat`

Now, when we refresh in the browser we see each of our todos with their respective data and markup displaying.

## `ng-repeat` - You Do - Grumblr (10 mins)

- Define a new controller attached to your app's module
- Attach a property to your controller called `grumbles` which is equal to all of your hard-coded data
- In the view, initialize an instance of your controller as the view model
- Use a directive to display all of the information for each `grumble` (title, name, content, photo url)

---
## Break (10 mins)
---

## User Input and Data Binding

Up until this point we have focused on displaying data, or the R of CRUD for a todo. Let's continue to dive deeper into Angular, by looking at how to respond to user events and capture user input, two fundamentals for front-end web development.

Let's continue building out our app's functionality, by adding the ability to add a new todo.

First we need to add some UI to allow a user to enter a new todo.

For now, a simple input and button will do...

In `index.html`:

```html
<body ng-controller='todosCtrl as vm'>
  <h2>Todos</h2>
  <div ng-repeat="todo in vm.todos | filter: {completed: false}">
    <p>{{$index + 1}}. {{todo.name}} - {{todo.completed}}</p>
  </div>
  <div>
    <input type="text">
    <button>Add Todo</button>
  </div>
</body>
```

Ok, now that we have that piece of UI, let's focus on just wiring up some JS to run whenever that button is clicked.

### [`ng-click`](https://docs.angularjs.org/api/ng/directive/ngClick)

If we want to hook into Angular's custom event system, we need to utilize its built-in directives.

In this case, we can add a `ng-click` directive to an element so that whenever its clicked, we can fire a specified function defined in our controller.

Let's add that `ng-click` to our button so that it will fire a method `addTodo()` that we will define later on in the controller...

In `index.html`:

```html
<div>
  <input type="text">
  <button ng-click="vm.addTodo()">Add Todo</button>
</div>
```

> **Note**:  The value of what's passed to `ng-click` is a method on `vm`, and the method is invoked!

Now, in the controller we can go write the function definition for the `addTodo()` method we just referenced.

To start off and make sure that everything is wired up correctly, let's just log something to console to test that its working...

In `app.js`:

```js
function todoController () {
  this.todos = todoData
  this.addTodo = function() {
    console.log("clicked!")
  }
}
```
> Here we can just define a method on our controller, which will be the same function called whenever a user clicks the button.

When we refresh the page in the browser, we should be able to click and see the message logged to the console.

Next up, let's focus on capturing whatever the user entered, and then adding that to our collection of todos.

### [`ng-model`](https://docs.angularjs.org/api/ng/directive/ngModel)

Now, our goal is to access whatever the user entered into the form in our controller. To start, we need a way of talking about the data that the user entered. Angular allows us to bind the data entered into the input as a variable.

The cool thing about this, is that this variable will update on every change of input - in real time! This is one of Angular's core selling points, and is known as **two-way data binding**.

Let's see what happens when we track the user's input to a variable, and then display that variable.

In `index.html`:

```html
<div>
  <input type="text" ng-model="vm.newTodo">
  <button ng-click="vm.addTodo()">Add Todo</button>
  <p>User input: {{vm.newTodo}}</p>
</div>
```
> Here we added an `ng-model` to our input tag with a value of a `newTodo` property we are attaching to our `vm`.

Now, when we refresh in the browser, we can see the data we enter into the input displayed in realtime.

Furthermore, in this example we bound the user's input to a property we are calling `newTodo` on our the `vm`. Why this is important is that because of Angular's two-way data binding, any property attached to the VM in the view, is also available as a property inside the controller. This means that we are now all set up and ready to complete our `addTodo` method in the controller.

Moving back to our `addTodo` method in the controller, we need to grab the user input, and create a new todo from that data.

Let's look at the code that makes this a reality:

```js
this.addTodo = function(){
  let todo = {name: this.newTodo, completed: false }
  this.todos.push(todo)
};
```

Here we have access to the todo the user entered via a property on a controller of the same name that we used in the view (`this.newTodo`), we use that data to create a new todo, then add it to our collection.

## You Do: Add a New Grumble

- Create some UI for the user to enter in information about a new Grumble (i.e. inputs for `title`, `author`, `content`, and `photo_url`, as well as a button to submit)
- Wire up your form's button to a method defined in controller
- Bind each input to a property attached on the view model
- When the user clicks submit, inside your method in the controller - use the user data to create a new `grumble` and add it to your collection of `grumbles`.

## Bonus: Conditional Rendering

Since Angular is so coupled to the view, you will often times run into situations were you want to conditionally render a single / group of element/s. Angular provides several different options to quickly embed logic into your templating.

Let's take a look at an example, by adding a new feature to our app. So far our todo list application is coming along nicely, but it would be really great if we could only show the todos that are not yet completed.

### [`ng-show`](https://docs.angularjs.org/api/ng/directive/ngShow)

In order to display only the todos that have a `completed` value of `true`, we can take advantage of the Angular directive `ng-show`:

Let's add it to our view in `index.html`:

```html
<body ng-controller='todosCtrl as vm'>
  <h2>Todos</h2>
  <div ng-repeat="todo in vm.todos">
    <p ng-show="todo.completed">{{$index + 1}}. {{todo.name}} - {{todo.completed}}</p>
  </div>
</body>
```

> `ng-show` takes any truthy or falsey value as an argument, and if it evaluates to true - the element will be displayed, otherwise the element is set as display:none.

> **Note**: To offer a semantic opposite, there is also the equivalent directive [ng-hide](https://docs.angularjs.org/api/ng/directive/ngHide) which hides an element if the passed in value is true.

### [Filters](https://docs.angularjs.org/api/ng/filter/filter)

Another very useful feature of Angular is its built in filtering functionality. Anywhere we are using `ng-repeat`, we can add a filter to modify the collection it is iterating over.

Let's look at another way of only showing the todos that have not yet been completed...

In `index.html`:
```html
<body ng-controller='todosCtrl as vm'>
  <h2>Todos</h2>
  <div ng-repeat="todo in vm.todos | filter: {completed: false}">
    <p>{{$index + 1}}. {{todo.name}} - {{todo.completed}}</p>
  </div>
</body>
```
> **Note**: the `|` operator starts a filter - which needs a key value pair of how to filter/sort. Note, here we are passing an object as the value specifying that we want to filter by the `completed` property of a `todo` as `false`

### You Do: Filters in Grumblr

Implement a search functionality for your Grumblr application so that a user can enter in some input, and your collection of `grumbles` is filtered based on user input
