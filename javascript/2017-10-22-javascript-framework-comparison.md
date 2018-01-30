# JavaScript Framework Comparison
> :calendar: *October 22, 2017*

*Note: these opinions are based on my own personal experiences.*


### React

**Pros:**
  * Developed in-house at Facebook with contributions from the GitHub community
  * Used in global-scale production applications by Facebook, Airbnb, Netflix, and many, many [others](https://github.com/facebook/react/wiki/sites-using-react)
  * Requires an advanced understanding of modern JavaScript (it will make you a better JavaScript developer)
    - ES6 classes
    - ES6 modules
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
  * JSX makes more sense than HTML templates in a JavaScript application
  * Unidirectional data flow means your view and state will always be synced
  * State management using `setState` is incredibly powerful and simple (Redux isn't always necessary)
  * Massive ecosystem of extension libraries available (Redux/MobX, React Router, React Motion, etc)
  * Code-splitting and lazy-loading using dynamic imports is very simple to implement
  * Server-side rendering can be implemented either directly (i.e., `ReactDOMServer`) or via a purpose-built framework (i.e., Next.js)
  * React Native allows native application development for mobile and TV devices
  * Routing is now simpler thanks to React Router 4
  * Testing is simple thanks to Jest and Enzyme
  * `create-react-app` makes scaffolding a new app a breeze
  * `react-hot-loader` simplifies implementing hot module replacement in development
  * TypeScript support using TSX is excellent
  * React 16 added increased rendering speed and enhanced error management

**Cons:**
  * Is a complete paradigm shift from both jQuery and AngularJS, which can make it difficult to learn
  * Only provides component lifecycle methods - everything else you're on your own
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

**Hello World**

```javascript
import React from 'react';
import { render } from 'react-dom';

const style = { fontFamily: 'sans-serif', color: '#007bff', textAlign: 'center' };

const App = ({ message }) => <h1 style={style}>{message}</h1>;

// Must have <div id="root"></div> in your index.html
render(<App message='Hello World' />, document.getElementById('root'));
```


### Angular

**Pros:**
  * Developed in-house at Google with contributions from the GitHub community
  * You'll learn to appreciate the benefits of static typing in JavaScript
  * You'll learn reactive programming using RxJS (i.e., Observables instead of Promises)
  * You'll learn MVC architecture and the dependency injection pattern
    - I found Angular very easy to pick up coming from Spring
  * Routing and HTTP client are built-in
  * Forms are simple thanks to the `ReactiveFormsModule`
  * Migrating from Redux to NgRx Store is fairly straight-forward
  * Redux Dev Tools in Chrome can work with NgRX Store
  * Native app development using NativeScript
  * Styling is simple - either use global stylesheets or component-scope CSS
  * Animations use the Web Animations API (which will eventually be a standard)
    - requires a polyfill for older browsers
  * Angular Material is an excellent UI component library
  * Angular 4.x focused on significant file size reduction over Angular 2.x

**Cons:**
  * Overall, Angular has the steepest learning curve compared to React and Vue
  * Not everyone likes TypeScript
  * "Hello World" requires EIGHT dependencies


**Hello World**

```typescript
import 'core-js/es7/reflect';
import 'zone.js/dist/zone';

import { Component, NgModule, enableProdMode } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';

// Must have <app-root></app-root> in your index.html
const selector: string = 'app-root';
const template: string = '<h1>{{message}}</h1>';
const styles: string[] = ['h1 { font-family: sans-serif; color: #007bff; text-align: center }']

@Component({ selector, template, styles })
class AppComponent {
  public message: string;

  constructor () {
    this.message = 'Hello World';
  }
}

const imports: any[] = [BrowserModule];
const declarations: any[] = [AppComponent];
const bootstrap: any[] = [AppComponent];

@NgModule({ imports, declarations, bootstrap })
class AppModule {}

if (process.env.NODE_ENV === 'production') {
  enableProdMode();
}

platformBrowserDynamic()
  .bootstrapModule(AppModule)
  .catch(error => console.error(error));
```


### Vue

**Pros:**
  * Almost as many stars as React on GitHub (and seems to be getting more stars at a faster rate)
  * Everything just makes sense - there's not a lot of hackery needed to make things work
  * Excellent API documentation
  * Directives are similar to AngularJS (1.x), which could make transitioning easier (e.g., `v-for`, `v-if`, `v-model`, etc)
  * Vuex seems more straight-forward than Redux
  * Does not require a compiler or module bundler (you can just use a bunch of script tags)
  * First-class support for TypeScript (no need to install additional @types definitions)
  * TypeScript decorator pattern and class syntax is very similar to Angular
  * Excellent editor support in VS Code with the Vetur extension
  * Being able to use Jade and Sass (when using `.vue` files with Webpack and `vue-loader`) is awesome
  * Vue Devtools Extension is the best compared to React Devtools and Augury
  * Very popular in Asia (Alibaba, Baidu, Tencent, Xiaomi, and Nintendo are using it in production)
  * Fast rendering benchmarks

**Cons:**
  * Not backed by a large organization like Facebook or Google
    - financially backed by smaller companies like stdlib and deepstreamHub
    - honestly not a huge deal but worth mentioning when comparing to React and Angular
  * Native mobile app development (Weex) is not as mature as React (React Native) or Angular (NativeScript)

**Hello World**

```javascript
// You can use Pug/Jade with vue-loader
<template lang="jade">
  h1 {{message}}
</template>

<script>
  export default {
    // "name" will appear as <App> in Vue Devtools
    name: 'App',
    // "data" must be a function that returns an object
    data () {
      return {
        message: 'Hello World';
      }
    }
  }
</script>

// You can use Sass/SCSS with vue-loader
<style lang="sass" scoped>
  $primary-color: #007bff;

  h1 {
    font-family: sans-serif;
    color: $primary-color;
    text-align: center;
  }
</style>

new Vue({
  // Must have <div id="app"></div> in your index.html
  el: '#app',
  template: '<App />',
  components: { App }
});
```


### Aurelia

**Pros:**
  * Developed by Rob Eisenberg, who previously created Durandal
  * Active community on GitHub, Stack Overflow, and Gitter
  * Uses ES6 classes, property initializers, and decorators
  * Works great with TypeScript
  * Like Angular, it's easy to learn if you've used another object-oriented MVC framework
    - seems to be very popular in the C# / ASP.NET community
  * Includes routing, an HTTP client, animation, and internationalization
  * Dependency injection couldn't be easier
  * Provides simple databinding for any object (both one-way and two-way)
  * Simple pub/sub with the Event Aggregator
  * Extendable via plugins like `aurelia-auth`
  * Works well with Web Components and Polymer
  * Can use any UI library (like jQuery or React)
    - this means you can also use libraries like Bootstrap or Kendo
  * Dedicated Webpack plugin
  * Very fast rendering benchmarks
  * Excellent tutorials on the website

**Cons:**
  * There is a lot of documentation, but it felt hard to find what I was looking for
  * There were a few gotchas with getting Webpack to work
  * Editor support is not quite as robust as the other popular frameworks
  * A dedicated file format like `.vue` would be nice to facilitate single-file components

**Hello World**

```javascript
import { inlineView } from 'aurelia-framework';
import { PLATFORM } from 'aurelia-pal';

@inlineView(`
  <template>
    <h1>Hello World</h1>
  </template>
`)
class App {}

export async function configure (aurelia) {
  aurelia.use.standardConfiguration();

  if (process.env.NODE_ENV !== 'production') {
    aurelia.use.developmentLogging();
  }

  await aurelia.start();

  aurelia.setRoot(PLATFORM.moduleName(App));
}
```
