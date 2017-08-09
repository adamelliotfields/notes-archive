# Babel Preset Plugins
This is a list of all the plugins included with various Babel presets.

Using the presets is super convenient, but if you don't need to target browsers that don't support ES6 (like IE, or 2 year old versions of Chrome), you're compiling more than you need to and also significantly bloating your code. For example, a single React class component with an async/await `axios` request and a for...of loop went from 30 lines of code to 110 when using all of the presets (not to mention adding unnecessary polyfills).

### `babel-preset-env`
You can use `babel-preset-env` and supply the browser(s) you wish to target. I've found Chrome to be the most accurate. Targeting Firefox or Opera was not accurate at all (the version numbers were way off). Edge and Safari were fairly accurate, but the differences between Edge 14 and 15, or Safari 9 and 10 are pretty significant. When in doubt, just try out some code snippets in the Babel [REPL](https://babeljs.io/repl).

Using `babel-preset-env` also has the benefit of selectively polyfilling based on the browser environment. You will need to install `babel-polyfill` and import it in your main entry file. The import statement will be converted to individual import statements for only the polyfills you need. You will also need to install and import `regenerator` if you're targeting browsers that don't support generator functions.

Note that `babel-preset-env` does not include any `stage` plugins or experimental polyfills.

`.babelrc`
```json
{
  "presets": [
    [ "env", {
      "targets": {
        "chrome": 51
      },
      "modules": false,
      "useBuiltIns": true
    }]
  ]
}
```

This will use the `es2016` and `es2017` presets as well as the following CoreJS polyfills:
 - es7.object.values
 - es7.object.entries
 - es7.object.get-own-property-descriptors
 - es7.string.pad-start
 - es7.string.pad-end
 - web.timers
 - web.immediate
 - web.dom.iterable

If you need to target older browsers, `{ "chrome": 40 }` is pretty much the same as using the `es2015`, `es2016`, and `es2017` presets.

