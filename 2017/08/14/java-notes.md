# Java Notes

### Whitespace
Java ignores whitespace. The Google style guide recommends block indentation of 2 spaces, and indent
continuation of 4 spaces (when line-wrapping). Column width should be 100.

### Comments

```java
// single-line comment

/* multi-line
   comment */
```

### Primitive Data Types

**`int`**
 - short for integer, which are all positive/negative numbers including zero
 - values can be between -2,147,483,648 and 2,147,483,647
 - starting in Java 7, you can now add underscores to make numerical literals more readable
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
 - longs are suffixed with an uppercase L
 - in Java 8, an unsigned long can be between 0 and 2^64 - 1

**`float`**
 - a single-precision 32-bit IEEE 754 floating point
 - floats can be suffixed with a lowercase f

**`double`**
 - a double-precision 64-bit IEEE 754 floating point
 - doubles can be suffixed with a lowercase d

### Variables
In Java, all variables must have a specified data type.

```java
int myNumber = 42;
```

### Type Casting
Casting is the act of converting an object of one type to another.

There are two types of casts: downcasts and upcasts.

Downcasting takes an object and makes it more specific. Upcasting makes an object's type more broad.
You can only cast objects from the same type hierarchy.

```java
// downcasting
Object helloObject = "hello";
String helloString = (String) helloObject;

// upcasting
int integer = 42;
Number number = (Number) integer;
```

### Generic Types
A generic type is a reference type that has one or more type parameters. These type parameters are
later replaced with type arguments when instantiated.

When a generic class is instantiated with a type parameter, it becomes a *parameterized class* or
*parameterized type*.

Note that primitive types (e.g., `int`, `char`) cannot be passed as generic type parameters.

```java
// Generic method example
// <E> is a placeholder and E[] can be an array of any element type
public <E> void printArray(E[] inputArray) {
  for (E element : inputArray) {
    System.out.println(element);
  }
}

// Generic class example
// <T> is a placeholder for type
public class Thing<T> {
  private T t;

  public get() { return this.t; }
  public set(T t) { this.t = t; }

  public static void main(String[] args) {
    Thing<String> hello = new Thing<>();

    hello.set("hello");
  }
}

// The List interface is an example of a generic interface
public interface List<E> extends Collection<E> {
  // Java source code
}

List<String> arrayList = new ArrayList<>();
```

### Autoboxing and Unboxing
Autoboxing is the automatic conversion that the compiler makes between primitive types and their
corresponding wrapper classes. For example, converting an `int` to an `Integer`. The inverse
operation is known as unboxing (i.e., converting an `Integer` to an `int`).

```java
// We must use the Integer class because a generic type parameter cannot be a primitive type
List<Integer> list = new ArrayList<>();

// Even though list was declared with an Integer type parameter,
// autoboxing will convert the int i to an Integer when adding to the list
for (int i = 1; i < 5; i++) {
  list.add(i);
}

// The value is unboxed when assigned to a variable of a primitive type
int first = list.get(0);
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

Read more about operators and precedence [here](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/operators.html).

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

// array for each loop
for (int item : array) {
  System.out.println(item);
}
```

Note that arrays do not have functional methods like `map` and `forEach`. You'll need to convert the
array to a Collections object to access them.

```java
int[] primes = { 2, 3, 5, 7 };

List<Integer> primesList = Arrays.asList(primes);

primesList.forEach(System.out::println);
```

You can also use the `Arrays.stream()` static method to return a sequential Stream.

```java
int[] numbers = { 1, 2, 3, 4 };

Arrays.stream(numbers)
  .map(item -> item * 2)
  .forEach(System.out::println)
```

Note that the object returned from the Arrays methods inherits from AbstractList, not ArrayList, and
thus does not inherit all of the methods of ArrayList. You'll need to create a new ArrayList if you
need one.

Using a primitive array:

```java
int[] numbers = { 1, 2, 3, 4 };

// You cannot pass a primitive array to the ArrayList constructor
// You'll have to manually add the array items
List<Integer> numbersList = new ArrayList<>();

Arrays
  .stream(numbers)
  .forEach(numbersList::add);

numbersList
  .map(item -> item * 2)
  .forEach(System.out::println);
```

Using a class array:

```java
// If possible, use the wrapper class for the primitive type
Integer[] numbers = { 1, 2, 3, 4 };

List<Integer> numbersList = new ArrayList<>(Arrays.asList(numbers));

numbersList
  .map(item -> item * 2)
  .forEach(System.out::println);
```

