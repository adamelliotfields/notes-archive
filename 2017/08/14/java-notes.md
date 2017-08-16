# Java Notes

### Primitive Data Types

**`int`**
 - short for integer, which are all positive/negative numbers including zero
 - values can be between -2,147,483,648 and 2,147,483,647
 - in Java 8, an unsigned int can be between 0 and 2^32 -1

**`boolean`**
 - a data type that can be either `true` or `false`

**`char`**
 - represents a single character
 - all values must be enclosed in single-quotes

**`byte`**
 - an 8-bit signed [two's-complement](https://en.wikipedia.org/wiki/Two%27s_complement) integer
 - values can be between -128 and 127

**`short`**
 - a 16-bit signed two's-complement integer
 - values can be between -32,768 and 32,767

**`long`**
 - a 64-bit two's-complement integer
 - a signed long can be betwee -2^63 and 2^63 - 1
 - in Java 8, an unsigned long can be between 0 and 2^64 - 1

**`float`**
 - a single-precision 32-bit IEEE 754 floating point

**`double`**
 - a double-precision 64-bit IEEE 754 floating point

### Variables
In Java, all variables must have a specified data type.

```java
int myNumber = 42;
```

### Whitespace
Java ignores whitespace. The Google style guide recommends block indentation of 2 spaces, and indent
continuation of 4 spaces (when line-wrapping). Column width should be 100.

### Comments

```java
// single-line comment

/* multi-line
   comment */
```

### Math

```java
int sum = 34 + 113;
int difference = 91 - 205;
int product = 2 * 8; 
int quotient = 45 / 3;
int remainder = 3 % 2;
```

### Relational Operators

```java
<  // less than
<= // less than or equal to
>  // greater than
>= // greater than or equal to
```

### Equality Operators
Because there is no implicit type coercion in Java, there is no need for strict equality.

```java
== // equal to
!= // not equal to
```

### Conditional Operators

```java
&& // and
|| // or
```

### Unary Operators

```java
+  // indicates positive value
-  // indicates negative value
++ // increment by 1
-- // decrement by 1
!  // inverts the value of a boolean
```

Read more about operators and precedence
[here](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/operators.html).

### If Statement

```java
if (condition) {
  // do something
} else if (anotherCondition) {
  // do something else
} else {
  // do this instead
}
```

### Ternary Statement

```java
char gameResult = (pointsScored > 20) ? 'W' : 'L';
```

### Switch Statement

```java
int restaurantRating = 3;

switch (restaurantRating) {
  case 1: System.out.println("This restaurant is not my favorite.");
    break;

  case 2: System.out.println("This restaurant is good.");
    break;

  case 3: System.out.println("This restaurant is fantastic!");
    break;

  default: System.out.println("I've never dined at this restaurant.");
    break;
}
```

### For Loop

```java
for (int i = 0; i < 5; i++) {
  System.out.println("The counter value is: " + i);
}
```

### While Loop and Do While Loop

```java
while (condition) {
  // do something
}

do {
  // do something at least once
} while (condition)
```

### Array
An array is a container for holding a fixed number of values of a single type. The length of the
array is established when the array is created.

```java
// declare an array of integers
int[] myArray;

// allocate memory for 10 integers
myArray = new int[10];

// initialize the element at index 0
myArray[0] = 100;

// shorthand syntax for declaring an array
int[] myArray = {
  100, 200, 300
};
```

### `ArrayList`
ArrayList is a built-in Java class that stores a list of data of the specified type.

The Java ArrayList is similar to JavaScript's `Set`.

```java
// import the ArrayList class
import java.util.ArrayList;

// create a new programmingLanguages object
ArrayList<String> programmingLanguages = new ArrayList<String>();

// add a String to programming languages
programmingLanguages.add("JavaScript");

// insert a new value at index 0
programmingLanguages.add(0, "HTML");

// access the value at index 0
programmingLanguages.get(0);

// iterate over the list and print each value using a for each loop
for (String language : programmingLanguages) {
  System.out.println(language);
}
```

### `HashMap`
HashMap is another built-in Java class containing a set of key-value pairs.

The Java HashMap is similar to JavaScript's `Map`.

```java
import java.util.HashMap;

HashMap<String, String> react = new HashMap<String, String>();

react.put("currentVersion", "15.6.1");
react.put("githubStars", "73,000");

// HashMap's keySet method returns a list of keys that can be iterated over
for (String key : react.keySet()) {
  System.out.println(key + ":" react.get(key));
}
```

### Classes
Classes are sets of instructions that defined how an object should behave.

Class constructors allow you create instances of the class and set initial information. Class
constructors are given the same name as the class. Class instances are objects.

Objects store their state in instance variables, and define their behavior in methods.

Instance variables are declared before the constructor and assigned within the constructor. Instance
variables should be private and only accessable via getter and setter methods. This is known as
*data encapsulation*.

Instance variables are *non-static fields* that are unique to each class instance; however, the
`static` keyword can be used to declare *class variables* or *static fields*. Class variables will
be the same in every instance.

The `main` method is a built-in method that is executed when the program is run. Not every class
needs a `main` method, as some classes are made solely to be used in other classes.

Class methods are declared after the constructor, and invoked within the `main` method. Variables
declared within a method are *local variables*.

Method parameters are variables that provide extra information to a method. Local variables and
parameters are only referred to as "variables" and never as "fields".

The `void` keyword indicates that no value should be returned by the method. If the method does
return a value, it must be specified using the appropraite data type keyword instead.

```java
class Person {
  String name;
  int age;

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  public void speak(String message) {
    System.out.println(message);
  }

  public int getAge() {
    return age;
  }

  public static void main(String[] args) {
    Person adam = new Person("Adam", 33);

    adam.speak("Hello!");

    int adamAge = adam.getAge();
  }
}
```

### Access Level Modifiers
Access level modifiers determine whether other classes can use a particular field or invoke a
particular method. There are two levels of access control:
 - top level: `public` or package-private (no modifier)
 - member level: `public`, `private`, `protected`, or package-private

### Inheritance
Inheritance is used to share behavior between classes. This enables code reuse.

```java
class WebDeveloper extends Person {
  public static void main(String[] args) {
    String[] programmingLanguages = {
      "HTML", "CSS", "JavaScript"
    }
  }
}
```

### Interfaces
An interface is an *abstract* class that contains only method definations, but not implementations.

Interfaces are *implemented*, while classes are *extended*. Interfaces are useful in that a sub
class can only extend one super class; however, a class can implement multiple interfaces.

Implementing an interface forms a contract in a way that the class must define all methods in the
interface in order to be compiled.

For example, if a Human eats and drinks, then a Person implementing the Human
interface must also eat and drink in order to be defined as a Human.

```java
interface Human {
  void eat(boolean value);
  void drink(int value);
}

class Person implements Human {
  int hungry = true;
  int thirsty = true;

  public void eat(boolean value) {
    hungry = value;
  }

  public void drink(boolean value) {
    thirsty = value;
  }
}
```

### Fizz Buzz

```java
public class FizzBuzz {
  public static void main(String[] args) {
    for (int i = 1; i <= 100; i++) {
      if (i % (3 * 5) == 0) {
        System.out.println("FizzBuzz")
      } else if (i % 3 == 0) {
        System.out.println("Fizz");
      } else if (i % 5 == 0) {
        System.out.println("Buzz");
      } else {
        System.out.println(i);
      }
    }
  }
}
```
