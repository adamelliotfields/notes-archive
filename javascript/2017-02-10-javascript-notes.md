# JavaScript Notes
> :calendar: *February 10, 2017*

### What can we use JavaScript for?
 - Make websites respond to user interaction.
 - Build apps and games (e.g. blackjack).
 - Access information on the Internet (e.g. find out the top trending words on Twitter by topic).
 - Organize and present data (e.g. automate spreadsheet work; data visualization).

### Comments

```javascript
// this is a comment
```

### Numbers and Strings
 - Numbers are quantities. You can do math with them.
 - Strings are sequences of characters surrounded by quotes like letters, spaces, punctuation, and even numbers.

### Booleans
 - A boolean is either `true` or `false`.

### Console
 - `console.log()` will take whatever is passed in and log it to the console.
 - This is commonly called printing out.

### Comparison Operators

```javascript
>   // Greater than
<   // Less than
<=  // Less than or equal to
>=  // Greater than or equal to
=== // Equal to
!== // Not equal to
```

### Logical Operators

```javascript
&& // and
|| // or
!  // not
```

### Conditional Statements
 - An `if` statement is made up of the `if` keyword and a pair of curly braces.
 - If the condition is true, the code inside the braces will run.
 - The code after the `else` keyword will run if the `if` condition is false.

```javascript
if (myName.length >= 7) {
  console.log('You have a long name!');
} else {
  console.log('You have a short name!');
}
```

### `switch()`
 - `switch()` allows you to preset a number of options (called `case`s), then check an expression to see if it matches any of them.
 - If there is a match, the program will perform the action for the matching `case`.
 - If there is no match, the program can execute a `default` option.
 - Make sure you include a `break` after each case, otherwise it will run the default code even if there is a match.

```javascript
const game = prompt('What\'s your favorite video game?');

switch (game) {
  case 'World of Warcraft':
    console.log('Me too!');
  break;

  case 'Call of Duty':
    console.log('My favorite FPS!');
  break;

  case 'Fallout 4':
    console.log('I think it\'s boring.')
  break;

  default:
    console.log('I haven\'t played that yet!');
}
```

### Ternary Operator
A ternary operator is compact way of writing a conditional statement. It is called a "ternary" because it involves 3 components: a boolean, an expression if true, and an expression if false.

```javascript
const isTrue = true;

isTrue ? console.log('yes') : console.log('no');
```

It is common to use a ternary as an expression and store the value in a variable to be used later.

```javascript
const yesOrNo = isTrue ? 'yes' : 'no';

console.log(yesOrNo);
```

### Short Circuit
As logical expressions are evaluated left to right, they are tested for possible "short-circuit" evaluation using the following rules:
 - `false && (anything)` is short-circuit evaluated to false.
 -`true || (anything)` is short-circuit evaluated to true.

The function:

```javascript
const isAdult = (age) => {
  if (age && age >= 18) {
    return true;
  } else {
    return false;
  }
}
```

Is the same as:

```javascript
const isAdult = (age) => {
  return age && age >= 18;
}
```

### Math

```javascript
'()' // control order of operations
'*'  // multiplication
'/'  //  division
'-'  // subtraction
'+'  // addition
'%'  // modulo
```

### Substrings
 - The `.substring()` function takes in 2 arguments (the beginning and end) and returns a substring.

```javascript
'hello'.substring(0, 2);
```

### Variables
 - Once you delcare a variable, you can call its value by typing the variable name.
 - A variable's value can be changed by reassigning a new value to an existing variable name.

### Functions
 - A function takes in inputs, does something with them, and produces an output.
 - Parameters are placeholders that we give specific value to when we call the function (an argument).
 - Functions can have multiple parameters, but remember to give multiple arguments when calling the function.

```javascript
const sayHello = (name) => {
  console.log('Hello', name);
}

sayHello('Adam');
```

### `return`
 - The `return` keyword gives the programmer back the value that comes out of the function.

### Scope
 - Variables defined outside a function are accessible anywhere. These are global variables.
 - Variables defined inside a function are only accessible within the function. These are local variables.

### For Loops
 - Every `for` loop makes use of a counting variable (an iterator).

```javascript
let i;
for (i = 1; i < 10; i++) {
  // do something
}
```

### Arrays
 - Arrays store lists of data.
 - Can store different data types in the same array (heterogeneous array).
 - Arrays are ordered, so each piece of data is fixed in a specific position (the index).
 - Arrays have a property in common with strings: they can both use `.length`.