### Enum
An Enum Type is a special data type that enables for a variable to be a set of predefined constants.
The variable must be equal to one of the values that have been predefined for it.

Enum constants are implicitly static and final. The enum constructor can only be package-private (no
modifier) or private.

```java
public enum Day {
  MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;
}
```

You can specify enum constant values at creation. Values can be accessed by the enum `values()` static
method which returns an array of values in the order they were defined. The `value` property on each
constant returns the value.

```java
public enum StockSymbol {
  APPLE("AAPL"),
  GOOGLE("GOOG"),
  MICROSOFT("MSFT"),
  AMAZON("AMZN");

  String value;

  StockSymbol(String value) {
    this.value = value;
  }
}

public class Main {
  public static void main(String[] args) {
    Arrays
      .stream(StockSymbol.values())
      .forEach(item -> System.out.println(item + ": " + item.value));
  }
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
public class Person {
  private String name;
  private int age;

  public Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  public void speak(String message) {
    System.out.println(message);
  }

  public int getAge() {
    return this.age;
  }

  public static void main(String[] args) {
    Person adam = new Person("Adam", 33);

    adam.speak("Hello!");

    int adamAge = adam.getAge();
  }
}
```

### Static Fields
Normally, when instantiating a class, the new object will have its own copies of the super class'
fields. Sometimes, you want to have fields common to all sub classes. Use the static keyword to do
this.

Typically, static variables will be constants (their value cannot be changed after assignment). In
order to ensure immutability, use the final keyword as well.

By convention, constants are named in uppercase.

### Method Overloading
Method overloading is the process of assigning multiple methods with the same name, but different signatures.

```java
public void speak(String message) {
  System.out.println(message);
}

public void speak(int age) {
  System.out.println("I am " + age + " years old.");
}
```

### Method Overriding
Method overriding allows you to override a method defined on a super class. The method invoked at
runtime will be determined by the instance of the class invoking it.

```java
public class Parent {
  public void greet() {
    System.out.println("Hello!");
  }
}

public class Child extends Parent {
  @Override
  public void greet() {
    System.out.println("Sup?");
  }
}

Parent parent = new Parent();
Child child = new Child();

parent.greet(); // Hello!
child.greet();  // Sup?
```

### Polymorphism
Polymorphism allows behaviors to be different based on the object invoking the behavior.

There are two types of polymorphism in Java: Runtime (dynamic) and Compile-time (static).

Method overriding is an example of dynamic polymorphism. The Java compiler doesn't know which method
to call. The JVM will decide at runtime whether to call the method on the super class, or the
overridden method on the sub class.

Method overloading is an example of static polymorphism. The compiler will know which method to call
based on the method signature at compile time.

Polymorphism is one of the four pillars of object oriented programming.

### Access Level Modifiers
Access level modifiers determine whether other classes can use a particular field or invoke a
particular method. There are two levels of access control:
 - top level: `public` or package-private (no modifier)
 - member level: `public`, `private`, `protected`, or package-private

| Modifier        | Class | Package | Subclass | World |
|-----------------|-------|---------|----------|-------|
| public          | yes   | yes     | yes      | yes   |
| protected       | yes   | yes     | yes      | no    |
| package private | yes   | yes     | no       | no    |
| private         | yes   | no      | no       | no    |

### Encapsulation
Encapsulation is the practice of making data fields private so they cannot be accessed or modified
directly. Instead, the class must define *getter* and *setter* methods to access and modify the
data.

Encapsulation is one of the four pillars of object oriented programming.

### Inheritance
Inheritance is used to share behavior between classes. This enables code reuse.

Inhertiance is one of the four pillars of object oriented programming.

```java
public class Person {
  private String name;
  private int age;

  Person(String name, int age) {
    this.name = name;
    this.age= age;
  }

  public String getName() {
    return this.name;
  }
}

public class WebDeveloper extends Person {
  // Web Developers have a programmingLanguages field that Persons do not
  private String[] programmingLanguages = {
    "HTML", "CSS", "JavaScript"
  }

  // Because Web Developers are Persons, they need a name and age
  // super calls the constructor on the Person class
  public WebDeveloper(String name, int age) {
    super(name, age);
  }
}

// You can also pass arguments directly to the super call
public Adam extends Person {
  public Adam() {
    super("Adam", 33);
  }

  // You can use super to call the getName method on the super class
  public printName() {
    String name = super.getName();
    System.out.println(name);
  }
}
```

