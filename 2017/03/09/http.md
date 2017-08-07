# HTTP
HTTP stands for HyperText Transfer Protocol and represents a format of communication between two devices over the internet.

The internet consists of a vast array of highly-connected devices spanning the entire globe. To ensure that any two devices can communicate, it was necessary to develop a common set of rules - or protocol - to facilitate dependable communication.

HTTP itself is a "stateless" protocol, which means there is no record of previous interactions, and each interaction is processed only with the information that comes with that particular interaction. 

### HTTP Request Format
In general, there are four parts:
 1. The request line
 2. A series of headers with name/value pairs on separate lines
 3. A blank line
 4. If the request is a POST request, a body or payload.

### HTTP Response Format
The format is very similar to requests, and consists of four parts:
 1. A status line
 2. A series of headers in name/value pairs that are on lines of their own
 3. A blank line
 4. The response body.

### URI vs URL
A Uniform Resource Identifier (URI) is a compact sequence of characters that identifies an abstract or physical resource.

A Uniform Resource Locator (URL) refers to the subset of URIs that, in addition to identifying a resource, provide a means of locating the resource by describing its primary access mechanism (e.g., its network “location”).

A Uniform Resource Name (URN) functions like a person’s name, while a Uniform Resource Locator (URL) resembles that person’s street address. In other words: the URN defines an item’s identity, while the URL provides a method for finding it.

### Telnet
Telnet is a protocol used to provide bidirectional, text-oriented communication using a terminal connection.

Connect to httpbin.org on port 80:

```bash
telnet httpbin.org 80
```

Use a `GET` request on the root (`/`) resource using HTTP 1.1 specification. 

Specify the host again in the event the host has multiple domains on the same IP:

```bash
GET / HTTP/1.1
Host: httpbin.org
```

You can also make a request on the `/xml` resource which will return a response in XML:

```bash
GET /xml HTTP/1.1
Host: httpbin.org
```
