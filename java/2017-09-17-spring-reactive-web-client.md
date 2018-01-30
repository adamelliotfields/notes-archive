# Spring Reactive Web Client
> :calendar: *September 17, 2017*

This is a demonstration of the new `WebClient` interface in Spring 5 Reactive, as well as some basic
data manipulation with the new `Mono` reactive type.

We'll be using the familiar annotation-based approach to routing, instead of the new
Handler/Function convention. The new way seems better suited to Kotlin (or another framework
altogether like Play using Scala).

For the purpose of the demo, we'll be making a request to the Giphy API, constructing a new model
object from the response, and returning a Mono emitting either the success or error object.

### References
 - <https://spring.io/blog/2017/03/15/spring-tips-the-spring-web-flux-reactive-client>
 - <https://docs.spring.io/spring-framework/docs/5.0.x/spring-framework-reference/reactive-web.html>
 - <https://docs.spring.io/spring/docs/5.0.x/javadoc-api/org/springframework/web/reactive/function/client/WebClient.html>
 - <https://projectreactor.io/docs/core/release/reference/>
 - <https://projectreactor.io/docs/core/release/api/>
 - <http://www.baeldung.com/spring-5-webclient>

### `settings.gradle`

```gradle
rootProject.name = 'spring-webclient-demo'
```

### `build.gradle`
In Spring Boot 2.0.0, you'll need to add both the Spring Boot plugin as well as the Spring
dependency management plugin. Read this blog post from the Spring team for more information: <https://spring.io/blog/2017/04/05/spring-boot-s-new-gradle-plugin>.

```gradle
buildscript {
  ext {
    springBootVersion = '2.0.0.M4'
  }
  repositories {
    jcenter()
    maven { url 'https://repo.spring.io/milestone' }
  }
  dependencies {
    classpath "org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}"
  }
}

plugins {
  id 'java'
  id 'application'
}

apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management'

repositories {
  jcenter()
  maven { url 'https://repo.spring.io/milestone' }
}

dependencies {
  compile "org.springframework.boot:spring-boot-starter-webflux:${springBootVersion}"
  compile 'org.projectlombok:lombok:1.16.18'
}

mainClassName = 'demo.App'
group = 'demo'
version ='1.0.0'
sourceCompatibility = 1.8
targetCompatibility = 1.8
```

### `src/main/resources/giphy.properties`
Add your Giphy API key in this file. You can get one easily from <https://developers.giphy.com/>.

```ini
key=YOUR_API_KEY
```

### `src/main/java/demo/App.java`

```java
@SpringBootApplication
public class App {
  public static void main(String[] args) throws Exception {
    SpringApplication.run(App.class, args);
  }
}
```

### `src/main/java/demo/dto/GifDto.java`
I've tried a few different approaches, but nothing is simpler than capturing the API response in a
Data Transfer Object (DTO) and using the DTO to construct a new object with the properties we want.

Lombok's `@Data` annotation will provide the necessary boilerplate for Jackson to deserialize it
(convert the JSON response string to a POJO).

The response from Giphy looks like this:

```json
{
  "data": {
    ...
  },
  "meta": {
    ...
  }
}
```

So our POJO will look like this:

```java
@Data
public class GifDto {
  private final Map data;
  private final Map meta;
}
```

### `src/main/java/demo/model/Gif.java`
In this example, we'll just take the "image_url" property from Giphy. This is the URL to use when
displaying in a `<img>` tag.

Note that we must use the `Object` type and not `String`, as the `"image_url"` property could be
anything (a string, integer, boolean, array, object, etc).

```java
@Data
public class Gif {
  private Object imageUrl;

  public Gif(GifDto gif) {
    this.imageUrl = gif.getData().get("image_url");
  }
}
```

The serialized JSON will look like this:

```json
{
  "imageUrl": ...
}
```

### `src/main/java/demo/model/Error.java`
We need to also provide an `Error` object, in the event our API key was invalid or we were not able
to connect to Giphy.

The constructor will take the exception thrown (`WebClientResponseException` in this case) and the
`HttpStatus` we want to use.

```java
@Data
public class Error {
  private int status;
  private String error;
  private String message;

  public Error(Throwable exception, HttpStatus httpStatus) {
    this.status = httpStatus.value();
    this.error = httpStatus.getReasonPhrase();
    this.message = exception.getMessage();
  }
}
```

### `src/main/java/demo/controller/GifController.java`
Finally, our controller will have one route which returns a `Mono`. A Mono is a reactive type that
emits either 0 or 1 items. In this case, it will either emit a `Gif` or an `Error` object.

There are numerous ways to handle errors when working with reactive types, and they are all outlined
in the Reactor reference link. I've found the old fashioned try/catch block to be the most straight
forward.

If we were able to successfully connect to Giphy and get a response, we'll construct a new `Gif`
object, set the status to 200, and return a `Mono` that emits the `Gif`.

