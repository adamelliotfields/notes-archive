# Java Functional Programming

### Imperative vs Declarative
With Imperative Programming, your code explains step-by-step what you want to happen:

```java
int[] integers = {1, 2, 3, 4};

// We are explaining how we want to iterate over the array
for (int i = 0; i < integers.length; i++) {
  // We are explaining how to filter the even numbers
  if (integers[i] % 2 == 0) {
    System.out.println(integers[i]);
  }
}
```

With Declarative programming, your code describes the result without explaining how:

```java
int[] integers = {1, 2, 3, 4};

Arrays
  .stream(integers)
  // We don't explain how the filter algorithm works
  .filter(integer -> integer % 2 == 0)
  // We don't explain how the forEach loop works
  .forEach(System.out::println);
```

### Pure Functions
Given the same input, a pure function will always produce the same output. This is known as
referential transparency.

Pure functions must not produce any side effects. This is known as idempotence.

Pure functions can be cached. This is known as memoization.

### Higher Order Functions

### Functional Composition

### Closures

### Lazy Evaluation

### Lambdas
A lambda expression represents an anonymous function. It is comprised of a set of parameters, the
lambda operator (`->`), and a function body.

When there is a single statement curly brackets are not mandatory and the return type of the
anonymous function is the same as that of the body expression.

Read more [here](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html).

### Method Reference
A method reference is the shorthand syntax for a lambda expression that executes just one method.

### Function Interface

### Iterable Interface

### Optionals
An optional is a monad.

### Consumer
A function that accepts something, but returns nothing.

### Supplier
A function that accepts nothing, but returns something.

### Predicate
A function that accepts a parameter and returns a boolean.

### Stream
A stream is a sequence of elements. In contrast, a list is a collection of elements. Streams carry
elements through a sequence of operations known as a pipeline.

The pipeline operations are known as Intermediate Operations, and the final operation is known as
the Terminal Operation.

Streams are lazy - they don't do anything until instructed.

### Range

### `forEach`
`forEach` is an instance method on any class that implements the `Iterable` interface.

`forEach` performs the given action for each element of the Iterable until all elements have been
processed or the action throws an exception.

Read more [here](https://docs.oracle.com/javase/8/docs/technotes/guides/language/foreach.html).

### `stream`

### `filter`

### `limit`

### `collect`

### `map`

### `flatMap`

### `reduce`

### `distinct`

### `sorted`
