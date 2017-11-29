# JavaScript Framework Comparison

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
  * Angular 4.x focused on significant file size reduction over Angular 2.x

**Cons:**
  * Overall, Angular has the steepest learning curve compared to React and Vue
  * Not everyone likes TypeScript
  * Like React, you'll need to compile and bundle using TypeScript and Webpack
    - you could use SystemJS if you absolutely had to
  * "Hello World" requires EIGHT dependencies
  * NgRx has the same steep learning curve as Redux, except with fewer available tutorials
  * Finding large-scale production web applications using Angular 4.x+ has proven difficult
    - Angular remains the top choice for developing internal dashboards and portals, though

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
  * Directives are similar to AngularJS (1.x), which could make transitioning easier (e.g., `v-for`, `v-if`, `v-model`, etc)
  * Vuex seems more straight-forward than Redux
  * Supposedly easier to learn than React (based on what I've read on Quora and Reddit)
    - these opinions tend to come from the PHP/Laravel community
    - I personally found React to be easier to learn and more enjoyable to write
  * Does not require a compiler or module bundler (you can just use a bunch of script tags)
    - just because you can do something doesn't mean you should
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
  * Even harder to find large-scale production applications than Angular
  * Native mobile app development (Weex) is not as mature as React (React Native) or Angular (NativeScript)
  * Between React and Angular (and Preact/Inferno/Riot/Aurelia/Ember), do we really need another library that does the same thing?

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
