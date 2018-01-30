# React Notes
> :calendar: *February 26, 2017*

React.js is a JavaScript library. It was developed by engineers at Facebook.

React is fast. Apps made in React can handle complex updates and still feel quick and responsive.

React is modular. Instead of writing large, dense files of code, you can write many smaller, reusable files. React's modularity can be a beautiful solution to JavaScript's maintainability problems.

React is scalable. Large programs that display a lot of changing data are where React performs best.

React is flexible. You can use React for interesting projects that have nothing to do with making a web app. People are still figuring out React's potential. There's room to explore.

### JSX
JSX is a syntax extension for JavaScript. It was written to be used with React. JSX code looks a lot like HTML.

If a JavaScript file contains JSX code, then that file will have to be compiled. That means that before the file reaches a web browser, a JSX compiler will translate any JSX into regular JavaScript.

JSX elements are treated as JavaScript expressions. They can go anywhere that JavaScript expressions can go. You can nest JSX elements inside of other JSX elements, just like in HTML. If a JSX expression takes up more than one line, then you should wrap the multi-line JSX expression in parentheses.

JSX elements can have attributes, just like HTML elements can. A JSX attribute is written using HTML-like syntax: a name, followed by an equals sign, followed by a value. The value should be wrapped in quotes.

A JSX expression must have exactly one outermost element. The first opening tag and the final closing tag of a JSX expression must belong to the same JSX element. If you notice that a JSX expression has multiple outer elements, the solution is usually simple: wrap the JSX expression in a `<div></div>`.

### Rendering JSX
`ReactDOM` is the name of a JavaScript library. This library contains several React-specific methods, all of which deal with the DOM in some way or another.

`ReactDOM.render()` is the most common way to render JSX. It takes a JSX expression, creates a corresponding tree of DOM nodes, and adds that tree to the DOM. `ReactDOM.render()` takes two arguments: the JSX to render, and the HTML element to append to.

`ReactDOM.render()`'s first argument should evaluate to a JSX expression, it doesn't have to literally be a JSX expression. The first argument could also be a variable, so long as that variable evaluates to a JSX expression.

```javascript
import React from 'react';
import { render } from 'react-dom';

render(<h1>Render me!</h1>, document.getElementById('root'));
```

### Virtual DOM
`ReactDOM.render()` only updates DOM elements that have changed. If you render the exact same thing twice in a row, the second render will do nothing.

In React, for every DOM object, there is a corresponding "virtual DOM object." A virtual DOM object is a representation of a DOM object, like a lightweight copy. A virtual DOM object has the same properties as a real DOM object, but it lacks the real thing's power to directly change what's on the screen.

Manipulating the DOM is slow. Manipulating the virtual DOM is much faster, because nothing gets drawn onscreen. When you render a JSX element, every single virtual DOM object gets updated. Once the virtual DOM has updated, React compares the virtual DOM with a virtual DOM snapshot that was taken right before the update.

By comparing the new virtual DOM with a pre-update version, React figures out exactly which virtual DOM objects have changed. This process is called "diffing." Once React knows which virtual DOM objects have changed, React updates those objects, and only those objects, on the real DOM.

### `className`
In JSX, you cannot use the word `class`; you have to use `className` instead. This is because JSX is transpiled into JavaScript and `class` is a reserved word in JavaScript. When JSX is rendered, `className` attributes are automatically rendered as `class` attributes.

### Self Closing Tags
Most HTML elements use two tags: an opening tag and a closing tag. However, some HTML elements such as `<img>` and `<input>` use only one tag. The tag that belongs to a single-tag element isn't an opening tag nor a closing tag; it's a self-closing tag.

When you write a self-closing tag in HTML, it is optional to include a forward-slash immediately before the final angle-bracket

In JSX, you have to include the slash. If you write a self-closing tag in JSX and forget the slash, you will raise an error.

### Embedding Expressions
You can embed any JavaScript expression in JSX by wrapping it in curly braces.

```javascript
const Div = () => (
  <div>
    <p>{2 + 3}</p>
  </div>
);
```

### Attribute Variables
When writing JSX, it's common to use variables to set attributes. Object properties are also used to set attributes.

### Event Listeners
JSX elements can have event listeners, just like HTML elements. You can create an event listener by giving a JSX element a special attribute. An event listener attribute's value should be a function.

### Ternary Operators
The ternary operator is used frequently in React. 

The ternary operator should be used only for assigning values conditionally and never as a shortcut for an if statement.

```javascript
// ternary
x ? y : z 

// conditional
if (x == true) {
  return y
} else {
  return z
}
```

### Double Ampersand
Like the ternary operator, `&&` is frequently used in React applications.

```javascript
// generate a random number between 1 and 10
const randNum = Math.floor(Math.random() * 10) + 1;

// num is a div with a nested p
const Div = () => (
  <div>
    // return high if greater than 5
    {randNum > 5 && <p>High</p>}
    // return low if less than 5
    {randNum < 5 && <p>Low</p>}
  </div>
);
```

### Array.map()
`.map()` is also used frequently in React. The `.map()` method creates a new array with the results of calling a provided function on every element in the array.

```javascript
// create an array of strings
const strings = ['Home', 'Projects', 'Bio'];

//return a list item for each item in the array
const listItems = strings.map((string, index) => <li key={index}>{string}</li>);

const List = () => (
  <ul>
    {listItems}
  </ul>
);

// render to the DOM
render(<List />, document.getElementById('nav'));
```

### Keys
When you make a list in JSX, sometimes your list will need to include something called `key`s.

A `key` is a JSX attribute. The attribute's name is `key`. The attribute's value should be something unique, similar to an id attribute.

`key`s don't do anything that you can see. React uses them internally to keep track of lists. If you don't use `key`s when you're supposed to, React might accidentally scramble your list-items into the wrong order.
