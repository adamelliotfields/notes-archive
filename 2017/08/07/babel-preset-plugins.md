# Babel Preset Plugins
This is a list of all the plugins included with various Babel presets.

Alternatively, you can use `babel-preset-env` and supply the browsers you wish to target. Note that `babel-preset-env` does not include any `stage` plugins.

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

ES6 features like Promises, generator functions, `Object.assign`, or `Array.prototype.includes` can by polyfilled by including `babel-polyfill` in your main entry file (`index.js`).

Experimental features commonly used in React such as class property initializers and decorators will require a plugin to work in any modern browser.

| Babel Transform           | Reference                                                                                            | Chrome | Firefox | Opera | Edge       | Safari     |
|---------------------------|------------------------------------------------------------------------------------------------------|--------|---------|-------|------------|------------|
| `arrow-functions`         | http://caniuse.com/#feat=arrow-functions                                                             | < 45   | < 22    | < 32  | < 12       | < 10       |
| `block-scoping`           | http://caniuse.com/#feat=const                                                                       | < 49   | < 36    | < 36  | < 12       | < 10       |
| `classes`                 | http://caniuse.com/#feat=es6-class                                                                   | < 49   | < 45    | < 36  | < 12       | < 9        |
| `computed-properties`     | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer       | < 44   | < 34    | < 34  | < 12       | < 7.1      |
| `destructuring`           | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment | < 49   | < 34    | < 36  | < 12       | < 10       |
| `for-of`                  | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of                | < 51   | < 13    | < 25  | < 12       | < 7.1      |
| `parameters`              | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters       | < 49   | < 15    | < 45  | < 12       | < 10       |
| `shorthand-properties`    | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer       | < 42   | < 34    | < 34  | < 12       | < 9        |
| `spread`                  | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator          | < 49   | < 34    | < 37  | < 15       | < 10       |
| `template-literals`       | http://caniuse.com/#feat=template-literals                                                           | < 41   | < 34    | < 29  | < 13       | < 9.1      |
| `regenerator`             | http://caniuse.com/#feat=es6-generators                                                              | < 39   | < 26    | < 26  | < 13       | < 10       |
| `exponentiation-operator` | https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Arithmetic_Operators     | < 52   | < 52    | < 39  | < 14       | < 10.1     |
| `object-rest-spread`      | http://kangax.github.io/compat-table/esnext/#test-object_rest/spread_properties                      | < 60   | < 55    | < 47  | No support | No support |
| `async-to-generator`      | http://caniuse.com/#feat=async-functions                                                             | < 55   | < 52    | < 42  | < 15       | < 10.1     |