### `babel-preset-es2015`
> v6.24.1

 - [`babel-plugin-check-es2015-constants`](https://babeljs.io/docs/plugins/check-es2015-constants/)
   - This check will only validate `const`s. If you need it to compile down to `var` then you must also install and enable `transform-es2015-block-scoping`.
 - [`babel-plugin-transform-es2015-arrow-functions`](https://babeljs.io/docs/plugins/transform-es2015-arrow-functions/)
   - Compiles ES6 arrow functions to ES5.
 - [`babel-plugin-transform-es2015-block-scoped-functions`](https://babeljs.io/docs/plugins/transform-es2015-block-scoped-functions/)
   - Ensures block-level function declarations are block-scoped.
 - [`babel-plugin-transform-es2015-block-scoping`](https://babeljs.io/docs/plugins/transform-es2015-block-scoping/)
   - Compiles ES6 `const` and `let` to ES5.
 - [`babel-plugin-transform-es2015-classes`](https://babeljs.io/docs/plugins/transform-es2015-classes/)
   - Compiles ES6 `class`es to ES5.
 - [`babel-plugin-transform-es2015-computed-properties`](https://babeljs.io/docs/plugins/transform-es2015-computed-properties/)
   - Compiles ES6 computed properties to ES5.
 - [`babel-plugin-transform-es2015-destructuring`](https://babeljs.io/docs/plugins/transform-es2015-destructuring/)
   - Compiles ES6 destructuring to ES5.
 - [`babel-plugin-transform-es2015-duplicate-keys`](https://babeljs.io/docs/plugins/transform-es2015-duplicate-keys/)
   - Compiles objects with duplicate keys to valid strict ES5.
 - [`babel-plugin-transform-es2015-for-of`](https://babeljs.io/docs/plugins/transform-es2015-for-of/)
   - Compiles ES6 `for...of` to ES5.
 - [`babel-plugin-transform-es2015-function-name`](https://babeljs.io/docs/plugins/transform-es2015-function-name/)
   - Applies ES6 `function.name` semantics to all functions.
 - [`babel-plugin-transform-es2015-literals`](https://babeljs.io/docs/plugins/transform-es2015-literals/)
   - Compiles ES6 integer and unicode literals to ES5.
 - [`babel-plugin-transform-es2015-modules-amd`](https://babeljs.io/docs/plugins/transform-es2015-modules-amd/)
   - Transforms ES6 modules to AMD.
 - [`babel-plugin-transform-es2015-modules-commonjs`](https://babeljs.io/docs/plugins/transform-es2015-modules-commonjs/)
   - Transforms ES6 modules to CommonJS.
 - [`babel-plugin-transform-es2015-modules-systemjs`](https://babeljs.io/docs/plugins/transform-es2015-modules-systemjs/)
   - Transforms ES6 modules to SystemJS.
 - [`babel-plugin-transform-es2015-modules-umd`](https://babeljs.io/docs/plugins/transform-es2015-modules-umd/)
   - Transforms ES6 modules to UMD.
 - [`babel-plugin-transform-es2015-object-super`](https://babeljs.io/docs/plugins/transform-es2015-object-super/)
   - Compiles ES6 object super to ES5.
 - [`babel-plugin-transform-es2015-parameters`](https://babeljs.io/docs/plugins/transform-es2015-parameters/)
   - Compiles ES6 default and rest parameters to ES5.
 - [`babel-plugin-transform-es2015-shorthand-properties`](https://babeljs.io/docs/plugins/transform-es2015-shorthand-properties/)
   - Compiles ES6 shorthand properties and methods to ES5.
 - [`babel-plugin-transform-es2015-spread`](https://babeljs.io/docs/plugins/transform-es2015-spread/)
   - Compiles ES6 spread to ES5.
 - [`babel-plugin-transform-es2015-sticky-regex`](https://babeljs.io/docs/plugins/transform-es2015-sticky-regex/)
   - Compiles ES6 sticky regex to an ES5 RegExp constructor.
 - [`babel-plugin-transform-es2015-template-literals`](https://babeljs.io/docs/plugins/transform-es2015-template-literals/)
   - Compiles ES6 template literals to ES5.
 - [`babel-plugin-transform-es2015-typeof-symbol`](https://babeljs.io/docs/plugins/transform-es2015-typeof-symbol/)
   - Wraps all `typeof` expressions with a method that replicates native behavior.
 - [`babel-plugin-transform-es2015-unicode-regex`](https://babeljs.io/docs/plugins/transform-es2015-unicode-regex/)
   - Compiles ES6 unicode regex to ES5.
 - [`babel-plugin-transform-regenerator`](https://babeljs.io/docs/plugins/transform-regenerator/)
   - Transforms `async` and generator functions.
   - Requires either `babel-polyfill` or Facebook's regenerator runtime.
   - Does not require a syntax plugin (since Babylon v6.9.1).

### `babel-preset-es2016`
> v6.24.1

 - [`babel-plugin-transform-exponentiation-operator`](https://babeljs.io/docs/plugins/transform-exponentiation-operator/)
   - Compiles exponentiation operator to ES5.

### `babel-preset-es2017`
> v6.24.1

 - [`babel-plugin-syntax-trailing-function-commas`](https://babeljs.io/docs/plugins/syntax-trailing-function-commas/)
   - Allows Babel to parse trailing function commas.
   - No longer necessary (since Babylon v6.9.1).
 - [`babel-plugin-transform-async-to-generator`](https://babeljs.io/docs/plugins/transform-async-to-generator/)
   - Compiles ES8 `async` functions to ES6 generators.

### `babel-preset-react`
> v6.24.1

 - [`babel-plugin-transform-flow-strip-types`](https://babeljs.io/docs/plugins/transform-flow-strip-types/)
   - Strips all Flow type annotations and declarations from your output code.
 - [`babel-plugin-syntax-jsx`](https://babeljs.io/docs/plugins/syntax-jsx/)
   - Allows parsing of JSX syntax.
 - [`babel-plugin-transform-react-display-name`](https://babeljs.io/docs/plugins/transform-react-display-name/)
   - Adds `displayName` to `React.createClass` calls.
 - [`babel-plugin-transform-react-jsx`](https://babeljs.io/docs/plugins/transform-react-jsx/)
   - Transforms JSX to `React.createElement` function calls.
 - [`babel-plugin-transform-react-jsx-source`](https://babeljs.io/docs/plugins/transform-react-jsx-source/)
   - Adds `__source={{ fileName, lineNumber }}` to JSX elements.
 - [`babel-plugin-transform-react-jsx-self`](https://babeljs.io/docs/plugins/transform-react-jsx-self/)
   - Adds `__self={this}` to JSX elements (used in development mode to generate runtime warnings)

### `babel-preset-stage-3`
> v6.24.1

 - [`babel-plugin-syntax-trailing-function-commas`](https://babeljs.io/docs/plugins/syntax-trailing-function-commas/)
   - Allows Babel to parse trailing function commas.
   - No longer necessary (since Babylon v6.9.1).
 - [`babel-plugin-transform-async-generator-functions`](https://babeljs.io/docs/plugins/transform-async-generator-functions/)
   - Transforms `async` generator functions and `for...await` statements to ES6 generators.
 - [`babel-plugin-transform-async-to-generator`](https://babeljs.io/docs/plugins/transform-async-to-generator/)
   - Compiles ES8 `async` functions to ES6 generators.
 - [`babel-plugin-transform-exponentiation-operator`](https://babeljs.io/docs/plugins/transform-exponentiation-operator/)
   - Compiles exponentiation operator to ES5.
 - [`babel-plugin-transform-object-rest-spread`](https://babeljs.io/docs/plugins/transform-object-rest-spread/)
   - Transforms rest properties for object destructuring assignment and spread properties for object literals.

### `babel-preset-stage-2`
> v6.24.1

 - *Includes `babel-preset-stage-3`*
 - [`babel-plugin-transform-class-properties`](https://babeljs.io/docs/plugins/transform-class-properties/)
   - Transforms class property initializers.
 - [`babel-plugin-transform-decorators`](http://babeljs.io/docs/plugins/transform-decorators/)
   - Compiles class and object decorators to ES5.
 - [`babel-plugin-syntax-dynamic-import`](https://babeljs.io/docs/plugins/syntax-dynamic-import/)
   - Allows parsing of `import()`
   - No longer necessary (since Babylon v6.12.0).

### `babel-preset-stage-1`
> v6.24.1

 - *Includes `babel-preset-stage-2` and `babel-preset-stage-3`*
 - [`babel-plugin-transform-class-constructor-call`](https://babeljs.io/docs/plugins/transform-class-constructor-call/)
   - Transforms class constructor calls.
   - *Deprecated: The proposal has been withdrawn and the plugin will be removed in Babel 7.*
 - [`babel-plugin-transform-export-extensions`](https://babeljs.io/docs/plugins/transform-export-extensions/)
   - Compiles additional `export...from` statements to ES6.

### `babel-preset-stage-0`
> v6.24.1

 - *Includes `babel-preset-stage-1`, `babel-preset-stage-2`, and `babel-preset-stage-3`*
 - [`babel-plugin-transform-do-expressions`](https://babeljs.io/docs/plugins/transform-do-expressions/)
   - Compiles `do` expressions to ES5.
 - [`babel-plugin-transform-function-bind`](https://babeljs.io/docs/plugins/transform-function-bind/)
   - Compiles the function bind operator (`::`) to ES5.

### Plugin Requirement Table
Here is a table showing which plugins you need to target specific browser versions (desktop browsers only, for brevity).

ES6 features like Promises, generator functions, `Object.assign`, or `Array.prototype.includes` can by polyfilled by including `babel-polyfill` in your main entry file.

Experimental features commonly used in React such as class property initializers and decorators will require a Babel plugin to work in any modern browser. Chrome 60 is currently the only browser that supports the object spread/rest operator, so you should probably include the Babel plugin for it as well.

Browser versions below are based on what `babel-preset-env` will transpile. For example, Babel will transpile arrow functions when targeting Chrome 46 and below.

| Babel Transform           | Chrome | Edge | Safari |
|---------------------------|--------|------|--------|
| `arrow-functions`         | < 47   | < 13 | < 10   |
| `block-scoping`           | < 49   | < 14 | < 10   |
| `classes`                 | < 46   | < 13 | < 10   |
| `computed-properties`     | < 44   | < 12 | < 8    |
| `destructuring`           | < 51   | < 15 | < 10   |
| `for-of`                  | < 51   | < 15 | < 10   |
| `parameters`              | < 49   | < 14 | < 10   |
| `shorthand-properties`    | < 43   | < 12 | < 9    |
| `spread`                  | < 46   | < 13 | < 10   |
| `template-literals`       | < 41   | < 13 | < 9    |
| `regenerator`             | < 50   | < 13 | < 10   |
| `exponentiation-operator` | < 52   | < 14 | < 10.1 |
| `async-to-generator`      | < 55   | < 15 | < 10.1 |
