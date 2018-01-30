# Angular Notes
> :calendar: *October 22, 2017*

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

Templates can either be separate HTML files or string literals defined in the Component's metadata.

Templates can be styled either using global CSS, or as an array of CSS rules also defined in the
Component's metadata.

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
