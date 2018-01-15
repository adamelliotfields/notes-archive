# ES2015 Notes

### [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let)
The `let` statement declares a block scope local variable, optionally initializing it to a value. 

`let` allows you to declare variables that are limited in scope to the block, statement, or expression on which it is used. This is unlike the `var` keyword, which defines a variable globally, or locally to an entire function regardless of block scope.

### [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)
`const`s are block-scoped, much like variables defined using the `let` statement. The value of a `const` cannot change through re-assignment, and it can't be redeclared.

This declaration creates a `const` that can be either global or local to the function in which it is declared. An initializer for a `const` is required; that is, you must specify its value in the same statement in which it's declared (which makes sense, given that it can't be changed later). 

The `const` declaration creates a read-only reference to a value. It does not mean the value it holds is immutable, just that the variable identifier cannot be reassigned. For instance, in case the content is an object, this means the object itself can still be altered.

### [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)
Template literals are string literals allowing embedded expressions. You can use multi-line strings and string interpolation features with them. They were called "template strings" in prior editions of the ES2015 specification.

Template literals are enclosed by the back-tick character instead of double or single quotes. Template literals can contain place holders. These are indicated by the Dollar sign and curly braces `${expression}`. The expressions in the place holders and the text between them get passed to a function. The default function just concatenates the parts into a single string.

If there is an expression preceding the template literal (tag here), the template string is called "tagged template literal". In that case, the tag expression (usually a function) gets called with the processed template literal, which you can then manipulate before outputting. To escape a back-tick in a template literal, put a backslash before the back-tick.

### [String.raw()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/raw)
The static `String.raw()` method is a tag function of template literals. It's used to get the raw string form of template strings (that is, the original, uninterpreted text).

### [String.prototype.startsWith()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/startsWith)
The `startsWith()` method determines whether a string begins with the characters of another string, returning `true` or `false` as appropriate.

### [String.prototype.endsWith()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/endsWith)
The `endsWith()` method determines whether a string ends with the characters of another string, returning `true` or `false` as appropriate.

### [String.prototype.includes()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/includes)
The `includes()` method determines whether one string may be found within another string, returning `true` or `false` as appropriate.

### [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
An arrow function expression has a shorter syntax than a function expression and does not bind its own `this`, arguments, `super`, or `new.target`. These function expressions are best suited for non-method functions, and they cannot be used as constructors.

### [Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
The `Promise` object is used for asynchronous computations. A `Promise` represents a value which may be available now, or in the future, or never.

### [Default Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)
Default function parameters allow formal parameters to be initialized with default values if no value or `undefined` is passed. 

In JavaScript, parameters of functions default to undefined. However, in some situations it might be useful to set a different default value. This is where default parameters can help.

In the past, the general strategy for setting defaults was to test parameter values in the body of the function and assign a value if they are undefined.

### [Rest Parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)
The rest parameter syntax allows us to represent an indefinite number of arguments as an array.

### [Spread Syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_operator)
The spread syntax allows an expression to be expanded in places where multiple arguments (for function calls) or multiple elements (for array literals) or multiple variables  (for destructuring assignment) are expected.

### [Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
The destructuring assignment syntax is a JavaScript expression that makes it possible to extract data from arrays or objects into distinct variables.

The object and array literal expressions provide an easy way to create ad hoc packages of data. The destructuring assignment uses similar syntax, but on the left-hand side of the assignment to define what elements to extract from the sourced variable.

### [Set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set)
The Set object lets you store unique values of any type, whether primitive values or object references.

If an iterable object is passed, all of its elements will be added to the new Set. If null is passed instead of iterable, it is treated as not passing iterable at all. 

Set objects are collections of values. You can iterate through the elements of a set in insertion order. A value in the Set may only occur once; it is unique in the Set's collection.

### [Map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map)
The Map object is a simple key/value map. Any value (both objects and primitive values) may be used as either a key or a value.

A Map object iterates its elements in insertion order — a for...of loop returns an array of [key, value] for each iteration.

It should be noted that a Map that is a map of an object, especially a dictionary of dictionaries, will only map to the object's insertion order -- which is random and not ordered.  

### [for...of](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/for...of)
The `for...of` statement creates a loop iterating over iterable objects (including Array, Map, Set, String, TypedArray, arguments object and so on), invoking a custom iteration hook with statements to be executed for the value of each distinct property.

### [Array.from()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
The `Array.from()` method creates a new Array instance from an array-like or iterable object.

Array.from() lets you create Arrays from array-like objects (objects with a length property and indexed elements) or iterable objects (objects where you can get its elements, such as Map and Set).

Array.from() has an optional parameter `mapFn`, which allows you to execute a map function on each element of the array (or subclass object) that is being created. More clearly, `Array.from(obj, mapFn, thisArg)` has the same result as `Array.from(obj).map(mapFn, thisArg)`, except that it does not create an intermediate array. This is especially important for certain array subclasses, like typed arrays, since the intermediate array would necessarily have values truncated to fit into the appropriate type.

The length property of the `from()` method is 1.

In ES2015, the class syntax allows for sub-classing of both built-in and user defined classes; as a result, static methods such as `Array.from` are "inherited" by subclasses of Array and create new instances of the subclass, not Array.

### [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
JavaScript classes introduced in ECMAScript 2015 are syntactical sugar over JavaScript's existing prototype-based inheritance. The class syntax is not introducing a new object-oriented inheritance model to JavaScript. JavaScript classes provide a much simpler and clearer syntax to create objects and deal with inheritance.

Classes are in fact "special functions", and just as you can define function expressions and function declarations, the class syntax has two components: class expressions and class declarations.

An important difference between function declarations and class declarations is that function declarations are hoisted and class declarations are not. You first need to declare your class and then access it, otherwise code like the following will throw a `ReferenceError`.

### [extends](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/extends)
The `extends` keyword is used in class declarations or class expressions to create a class which is a child of another class.

The `extends` keyword can be used to subclass custom classes as well as built-in objects.

The `.prototype` of the extension must be an Object or null.

### [static](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static)
The `static` keyword defines a static method for a class.

Static method calls are made directly on the class and are not callable on instances of the class. Static methods are often used to create utility functions.

In order to call a static method within another static method of the same class, you can use the `this` keyword.

### [get](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)
The `get` syntax binds an object property to a function that will be called when that property is looked up.

Sometimes it is desirable to allow access to a property that returns a dynamically computed value, or you may want to reflect the status of an internal variable without requiring the use of explicit method calls. In JavaScript, this can be accomplished with the use of a getter. It is not possible to simultaneously have a getter bound to a property and have that property actually hold a value, although it is possible to use a getter and a setter in conjunction to create a type of pseudo-property.

### [set](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set)
The `set` syntax binds an object property to a function to be called when there is an attempt to set that property.

In JavaScript, a setter can be used to execute a function whenever a specified property is attempted to be changed. Setters are most often used in conjunction with getters to create a type of pseudo-property. It is not possible to simultaneously have a setter on a property that holds an actual value.