```javascript
const cities = ['Boston', 'NYC', 'San Francisco'];

let i;
for (i = 0; i < cities.length; i++) {
  console.log('I would like to visit', cities[i]);
}
```

### Multidimensional Arrays
 - You can make a 2D array nesting arrays one-layer deep.
 - This array is two-dimensional because it contains 2 rows that contain 2 items each.

```javascript
const twoDimensional = [
  [1, 1],
  [1, 1]
];
```

If your array is not symetrical, it is a jagged array.

```javascript
const jagged = [
  [1,2,3],
  [4,5]
];
```

### While Loops
 - In situations where you don't know in advance when to stop looping, you can use a `while` loop.
 - As long as the loop condition evaluates to `true`, the loop will continue to run.
 - You need to include a way for the loop to eventualy evaluate to `false`, otherwise the loop will continue to run forever.

```javascript
let number = 1;

while (number < 3) {
  console.log('I\'m looping!');
  number ++;
}
```

### Do-While Loops
 - When you want to make sure your loops runs at least once (even if the condition is `false`), use the do-while loop.

```javascript
let number = 1;

do {
  console.log('I\'m looping!');
}
while (number < 1);
```

### Objects
 - Objects are a comination of key-value pairs (like arrays), only their keys don't have to be index numbers.
 - Objects can be created either using object literal notation, or with an object constructor.
 - Objects can have properties or methods (functions).

```javascript
const me = {
  name: 'Adam',
  age: 32
}
```

**OR**

```javascript
const me = new Object();
me.name = 'Adam';
me.age = 32;
```

### `this`
 - The keyword "this" will refer to whichever object called that method.

```javascript
// Here we define our method using "this"
function setAge (newAge) {
  this.age = newAge;
}

// Now we make the me Object
const me = new Object();

// When we call me.setAge(newAge), this.age will refer to me.age
me.setAge = setAge;
```

### Custom Constructors

```javascript
// "this" defines the name and age properties and sets them equal to the parameters given
function Person (name,age) {
  this.name = name;
  this.age = age;
}

// Make bob and susan using the constructor
const bob = new Person('Bob Smith', 30);
const susan = new Person('Susan Jordan', 25);
```

### Literal Methods

```javascript
const james = {
  job: 'programmer',
  married: false,
  speak: (feeling) => {
    console.log('Hello, I am feeling', feeling);
  }
};

james.speak('great');
```

### Constructor Methods

```javascript
function Person (job, married) {
  this.job = job;
  this.married = married;

  // add a speak() method to Person
  this.speak = () => {
    console.log('Hello!');
  }
}

const user = new Person('Student', false);

user.speak();
```

### For-In Loops

```javascript
const nyc = {
  fullName: 'New York City',
  mayor: 'Bill de Blasio',
  population: 8000000,
  boroughs: 5
};

// write a for-in loop to print nyc's keys
for (let key in nyc) {
  console.log(key);
}

// write a for-in loop to print nyc's values
for (let value in nyc) {
  console.log(nyc[value]);
}
```

### `typeof`

```javascript
const languages = {
  english: 'Hello!',
  french: 'Bonjour!',
  notALanguage: 4,
  spanish: 'Hola!'
};

// print hello in the 3 different languages
for (let value in languages) {
  if (typeof languages[value] === 'string') {
    console.log(languages[value]);
  }
}
```

### `hasOwnProperty()`

```javascript
const suitcase = {
  shirt: 'Hawaiian'
};

// Check to see if suitcase has the shorts property and print its value
if (suitcase.hasOwnProperty('shorts')) {
  console.log(suitcase.shorts);

// If suitcase.shorts doesn't exist, create it and give it a value of "Khaki" and print it
} else {
  suitcase.shorts = 'Khaki';
  console.log(suitcase.shorts);
}
```

### Prototype

```javascript
// Define the Dog Class with the property breed
function Dog (breed) {
  this.breed = breed;
}

// Make a new Dog Object, "buddy", and make buddy a "Golden Retriever"
const buddy = new Dog('Golden Retriever');

// Add the bark method to the Dog class using Prototype
Dog.prototype.bark = () => {
  console.log('Woof');
}

// Make buddy bark
buddy.bark();
```

### Prototypal Inheritance