In the event of an error, we will construct a new `Error` object, log the error, set the status to
500, and return a `Mono` that emits the `Error`.

The Lombok `@Log` annotation provides access to JUL (`java.util.logging`).

The Spring `@RestController` annotation is used when returning a JSON response, as it binds the
return value of a method to the response body.

Finally, the `@PropertySource` and `@Value` annotations allow us to access the `.properties` file
which contains our Giphy API key.

The array passed to `@RequestMapping` shows how to deal with trailing forward slashes (although for
the index route this is redundant).

The `block()` method at the end of the `WebClient` chain gives us access to the item emitted by the
`Mono` (in this case it's our `GifDto`).

The `Mono.just()` static method wraps an object in a `Mono`.

Also note the use of `ServerHttpResponse` instead of Tomcat's `HttpServletResponse`, because we are
using an embedded Netty web server.

```java
@Log
@RestController
@PropertySource("classpath:giphy.properties")
public class AppController {
  @Value("${key}")
  private String key;

  @RequestMapping(path = {"", "/"}, method = RequestMethod.GET, produces = MediaType.APPLICATION_JSON_VALUE)
  public Mono<Object> getGif(ServerHttpResponse response) {
    URI uri = URI.create(String.format("http://api.giphy.com/v1/gifs/random?api_key=%s", key));

    try {
      GifDto gifDto = WebClient
          .create()
          .get()
          .uri(uri)
          .retrieve()
          .bodyToMono(GifDto.class)
          .block();

      Gif gif = new Gif(gifDto);

      response.setStatusCode(HttpStatus.OK);

      return Mono.just(gif);
    } catch (WebClientResponseException exception) {
      Error error = new Error(exception, HttpStatus.INTERNAL_SERVER_ERROR);

      log.log(Level.SEVERE, exception.getMessage());
      response.setStatusCode(HttpStatus.INTERNAL_SERVER_ERROR);

      return Mono.just(error);
    }
  }
}
```

## Returning the Raw JSON Response

If you wanted to get the entire response from Giphy (if you were parsing the JSON in your client
app), you could eliminate the try/catch block and use `onErrorResume` instead.

Note that `bodyToMono()` and `onErrorResume()` have to return the same type, so you could not use
the `Gif` and `Error` objects. You could create a utility class with a static method that returns
the error `Map` if you wanted to repeat this pattern for multiple routes.

```java
@RequestMapping(path = {"", "/"}, method = RequestMethod.GET, produces = MediaType.APPLICATION_JSON_VALUE)
public Mono<Map> getGif(ServerHttpResponse response) {
  URI uri = URI.create(String.format("http://api.giphy.com/v1/gifs/random?api_key=%s", key));

  response.setStatusCode(HttpStatus.OK);

  return WebClient
      .create()
      .get()
      .uri(uri)
      .retrieve()
      .bodyToMono(Map.class)
      .onErrorResume(exception -> {
        Map<String, Object> map = new LinkedHashMap<>();
        map.put("status", HttpStatus.INTERNAL_SERVER_ERROR.value());
        map.put("error", HttpStatus.INTERNAL_SERVER_ERROR.getReasonPhrase());
        map.put("message", exception.getMessage());

        log.log(Level.SEVERE, exception.getMessage());
        response.setStatusCode(HttpStatus.INTERNAL_SERVER_ERROR);

        return Mono.just(map);
      });
}
```

## Alternative to `WebClient`

You can also use the Jackson `ObjectMapper`'s `readValue()` method and pass it a URL and class to
deserialize; however, to the best of my knowledge, this would not be asynchronous.

Finally, there is also a new `AsyncRestTemplate` as an alternative to `WebClient`.

```java
@Log
@RestController
@PropertySource("classpath:giphy.properties")
public class AppController {
  @Value("${key}")
  private String key;
  private ObjectMapper mapper;

  @Autowired
  public AppController(ObjectMapper mapper) {
    this.mapper = mapper;
  }

  @RequestMapping(path = {"", "/"}, method = RequestMethod.GET, produces = MediaType.APPLICATION_JSON_VALUE)
  public Mono<Map> getGif(ServerHttpResponse response) {
    try {
      URL url = new URL(String.format("http://api.giphy.com/v1/gifs/random?api_key=%s42", key));

      response.setStatus(HttpStatus.OK);

      return Mono.just(mapper.readValue(url, Map.class));
    } catch (IOException exception) {
      Map<String, Object> map = new LinkedHashMap<>();
      map.put("status", HttpStatus.INTERNAL_SERVER_ERROR.value());
      map.put("error", HttpStatus.INTERNAL_SERVER_ERROR.getReasonPhrase());
      map.put("message", exception.getMessage());

      log.log(Level.SEVERE, exception.getMessage());
      response.setStatus(HttpStatus.INTERNAL_SERVER_ERROR);

      return Mono.just(map);
    }
  }
}
