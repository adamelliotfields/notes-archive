# Angular Notes


### AngularJS vs Angular

AngularJS refers to Angular 1.x. Angular refers to Angular 2+ (presently v4.x). AngularJS was based
on MVC architecture, whereas Angular now focuses on services and components. AngularJS used vanilla
JavaScript, whereas Angular now encourages the use of TypeScript (Angular itself is written in
TypeScript). Note that you can use ES5 or ES6 JavaScript; however, typed JavaScript does have
advantages and the examples in the Angular documentation are all written using TypeScript. If you're
already using a compiler in your build process such as Babel, switching to TypeScript will not
introduce any steps you're not already accustomed to.


### Angular Architecture
> See [angular.io/guide/architecture](https://angular.io/guide/architecture)

 * Template: an HTML template file with Angular-ized markup
 * Component: a TypeScript class to manage the template
 * Service: the application logic for the component
 * Module: a bundle of components and services


### Angular Templates

An Angular Component's view is defined by its Template.

```html
<h1>Todo List</h1>
<ul>
  <li *ngFor="let todo of todos">{{todo.title}}</li>
</ul>
```


### Angular Components

An Angular Component controlls a view defined in an HTML template. Angular Components are actually a
construct designed to meet the Web Components standard.

Angular Components are a subset of Angular Directives that always have a Template.

Components are defined using the `@Component` decorator, which can include metadata such as where to
locate templates and stylesheets.

Angular offers Lifecycle Hooks for Components that allow them to exhibit specific behaviors when
Angular creates, updates, and deletes them. For example, the `ngOnInit` method is fired immediately
after Angular creates the Component.

```typescript
@Component({ templateUrl: todo.list.template.html })
class TodoListComponent implements OnInit {
  todos: Todo[];

  constructor(private service: TodoListService) {}

  ngOnInit() {
    this.todos = this.service.getTodos();
  }
}
```


### Angular Services

An Angular Service is any value, function, or feature needed by the application. A Service is
typically a class with a narrow, well-defined purpose. For example, a service class could have the
methods necessary to make HTTP requests to a specific API endpoint.

```typescript
class TodoListService {
  constructor(private http: HttpClient) {}

  getTodos () {
    // Note that you must install the HttpClientModule in your main application module
    // See https://angular.io/guide/http
    return this.http.get('/api/todos').subscribe(response => response.todos);
  }
}
```


### Angular Directives

There are three kinds of Directives in Angular: Component, Structural, and Attribute.

Components are simply Directives with a Template.

Structural Directives manipulate the DOM by adding and removing elements.

Attribute Directives change the appearance or behavior of an element or component.

Directives can be further classified as common, form, and router directives.


### Angular Data Binding

Angular supports "two-way data binding", where changes to the view (typically a form field) update
the Component and vice-versa.

This is in contrast to React's unidirectional data flow, where the Component is the single source of
truth.


### Angular Dependency Injection

Dependency Injection is an inversion-of-control design pattern in which an instance of a class is
automatically "injected" into the class requiring it. In Angular, this pattern is evident when a
Component class requires an instance of a Service class in its constructor. The Dependency Injection
pattern negates the need for instantiating a class every time it is required using the `new`
keyword.

The "injector" will maintain a "container" of previously created classes (typically Services). If a
class is requested, the injector will create it and add it to the container if it is not already
present.

Dependencies are listed as `providers` either in the main application module, or individually in
each component within the `@Component` decorator.


### Framework Comparison

*Note: these opinions are based on my own personal experiences.*

**React**

Pros:
 * Developed in-house at Facebook with contributions from the GitHub community
 * Used in global-scale production applications by Facebook, Airbnb, Netflix, and many, many [others](https://github.com/facebook/react/wiki/sites-using-react)
 * Requires an advanced understanding of modern JavaScript (it will make you a better JavaScript developer)
   - map/filter/reduce
   - ternary operator
   - short-circuiting
   - lambda functions
   - method-binding
   - object rest/spread and destructuring
 * You'll learn basic functional programming concepts
   - idempotence
   - pure fuctions
   - higher-order functions
   - avoiding side-effects (directly mutating global state)
 * Unidirectional data flow means your view and state will always be synced
 * `create-react-app` makes scaffolding a new app a breeze
 * State management using `setState` is incredibly powerful and simple (Redux isn't always necessary)
 * Massive ecosystem of extension libraries available (Redux/MobX, React Router, React Motion, etc)
 * Code-splitting and lazy-loading using dynamic imports is very simple to implement
 * Server-side rendering can be implemented either directly (i.e., `ReactDOMServer`) or via a purpose-built framework (i.e., Next.js)
 * React Native allows native application development for mobile and TV devices
 * Routing is now simpler thanks to React Router 4
 * Testing is simple thanks to Jest and Enzyme
 * TypeScript support using TSX is excellent
 * React 16 added increased rendering speed and enhanced error management

Cons:
 * Requires an advanced understanding of modern JavaScript (you need to already be a good JavaScript developer)
   - no `for` loops
   - no `if` statements
   - no global variables
 * Is a complete paradigm shift from classical DOM traversal and manipulation using jQuery
 * Not a framework, so HTTP requests and Routing require additional libraries
 * Requires compilation (Babel) and module bundling (Webpack)
   - this is a pro for me, but seems to be an area of concern for a lot of people
 * Unidirectional data flow means forms will be tricky when you're first starting out
 * More complex applications using Redux have an incredibly steep learning curve
 * There are way too many options for styling components (CSS-in-JS)
 * CSS Frameworks that use jQuery (i.e., Bootstrap) cannot be used
   - community-maintained forks are available, though
 * There is no standard for animation, unlike Angular
   - `react-transition-group` is available for mounting/unmounting animations
   - `velocity-react` is available as a wrapper around VelocityJS
   - `react-motion` has a steep learning curve
   - GSAP and AnimeJS can be used using `ref` to access the DOM

**Angular**

Pros:
 * Developed in-house at Google with contributions from the GitHub community
 * You'll learn to appreciate the benefits of static typing in JavaScript
 * You'll learn reactive programming using RxJS
 * Enforces a more opinionated approach to application architecture than React
 * Routing and HTTP client are built-in
 * Migrating from Redux to NgRx Store is fairly straight forward
 * Native app development using NativeScript
 * Animations use the Web Animations API (which will eventually be a standard)
   - requires a polyfill for older browsers
 * Angular 4.x focused on significant file size reduction over Angular 2.x

Cons:
 * Overall, Angular has the steepest learning curve compared to React and Vue
 * Not everyone likes TypeScript
 * Like React, you'll need to compile and bundle using TypeScript and Webpack
 * NgRx has the same steep learning curve as Redux, except with fewer available tutorials
 * Finding large-scale production web applications using Angular 4.x has proven difficult
   - Angular remains the top choice for developing internal dashboards and portals, though

**Vue**

Pros:
 * Almost as many stars as React on GitHub (and seems to be getting more stars at a faster rate)
 * API is similar to AngularJS (1.x), which should make transitioning easier
 * Supposedly easier to learn than React (based on what I've read on Quora and Reddit)
   - I personally found React to be easier to learn and more enjoyable to write
 * Does not require a compiler or module bundler (you can just use a bunch of script tags)
   - just because you don't use Webpack doesn't mean you shouldn't optimize your code for production
 * Fast rendering benchmarks
 * Very popular in Asia (Alibaba, Baidu, Tencent, Xiaomi, and Nintendo are using it in production)

Cons:
 * Not backed by a large organization like Facebook or Google
   - financially backed by smaller companies like stdlib and deepstreamHub
 * Even harder to find large-scale production applications than Angular
 * Centralized state management (Vuex) is a relatively new concept in Vue applications
 * Native mobile app development (Weex) is not as mature as React (React Native) or Angular (NativeScript)
