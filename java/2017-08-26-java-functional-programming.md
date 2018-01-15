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

Microsoft has a chart on the C# docs comparing the key differences:

| Characteristic     | Imperative                                                       | Functional                                                        |
|--------------------|------------------------------------------------------------------|-------------------------------------------------------------------|
| Programmer focus   | How to perform tasks (algorithms) and how to track state changes | What information is desired and what transformations are required |
| State changes      | Important                                                        | Non-existent                                                      |
| Order of execution | Important                                                        | Not important                                                     |
| Control flow       | Loops, conditionals, and methods                                 | Functions and recursion                                           |
| Primary unit       | Classes and instances                                            | Functions and data collections                                    |

### Pure Functions
Given the same input, a pure function will always produce the same output. This is known as
referential transparency.

Pure functions must not produce any side effects. This is known as idempotence.

Pure functions can be cached. This is known as memoization.

### Higher Order Functions
Functions can be passed both values and functions, and in the same way return either a value or a
function. A function that accepts one or more functions as arguments and/or returns a function is a
higher-order function.

### Functional Composition
Composition is the act of combining simple functions to build more complicated ones. The result of
each function if passed as the argument to the next.

The Function interface has two instance methods - `andThen` and `compose` to facilitate functional
composition.

`x.andThen(y)` is equivalent to `y.compose(x)`.

### Lambdas
A lambda expression represents an anonymous function. It is comprised of a set of parameters, the
lambda operator (`->`), and a function body.

When there is a single statement curly braces are not mandatory and the return type of the
anonymous function is the same as that of the body expression.

Read more [here](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html).

### Method Reference
A method reference is the shorthand syntax for a lambda expression that executes just one method.

There are four kinds of method references:

| Kind                                                                        | Example                                |
|-----------------------------------------------------------------------------|----------------------------------------|
| Reference to a static method                                                | `ContainingClass::staticMethodName`    |
| Reference to an instance method of a particular object                      | `containingObject::instanceMethodName` |
| Reference to an instance method of an arbitrary object of a particular type | `ContainingType::methodName`           |
| Reference to a constructor                                                  | `ClassName::new`                       |

### Functional Interface
A functional interface is an interface that contains only one abstract method. A functional
interface defines the target type of a lambda expression.

A functional interface is sometimes referred to as a Single Abstract Method (SAM) type.

### Stream
A stream is a sequence of elements. In contrast, a list is a collection of elements. Streams carry
elements through a sequence of operations known as a pipeline.

The pipeline operations are known as Intermediate Operations, and the final operation is known as
the Terminal Operation.

Streams are lazy - they don't do anything until instructed.

### Optionals
The Optional classes (`Optional`, `OptionalDouble`, `OptionalInt`, and `OptionalLong`) offer a way
to handle situations in which a value may or may not be present.

Optionals provide a better way to deal with potential null values and avoid `NullPointerException`s.

An Optional can contain a value or be empty. Optionals provide methods to work with their values,
and set a default value if no value is present.

You can call `isPresent()` to determine if a value is present and `get()` to obtain it. You should
always call `isPresent` before calling `get` to avoid throwing a `NoSuchElementException`.
