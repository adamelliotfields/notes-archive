#jQuery Notes
jQuery is a library, or set of helpful add-ons, to the JavaScript programming language. jQuery allows JavaScript developers to "write less, do more".

### What is jQuery?
A library of useful methods to do things like:
 - Select elements
 - Manipulate elements
 - Create new elements
 - Add event listeners
 - Animate elements
 - Add effects
 - Make AJAX HTTP requests

### Why Use jQuery?
 - It was originally created to fix the "broken" DOM API.
 - It makes your code more concise and clear.
 - It's very easy to use.
 - It has great cross-browser support.
 - It simplifies AJAX calls.
 - It is only 30kb minified and gzipped.
 - It is widely used across the web.

### Why NOT Use jQuery?
 - The DOM API is no longer "broken".
 - It doesn't do anything you can't do in vanilla JavaScript.
 - It can prevent you from actually learning the JavaScript methods that jQuery provides shortcuts for.
 - It is a dependency that isn't needed, especially if you are importing the entire library for a single animation or effect.
 - It can be not as performant as vanilla JS if you use it incorrectly.
 - It is 267kb unminified and uncompressed (9000+ lines of code).
 - You can run into complications when using jQuery with a framework that uses a virtual DOM like React.

### Document Object Model (DOM)
 - An HTML document is structured according to the Document Object Model.
 - The DOM consists of every element on the page, laid out in a hierarchical way that reflects the way the HTML document is ordered. 

### `$(document).ready(function(){});`
 - `$()` says, "Hey, jQuery things are about to happen!"
 - Putting `document` between the parentheses tells us that we're about to work our magic on the HTML document itself.
 - `.ready()` is a function, or basic action, in jQuery. It says, "Hey, I'm going to do stuff as soon as the HTML document is ready!"
 - Whatever goes in `.ready()`'s parentheses is the jQuery event that occurs as soon as the HTML document is ready.
 - If we add our `function(){}` inside our `.ready()`, jQuery will run the code in our function as soon as the HTML document loads. 

### Functions
 - A function is made up of three parts:
   - the function keyword
   - any inputs that function takes (they go between the `()`s and are separated by commas if there are more than one)
   - whatever actions the function should perform (these go between the `{}`s). 

### Callback Functions
 - A callback is a function that gets passed to another function as an argument. 

### Variables
 - Variables are a place for us to store information for use at a later time.
 - Variables can hold any type of information you work with, so just think of them as containers.
 - The single `=` sign is used to assign values.
 - Conventionally, jQuery variables are prefaced with `$`.

### Selectors
 - Any CSS selector (i.e., classes and IDs) (in quotes) can be passed into `$()`.
 - Anything you can target in CSS can be modified by jQuery.

### `this`
 - The `this` keyword refers to the jQuery object you're currently doing something with.
 - If you use an event handler on an element, you can call the actual event that occurs on `$(this)`, and the event will only affect the element you're currently doing something with.

### DOM Traversal
 - `.each()` iterates over a set of matched elements and executes a function.
 - `.eq()` reduces the set of matched element to the one at the specified index.
 - `.filter()` reduces the set of matched elements to those that match the selector or pass the function's test.
 - `.first()` reduces the set of matched elements to the first in the set.
 - `.last()` reduces the set of matched elements to the last in the set.

### Inserting HTML Elements
 - `.append()` inserts the specifed element as the last child of the target element.
 - `.prepend()` inserts the specified element as the first child of the target element.
 - We can specify where in the DOM we insert an element with the `.before()` and `.after()` functions.
 - `.html()` can be used to get or set the contents of the first element match it finds.
 - `.text()` gets the combined text contents of each element in the set of matched elements or sets the text contents of the matched elements.

### DOM Removal
 - `.empty()` deletes an element's content and all its descendants.
 - `.remove()` deletes the element itself.
 - `.detach()` removes the elements from the DOM.

### Adding and Removing Classes
 - `.addClass()` adds a class to an element.
 - `.removeClass()` removes a class from an element.
 - `.toggleClass()` adds a class to an element or removes a class from an element.
 - `.hasClass()` determines whether any of the matched elements are assigned the given class.

### Changing Style
 - You can resize an element using `.height()` and `.width()`.
 - You can modify an elements CSS atributes using the `.css()` function.
   - `.css()` takes 2 arguments: the property and the value.
   - Alternatively, you can pass in a single JavaScript object comprising multiple property-value pairs.

### General Attributes
 - `.val()` gets the value of the first element in the set of matched elements or set the value of each matched element.
 - `.attr()` gets the value of an attribute for the first element in the set of matched elements, or sets one or more attributes for every matched element.
 - `.prop()` gets the value of a property for the first element in the set of matched elements, or sets one or more properties for every matched element. 
 - `.removeAttr()` removes an attribute from each element in the set of matched elements.
 - `.removeProp()` removes a property for the set of matched elements.

### jQuery Events
 - `.on()` behaves similarly to `addEventListener()` in vanilla JavaScript.
 - `.off()` behaves similarly to `removeEventListener()`.
 - You can also add jQuery event handlers such as `.click()`, `.hover()`, and `.focus()`.
 - `.on()` will add events to existing and future elements; specific handlers such as `.click()` only add events to existing elements.
 - The `.keypress()` event is triggered whenever a key on the keyboard is pressed.
 - Use `event.preventDefault()` to prevent the default event from occuring (i.e., page refresh on form submit).
 - Use `event.stopPropagation()` to prevent events from bubbling up the DOM.
 - Use `return false` within a jQuery event handler to prevent default and stop propagation.

### jQuery Effects
 - `.animate()` effect performs a custom animation of CSS properties.
 - `.hide()` effect will hide a matched element.
 - `.show()` will display a matched element.
 - `.fadeIn()` will fade in a matched element to opaque.
 - `.fadeOut()` will fade out a matched element to transparent.
 - `.slideUp()` will hide a matched element using a sliding motion.
 - `.slideDown()` will display the matched element with a sliding motion.
 - `.slideToggle()` will toggle `slideUp` and `slideDown` accordinly.

### jQuery UI
 - jQuery UI is a library that includes a number of additional animations.
 - jQuery UI uses the `.effect()` function to pass in a special effect.
 - jQuery UI includes a `.draggable()` function that can make any HTML element draggable.
 - You can make any DOM element resizable using the `.resizable()` function.
 - You can reorder the elements of a list using the `.sortable()` function.
 - You can make elements (like a list) selectable using the `.selectable()` function.
 - You can create a collapsable panel using the `.accordion()` function.

### jQuery Plugins
 - A good jQuery plugin should have good documentation and be actively maintained.
 - Make sure plugins are responsive and mobile friendly.
 - Good plugins should include a CSS file along with the main JavaScript file.
