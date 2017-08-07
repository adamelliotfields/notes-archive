# AJAX Notes

### [AJAX](https://developer.mozilla.org/en-US/docs/AJAX)
AJAX stands for Asynchronous JavaScript and XML. 

In a nutshell, it is the use of the XMLHttpRequest object to communicate with server-side scripts. It can send as well as receive information in a variety of formats, including JSON, XML, HTML, and even text files.

AJAX lets you build webpages that ask for information from a web server. The web server returns data to the web browser, and JavaScript processes that data to selectively change parts of the web page. The amount of data the server returns is usually significantly less than an entire web page.

Microsoft first introduced AJAX in 1999 with IE5. AJAX isn't its official name; technically it is the `XMLHttpRequest` Object or XHR.

AJAX is the process of using JavaScript to send a request to a web server, receive a response, and do something with that response.

### How AJAX Works
 1. Create an `XMLHttpRequest` Object.
    - The web browser needs to create an object that has all the methods you'll need to send and receive data.
 2. Define a callback function.
    - This is the programming you want to run when the server sends its response.
 3. Open a request.
    - The method the browser will use to send the request, and the URL where the request will be sent.
 4. Send the request.

```html
<div id="ajax"></div>
```

```javascript
let xhr = new XMLHttpRequest();

xhr.onreadystatechange = () => {
  if (xhr.readyState === 4 && xhr.status === 200) {
    document.getElementById('ajax').innerHTML = xhr.responseText;
  }
}

xhr.open('GET', 'helloworld.html');

xhr.send();
```

### HTTP Requests
 - **GET:** Used for most requests. Browser uses the GET method whenever it requests a new web page, CSS file, image, and so on. Use GET when you want to "get" something from the server.
 - **POST:** Used frequently with web forms to send data to store in a database. Use POST when sending data that will store, delete or update information from a database.

### AJAX Response Formats
 - **XML:** Extensible Markup Language. When using XML with JavaScript, you must parse the document, then go through each node to extract data from the tags.
 - **JSON:** JavaScript Object Notation. JSON can be formatted using arrays or objects (or both). In valid JSON, property names and values must use double quotes.

### AJAX Security Limitations
Web browsers prevent certain types of AJAX requests, such as requests to other web sites:
 - **Same-origin Policy:** Two pages have the same origin if the protocol (http or https), port, and host are the same.

### Parsing JSON Data
JSON is transmitted as a plain text string. To make it useful for JavaScript, you need to parse it:
 - [JSON.parse()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON/parse)

```javascript
JSON.parse(xhr.responseText);
```

### AJAX with jQuery
[.load()](http://api.jquery.com/load/)
 - `.load()` loads data from the server and place the returned HTML into the matched element. This method is the simplest way to fetch data from the server. It is roughly equivalent to `$.get( url, data, callback )` except that it is a method rather than global function and it has an implicit callback function.

[$.post()](http://api.jquery.com/jQuery.post/)
 - `$.post(url, data, callback)` loads data from the server using a HTTP POST request. This is a shorthand Ajax function, which is equivalent to `$.ajax( { type: 'POST', url, data, success, dataType } )`.

[$.getJSON()](http://api.jquery.com/jQuery.getJSON/)
 - `$.getJSON(url, [data], [success])` loads JSON-encoded data from the server using a GET HTTP request. This is a shorthand Ajax function, which is equivalent to `$.ajax( { dataType: 'json', url, data, success } )`

[$.ajax()](http://api.jquery.com/jQuery.ajax/)
 - `$.ajax( url, [settings] )` performs an asynchronous HTTP (i.e., AJAX) request. `url` is a string containing the URL to which the request is sent. `[settings]` is a set of key-value pairs that configure the AJAX request. A default can be set for any option with `$.ajaxSetup()`.

[$.each()](http://api.jquery.com/jQuery.each/)
 - `$.each( array, callback(index, value) )` iterates over a jQuery object, executing a function for each matched element. The .each() method is designed to make DOM looping constructs concise and less error-prone. When called it iterates over the DOM elements that are part of the jQuery object. Each time the callback runs, it is passed the current loop iteration, beginning from 0. More importantly, the callback is fired in the context of the current DOM element, so the keyword this refers to the element.

[.serialize()](http://api.jquery.com/serialize/)
 - `.serialize()` creates a text string in standard URL-encoded notation. It can act on a jQuery object that has selected individual form controls, such as `<input>`, `<textarea>`, and `<select>`.

[event.preventDefault()](http://api.jquery.com/event.preventDefault/)
 - `event.preventDefault()` prevents the default action of an event (e.g., browser refresh) from triggering. You can check whether the default action was prevented using `event.isDefaultPrevented()`.

### jqXHR
The jQuery XMLHttpRequest (jqXHR) object returned by `$.ajax()` as of jQuery 1.5 is a superset of the browser's native XMLHttpRequest object. For example, it contains `responseText` and `responseXML` properties, as well as a `getResponseHeader()` method. When the transport mechanism is something other than `XMLHttpRequest` (for example, a script tag for a JSONP request) the jqXHR object simulates native XHR functionality where possible.
