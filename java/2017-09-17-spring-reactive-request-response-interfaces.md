# Spring Reactive Request and Response Interfaces
> :calendar: *September 17, 2017*

In Spring 4.x, to access the HTTP Servlet request and response objects, you'd use Tomcat's
[HttpServletRequest](https://tomcat.apache.org/tomcat-8.5-doc/api/org/apache/catalina/servlet4preview/http/HttpServletRequest.html)
and [HttpServletResponse](https://tomcat.apache.org/tomcat-8.5-doc/api/org/apache/catalina/servlet4preview/http/HttpServletResponse.html)
interfaces.

In Spring 5 Reactive (Webflux), Netty is the default web server and thus is not a Servlet container.

This is a list of Getters for Spring Reactive's `ServerHttpRequest` and Setters for
`ServerHttpResponse` interfaces. These are the interfaces to use when using Spring's traditional
annotation routing (i.e., `@RequestMapping`). You'll want to use `ServerRequest` and
`ServerResponse` if you're using the new functional routing approach using `RouterFunction`.

## Request

### `request.getMethod()` and `request.getMethodValue()`
`getMethod()` returns a value from the `HttpMethod` enum, while `getMethodValue()` returns a String.

```
GET
```

### `request.getPath()`
Returns a `DefaultRequestPath` object with `fullPath`, `contextPath`, and `pathWithinApplication`
fields. These fields are of the type `DefaultPathContainer` and can be accessed with the `value()`
method.

```
DefaultRequestPath[
  fullPath='[path='/']',
  contextPath='',
  pathWithinApplication='/'
]
```

### `request.getURI()`
Returns the URI of the request of the type `URI`.

```
//localhost:8080/
```

### `request.getRemoteAddress()`
Returns an `InetSocketAddress` remote address where the request is connected to.

```
/0:0:0:0:0:0:0:1:50342
```

### `request.getQueryParams()`
Returns a `MultiValueMap<String, String>` containing the query params.

E.g., `http://localhost:8080?greeting=hello&name=adam`:

```
{
  greeting=[hello],
  name=[adam]
}
```

### `request.getCookies()`
Returns a `MultiValueMap<String, HttpCookie>` sent by the client.

```
{
  Webstorm-5bf985f9=[Webstorm-5bf985f9=48667e12-349e-4bda-8a8b-17f36c2ebf8f],
  Idea-bee79cb2=[Idea-bee79cb2=d00fd55a-a68e-43a0-87bf-49b6e453c688]
}
```

### `request.getHeaders()`
Returns a `MultiValueMap<String, String>` containing the request headers.

```
{
  Host=[localhost:8080],
  Connection=[keep-alive],
  Upgrade-Insecure-Requests=[1],
  User-Agent=[Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.113 Safari/537.36],
  Accept=[text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8],
  DNT=[1],
  Accept-Encoding=[gzip, deflate, br],
  Accept-Language=[en-US,en;q=0.8],
  Cookie=[Webstorm-5bf985f9=48667e12-349e-4bda-8a8b-17f36c2ebf8f; Idea-bee79cb2=d00fd55a-a68e-43a0-87bf-49b6e453c688]
}
```

### `request.getBody()`
Returns a `Flux<DataBuffer>` containing the body of the message as a `Publisher`.

To access the JSON request body as a `Map`, use `@RequestBody Map requestBody` in your method
parameter as usual.

*Note: this is the serialized JSON*

```json
[
  {
    "nativeBuffer": {
      "direct": true,
      "readOnly": false,
      "readable": true,
      "writable": false
    }
  }
]
```

## Response

### `response.setStatusCode(HttpStatus status)`
Sets the HTTP status code for the response.

```java
response.setStatusCode(HttpStatus.I_AM_A_TEAPOT);
```