```javascript
// Define the Penguin class that takes in the name parameter and always has 2 legs
function Animal (name, numLegs) {
  this.name = name;
  this.numLegs = 2;
}

// Define the Emperor class, which only takes in the "name" parameter
function Penguin (name) {
  this.name = name;
}

// Set its prototype to be a new instance of Penguin which will inherit numLegs property
Emperor.prototype = new Penguin();
```

### Private Variables and Methods

```javascript
function Person (name, age) {
  this.age = name;
  this.age = age;

  // Create a private variable accountBalance
  const accountBalance = '$100,000.00';

  // Create a private method to retrieve the private variable accountBalance
  const returnBalance = () => accountBalance;

  // Create a public method to return the private method returnBalance
  // Return the method itself and not the result of calling the method (not returnBalance())
  this.returnPrivateBalance = () => returnBalance;
}

const adam = new Person('Adam', 32);

const getAdamBalance = adam.returnPrivateBalance();

// Because returnPrivateBalance returns a method, call that method
const adamBalance = getAdamBalance();

console.log(adamBalance);
```

### Sort
You can use the method `sort()` to easily sort the values in an array alphabetically or numerically.

Note that `sort()` **DOES** mutate the original array, while also returning it.

```javascript
const arr = [3, 1, 4, 2];

arr.sort();

// [1, 2, 3, 4]
```

### Reverse
You can use the `reverse()` method to reverse the elements of an array.

`reverse()` is another array method that alters the array in place, but it also returns the reversed array.

```javascript
const arr = [1, 2, 3, 4];

arr.reverse();

// [4, 3, 2, 1]
```

### Concat
`concat()` can be used to merge the contents of two arrays into one.

`concat()` takes an array as an argument and returns a new array with the elements of this array concatenated onto the end.

```javascript
const arr1 = ['a', 'b', 'c'];
const arr2 = ['d', 'e', 'f'];

arr1.concat(arr2);

// ['a', 'b', 'c', 'd', 'e', 'f']
```

### Split
You can use the `split()` method to split a string into an array.

`split()` uses the argument you pass in as a delimiter to determine which points the string should be split at.

```javascript
const str = 'hello world';

str.split(' ');

// ['hello', 'world']

const str = 'hello';

str.split('');

// ['h', 'e', 'l', 'l', 'o']
```

### Join
We can use the `join()` method to join each element of an array into a string separated by whatever delimiter you provide as an argument.

```javascript
const arr ['hello', 'world'];

arr.join(' ');

// 'hello world'
```

### Map
The `map()` method will iterate through every elements of the array, creating a new array with values that have been modified by the callback function and return it.

`map()` is passed a callback function which takes the current value as an argument.

```javascript
const arr = [1, 2, 3, 4];

arr.map((item) => item * 2);

// [2, 4, 6, 8]
```

Using map and call to reverse a string:

```javascript
const str = '12345';
const arr = [];

arr
  .map
  .call(str, (item) => item)
  .reverse()
  .join('');

// '54321'
```

### Reduce
The array method `reduce()` is used to iterate through an array and condense it into one value.

To use `reduce()`, you pass in a callback function whose arguments are an accumulator and the current value.

```javascript
const arr = [1, 2, 3, 4];

arr.reduce((sum, item) => sum + item);

// 10
```

### Filter
The `filter()` method is used to iterate through an array and filter out elements where a given condition is not true.

`filter()` is passed a callback function which takes the current value as an argument.

```javascript
const arr = [1, 2, 3, 4];

arr.filter((item) => item > 2);

// [3, 4]
```

### Regular Expressions
Regular expressions are used to find words or patterns inside strings.

For example, if we wanted to find the word `"the"` in the string `"The dog chased the cat"`, we could use the following regular expression: `/the/gi`
 - `/` is the start of the regular expression
 - `the` is the pattern we want to match
 - `/` is the end of the regular expression
 - `g` means `global`, which causes the pattern to return all matches, not just the first one
 - `i` means that we want to ignore case when searching for a pattern

We can also use special selectors in regular expressions. One such selector is the `digit` selector `\d` which is used to retrieve one digit (numbers 0-9) in a string. Appending a plus sign (`+`) after the selector allows the regular expression to match one or more digits. 

In JavaScript, it is used like this: `/\d+/g`

We can also use selectors like `\s` to find whitespace in a string. The whitespace regular expression looks like this: `/\s/g`

You can invert any match by using the uppercase version of the selector. For example, `\S` will match anything that isn't whitespace.
