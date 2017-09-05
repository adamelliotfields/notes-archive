# Spring Boot Shell
This is a walk-through of a basic Spring Shell app using Spring Boot.

### Gradle
Starting with v2, there is a new starter artifact which includes Spring Boot starter.

Note the use of Gradle's new plugin mechanism (you don't have to define the `classpath` in the
`buildscript` block).

**`build.gradle`**

```java
plugins {
  id 'java'
  id 'application'
  id 'org.springframework.boot' version '1.5.6.RELEASE'
}

repositories {
  jcenter()
  // Provide the location of Spring snapshots
  maven {
    url 'http://repo.spring.io/libs-snapshot'
  }
}

dependencies {
  // Includes spring-boot-starter v1.5.6
  compile 'org.springframework.shell:spring-shell-starter:2.0.0.BUILD-SNAPSHOT'
  // Optional, used to simplify creation of getters and setters
  compile 'org.projectlombok:lombok:1.16.18'
}

version = '1.0.0'
// Rename group and mainClassName to whatever you want
group = 'io.github.adamelliotfields'
mainClassName = 'io.github.adamelliotfields.App'
sourceCompatibility = 1.8
targetCompatibility = 1.8
```

### Main Class

**`App.java`**

Make sure you put your main class inside a base package, i.e., `io.github.adamelliotfields`,
otherwise Spring may not find your components.

```java
@SpringBootApplication
public class App {
  public static void main(String[] args) {
    SpringApplication.run(App.class, args);
  }
}
```

### Domain Classes

**`domain/Todo.java`**

This is a simple domain model class with two fields: a `String` title and a `boolean` completion
status.

Lombok will provide getters and setters.

```java
public class Todo {
  @Getter
  private String title;

  @Getter
  @Setter
  private boolean completed;

  public Todo(String title) {
    this.title = title;
    this.completed = false;
  }
}
```

**`domain/TodoRepository.java`**

The repository class is simply a list of `Todo`s with a getter method. You could have your CRUD
operation methods defined in this class or a seperate DAO implementation, but for the sake of
simplicity they will all be defined in a service class.

You may annotate the class with `@Component`, although it is a best practice to use a specific
stereotype annotation to improve readability.

```java
@Repository
public class TodoRepository {
  @Getter
  private List<Todo> todos;

  public TodoRepository() {
    this.todos = new ArrayList<>();
  }
}
```

### Service Class
The service class includes all CRUD operations and transformations to prepare the data for the
controller.

The repository class is autowired to the service class.

**`service/TodoService.java`**

```java
@Service
public class TodoService {
  private TodoRepository todoRepository;

  // Always use constructor dependency injection
  @Autowired
  public TodoService(TodoRepository todoRepository) {
    this.todoRepository = todoRepository;
  }

  public String add(String title) {
    Todo todo = new Todo(title);
    todoRepository.getTodos().add(todo);

    return "Added: " + todo.getTitle();
  }

  public String delete(int index) {
    Todo todo = todoRepository.getTodos().get(index);
    todoRepository.getTodos().remove(index);

    return "Deleted: " + todo.getTitle();
  }

  public List<String> list() {
    List<Todo> todos = todoRepository.getTodos();

    if (todos.size() == 0) {
      List<String> message = new ArrayList<>();
      message.add("Nothing to do!");

      return message;
    }

    // You could also just use a for-loop
    // But that wouldn't be any fun
    return IntStream
             .range(0, todos.size())
             .mapToObj(i -> String.format(
                 "%d. %s [%s]",
                 i + 1,
                 todos.get(i).getTitle(),
                 todos.get(i).isCompleted() ? "complete" : "incomplete"
             ))
             .collect(Collectors.toList());
  }

  public String setComplete(int index) {
    Todo todo = todoRepository.getTodos().get(index);
    todo.setCompleted(true);

    return "Completed: " + todo.getTitle();
  }

  public String setIncomplete(int index) {
    Todo todo = todoRepository.getTodos().get(index);
    todo.setCompleted(false);

    return "Incomplete: " + todo.getTitle();
  }
}
```

### Controller Class
The `@ShellComponent` annotation is a new annotation that is a subset of `@Component`. You can now
start your shell application through `SpringApplication.run()` instead of `Bootstrap.main()`.

The `@ShellMethod` annotation takes a default value String to be displayed when the `help` command
is executed.

You can further customize your commands using `prefix()` or `@ShellOption`.

You can control command availability using the `Availability` class and `@ShellMethodAvailability`
annotation.

The service class is autowired to the controller.

**`controller/ShellController.java`**

```java
@ShellComponent
public class ShellController {
  private TodoService todoService;

  @Autowired
  public ShellController(TodoService todoService) {
    this.todoService = todoService;
  }

  @ShellMethod("Add a todo.")
  public String add(String todo) {
    return todoService.add(todo);
  }

  @ShellMethod("Delete a todo.")
  public String delete(int index) {
    return todoService.delete(index - 1);
  }

  // Spring Shell will automatically iterate over lists and print each item on a new line
  @ShellMethod("List todos.")
  public List<String> list() {
    return todoService.list();
  }

  // Camel-cased methods will be converted to kebab-case in the console, i.e., set-complete
  @ShellMethod("Mark a todo as complete.")
  public String setComplete(int index) {
    return todoService.setComplete(index - 1);
  }

  @ShellMethod("Mark a todo as incomplete.")
  public String setIncomplete(int index) {
    return todoService.setIncomplete(index - 1);
  }
}
```
