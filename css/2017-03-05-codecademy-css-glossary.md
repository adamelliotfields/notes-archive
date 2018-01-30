# Codecademy CSS Glossary
> :calendar: *March 5, 2017*

### Comments
Comments in CSS are signified by a forward-slash and asterisk.

*Example:*

```css
/* This is a single line comment */
```

*Example:*

```css
/* This 
is a multi-line
comment */
```

### Properties
Properties are defined within selectors by defining a property and a value. They are separated with a colon and delineated with a semi-colon.

*Syntax:*

```css
selector {
  property: value;
}
```

*Example:*

```css
h1 {
  color: blue;
}
```

*Read more:*
 - [http://www.htmldog.com/reference/cssproperties/](http://www.htmldog.com/reference/cssproperties/)

### Defining many properties
Each CSS rule can have as many properties as you like. Each of them applies to the elements that the selector applies to.

*Example:*

```css
h1 {
  font-size: 24px;
  font-weight: bold;
  border: 1px solid black;
  color: pink;
}
/* This will make all <h1> headers big, bold, pink, and inside of a thin black rectangle! */
```

### Padding
The padding is the spacing between the content and the border (edge of the element.). We can adjust this value with CSS to move the border closer to or farther from the content. Here, the div with id 'box' will get 10px of padding all around it.

*Example:*

```css
#box {
  padding: 10px;
}
```

### Margin
The margin is the space around the element. The larger the margin, the more space between our element and the elements around it. We can adjust the margin to move our HTML elements closer to or farther from each other. Here, the div with id 'box' will get 10px of margin above and below it, and 5px of margin to the left and right.

*Example:*

```css
#box {
  margin: 10px 5px 10px 5px;
}
```

### `font-family`
The `font-family` property sets the font of an HTML element's text.

*Syntax:*

```css
p {
  font-family: Arial, Helvetica, sans-serif;
}
```

### Selectors
What are selectors?

Selectors are used in CSS to select the parts of the HTML that are being styled. You can use several different methods for selecting an element.

*Syntax:*

```css
selector {
  rules;
  rules;
  rules;
}
```

*Read more:*

 - [https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Getting_started/)

### Class name selectors
You can also select HTML elements by their Class name. Unlike ID selectors, Class selectors select all elements with a matching class.

*Example:*

```css
a.link {
  font-size: 12px;
}

/* HTML Selected: <a href="http://google.com" class="link">, 
<a href="http://codecademy.com" class="link jumbo"> */
```

*Example:*

```css
.jumbo {
  text-size: 1000px;
}

/* HTML Selected: <a href="http://codecademy.com" class="link jumbo">,
<span class="jumbo"> */
```

### Element selectors
You are able to select HTML elements first by simply using the name of the element.

*Example:*

```css
body {
  background-color: #333;
}
```

*Example:*

```css
h1 {
  color: blue;
}
```

*Example:*

```css
a {
  text-underline: none;
}
```

### ID selectors
ID selectors are used to select only a single item on a page. Like the term ("identification") indicates, ID selectors will ONLY select the first element with a matching ID.

*Example:*

```css
#thatThingINeededToStyle {
  color: blue;
  font-size: 24px;
}

/* HTML Selected: <span id="thatThingINeededToStyle"> */
```

*Example:*

```css
a#codecademy {
  color: purple;
}

/* HTML Selected: <a href="http://codecademy.com" id="codecademy"> */
```

### Attribute selectors
HTML elements are also able to be selected by their attributes.

*Example:*

```css
a[href="http://codecademy.com"] {
  color: purple;
}

/* HTML Selected: <a href="http://codecademy.com"> */
```

*Example:*

```css
input[type="text"] {
  width: 100px;
}

/* HTML Selected: <input type="text"> */
```

*Example:*

```css
input[required] {
  border: 1px red solid;
}

/* HTML Selected: <input type="text" required> */
```

*Read more:*
 - [http://dev.opera.com/articles/view/27-css-basics/#attribute](http://dev.opera.com/articles/view/27-css-basics/#attribute)

### Child selectors
You can also use multiple selectors to get the exact elements you want, by using parental nesting. By using the "greater-than" symbol (>), you can select only the direct children of an element, going down only one level.

*Example:*

```css
ul > li {
  display: inline-block
}

/* Selects only the first-level list items in all unordered lists in the HTML */
```

*Example:*

```css
ul a {
  text-underline: none;
}

/* Selects all anchors which have an unordered list their ancestry */
```

*Example:*

```css
ul + span {
  display: inline;
}

/* Selects only spans that directly follow an unordered list */
```

*Example:*

```css
a ~ h1 {
  color: blue;
}

/* Selects all h1 elements that are in the general vicinity of an anchor */
```

*Read more:*
 - [https://developer.mozilla.org/en-US/docs/Web/CSS/Descendant_selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Descendant_selectors)

### Universal selector
The universal selector (*) may be used to select all the elements in a particular range. Be aware that the universal selector is the most performance taxing selector, and should be used sparingly.

*Example:*

```css
* {
  background-color: blue;
}

/* Selects ALL HTML elements in the page */
```

*Example:*

```css
body * {
  color: red;
}

/* Selects ALL children of the body */
```

*Example:*

```css
div > * {
  color: red;
}

/* Selects ALL first-level children of all divs on the page */
```

*Read more:*
 - [https://developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/Universal_selectors)
 - [http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/)
 - [http://dev.opera.com/articles/view/27-css-basics/#universal](http://dev.opera.com/articles/view/27-css-basics/#universal)

### Pseudo class selectors
Pseudo Selectors can be used to narrow down a selection with certain rules.

*Example:*

```css
li:first-child {
  color: red;
}

/* 
    This selects only <li> elements that have no elements before them
    <ul>
      <li>Selected; will be red</li>
      <li>Not selected</li>
      <li>Not selected</li>
    </ul>
*/

li:last-child {
  color: red;
}

/* This does the opposite; only the last <li> will be red. */
```

*Example:*

```css
a:hover {
  text-decoration: underline;
}

/* Will underline all links when the user puts their mouse over them */

a:active {
  font-weight: bold;
}

/* Will make all links bold while the user is clicking on them. */
```

*Read more:*
 - [https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)
 - [http://dev.opera.com/articles/view/27-css-basics/#pseudoclasses](http://dev.opera.com/articles/view/27-css-basics/#pseudoclasses)