### Composition
While inheritance deals with *is a* relationships, composition deals with *has a* relationships.

In this example, a Monitor is not a child of a Resolution. A Monitor has a Resolution as one of its
fields.

```java
public class Resolution {
  private int width;
  private int height;

  public Resolution() {
    this.width = width;
    this.height = height;
  }
}

public class Monitor {
  private Resolution resolution;

  public Monitor(int width, int height) {
    this.resolution = new Resolution(width, height);
  }
}
```

### Abstract Class
An abstract class is a class that is never instantiated directly. An abstract class contains
abstract methods that must be defined in the sub class.

In this example, the Person class will inherit the sleep method; but it must define the eat and
drink methods.

Abstraction is one of the four pillars of object oriented programming.

```java
public abstract class Human {
  public void sleep(int hours) {
    System.out.println("Goodnight.");
  }

  public abstract void eat();
  public abstract void drink();
}

public class Person extends Human {
  private int isHungry = true;
  private int isThirsty = true;

  @Override
  public void eat() {
    this.isHungry = false;
  }

  @Override
  public void drink() {
    this.isThirsty = false;
  }
}
```

### Interfaces
Interfaces are *implemented*, while classes are *extended*. Interfaces represent a *can a*
relationship.

Interfaces are useful in that a sub class can only extend one super class; however, a class can
implement multiple interfaces.

Implementing an interface forms a contract in a way that the class must define all methods in the
interface in order to be compiled. In the future, if you add a method to an interface, you'll have
to also define that method in all classes that implement the interface.

For example, if a Human eats and drinks, then a Person implementing the Human
interface must also eat and drink in order to be defined as a Human. The Human interface does not
define the behavior of eating or drinking; that is left up to the implementing class.

Starting in Java 8, an interface can also have default methods which can be used or overridden by the
implementing class. In many cases, an interface can be used instead of an abstract class now. The
key difference is that a method in an interface is inherently public; whereas an abstract class may
have public, private, or protected methods.

```java
public interface Human {
  void eat(boolean value);
  void drink(boolean value);
}

public class Person implements Human {
  private boolean isHungry = true;
  private boolean isThirsty = true;

  public void eat(boolean value) {
    this.isHungry = value;
  }

  public void drink(boolean value) {
    this.isThirsty = value;
  }
}
```

### Nested Classes
A class defined within another class is a nested class. Nested classes make sense when a particular
class is only used by one other class. By defining the class within the consuming class, it makes
your code more maintainable (instead of having a separate file).

There are two types of nested classes: static nested classes and inner classes (non-static). Static
nested classes do not have access to other members of the enclosing class. Inner classes do have
access to other members of the enclosing class, even if they are declared private.

There are two types of inner classes: local and anonymous. Local classes are typically defined in
the body of a method (or even a loop or conditional statement). Anonymous classes are like local
classes, except they are declared and instantiated at the same time and do not have a name.

Anonymous classes can be created from either classes (including abstract) or interfaces.

```java
public class HelloWorldClasses {
  // Private member variables may be accessed by inner classes
  private String helloWorldEnglish = "Hello World";
  private String helloWorldFrench = "Tout le Monde";

  // Inner interface
  interface HelloWorld {
    public void greet();
  }

  public void sayHello() {
    // Local inner class declared within method body
    class EnglishGreeting implements HelloWorld {
      public void greet() {
        System.out.println(helloWorldEnglish);
      }
    }

    // englishGreeting is instantiated after being declared
    HelloWorld englishGreeting = new EnglishGreeting();

    // Anonymous inner class
    // Declared and instantiated at the same time
    HelloWorld frenchGreeting = new HelloWorld() {
      public void greet() {
        System.out.println(helloWorldFrench);
      }
    };

    englishGreeting.greet();
    frenchGreeting.greet();
  }
}
```

### Packages
Packages are groups of class files organized by namespace. Packages are conventionally named by
reverse domain name, e.g., com.domainname.applicationname.packagename.

For example, com.adamelliotfields.package or com.github.adamelliotfields.package.

For personal projects where your package will never be consumed by anyone else, you can name your
package anything.

### Modules
A module is a group of packages that can also contain class, resource, and property/configuration files as
well.
