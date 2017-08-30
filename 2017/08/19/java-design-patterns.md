# Java Design Patterns

### Gang of Four
The Gang of Four refers to the authors of [Design Patterns: Elements of Reusable Object-Oriented Software](https://www.amazon.com/Design-Patterns-Object-Oriented-Addison-Wesley-Professional-ebook/dp/B000SEIBB8/).

The book includes 23 design patterns, divided by type: Creational, Structural, and Behavioral.


## Creational Design Patterns
Creational patterns are ones that create objects for you, rather than having you instantiate objects
directly. This gives your program more flexibility in deciding which objects need to be created for
a given case.

### Singleton Pattern
The Singleton Pattern ensures that there is only ever one instance of a class created in the JVM.
The class consists of a private static member variable (the instance itself), an empty private
constructor (to prevent being instantiated by other classes), and a public static getter method
(returns the instance).

```java
public class Singleton {
  private static final Singleton instance = new Singleton();

  private Singleton(){}

  public static Singleton getInstance() {
    return instance;
  }
}
```

### Factory Pattern
The Factory Pattern is used when a super class has multiple sub classes. A factory class can return
an instance of a sub class based on input at runtime.

The super class can be a class, abstract class, or interface.

The factory class can be a singleton.

```java
public class Car {
  private int year;
  private String make;
  private String model;

  public Car(int year, String make, String model) {
    this.year = year;
    this.make = make;
    this.model = model;
  }
}

public class BMW extends Car {
  public BMW(int year, String make, String model) {
    super(year, make, model);
  }
}

public class Audi extends Car {
  public Audi(int year, String make, String model) {
    super(year, make, model);
  }
}

public class CarFactory {
  public static Car getCar(int year, String make, String model) {
    switch (make.toLowerCase()) {
      case "BMW":
        return new BMW(year, make, model);
        break;
      case "Audi":
        return new Audi(year, make, model);
        break;
      case default:
        return null;
    }
  }
}
```

### Abstract Factory Pattern
The Abstract Factory Pattern extends the Factory Pattern so that the if-else block can be replaced
with factory classes for each sub class, and an abstract factory class that will return the sub
class based on the input factory class.

### Builder Pattern


## Structural Design Patterns
These concern class and object composition. They use inheritance to compose interfaces and define
ways to compose objects to obtain new functionality.

### Decorator Pattern


## Behavioral Design Patterns
Most of these design patterns are specifically concerned with communication between objects.

### State Pattern

### Dependency Injection Pattern
Google Guice

### Template Method Pattern
Abstract classes

### Observer Pattern
RxJava

## Architectural Design Patterns
An architectural pattern is a general, reusable solution to a commonly occurring problem in software
architecture within a given context.

### Microservices Pattern

### API Gateway Pattern


## Concurrency Design Patterns
Concurrency patterns are those types of design patterns that deal with the multi-threaded
programming paradigm.

### Promise Pattern
Futures

### Thread Pool Pattern


## Presentational Design Patterns

### Model View Controller Pattern

### Model View View-Model Pattern

### Flux Pattern
