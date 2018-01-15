# NodeJS API Reference

### [Globals](https://nodejs.org/api/globals.html)
These objects are available in all modules. Some of these objects aren't actually in the global scope but in the module scope - this will be noted.

The objects listed here are specific to Node.js. There are a number of built-in objects that are part of the JavaScript language itself, which are also globally accessible.

[__dirname](https://nodejs.org/api/globals.html#globals_dirname)
 - The directory name of the current module. This the same as the `path.dirname()` of the `__filename`.
 - `__dirname` is not actually a global but rather local to each module.

[__filename](https://nodejs.org/api/globals.html#globals_filename)
 - The file name of the current module. This is the resolved absolute path of the current module file.
 - For a main program this is not necessarily the same as the file name used in the command line.
 - `__filename` is not actually a global but rather local to each module.

[console](https://nodejs.org/api/globals.html#globals_console)
 - Used to print to `stdout` and `stderr`.

[exports](https://nodejs.org/api/globals.html#globals_exports)
 - A reference to the `module.exports` object that is shorter to type.
 - `exports` is not actually a global but rather local to each module.

[global](https://nodejs.org/api/globals.html#globals_global)
 - In browsers, the top-level scope is the global scope. That means that in browsers if you're in the global scope, `var something` will define a global variable.
 - In Node.js this is different. The top-level scope is not the global scope; `var something` inside an Node.js module will be local to that module.

[module](https://nodejs.org/api/globals.html#globals_module)
 - A reference to the current module. In particular `module.exports` is used for defining what a module exports and makes available through `require()`.
 - `module` is not actually a global but rather local to each module.

[process](https://nodejs.org/api/globals.html#globals_process)
 - The process object.

[require()](https://nodejs.org/api/globals.html#globals_require)
 - To require modules.
 - `require` is not actually a global, but rather local to each module.

### [Modules](https://nodejs.org/api/modules.html#modules_modules)
Node.js has a simple module loading system. In Node.js, files and modules are in one-to-one correspondence (each file is treated as a separate module).

Variables local to the module will be private, because the module is wrapped in a function by Node.js.

If you want the root of your module's export to be a function (such as a constructor) or if you want to export a complete object in one assignment instead of building it one property at a time, assign it to `module.exports` instead of `exports`.

The module system is implemented in the `require('module')` module.

[module.exports](https://nodejs.org/api/modules.html#modules_module_exports)
 - The `module.exports` object is created by the Module system. Sometimes this is not acceptable; many want their module to be an instance of some class. To do this, assign the desired export object to `module.exports`.
 - Note that assigning the desired object to exports will simply rebind the local exports variable, which is probably not what you want to do.

### [Events](https://nodejs.org/api/events.html#events_events)
Much of the Node.js core API is built around an idiomatic asynchronous event-driven architecture in which certain kinds of objects (called "emitters") periodically emit named events that cause Function objects ("listeners") to be called.

For instance: a `net.Server` object emits an event each time a peer connects to it; a `fs.ReadStream` emits an event when the file is opened; a stream emits an event whenever data is available to be read.

All objects that emit events are instances of the `EventEmitter` class. These objects expose an `eventEmitter.on()` function that allows one or more functions to be attached to named events emitted by the object. Typically, event names are camel-cased strings but any valid JavaScript property key can be used.

When the `EventEmitter` object emits an event, all of the functions attached to that specific event are called synchronously. Any values returned by the called listeners are ignored and will be discarded.

[EventEmitter](https://nodejs.org/api/events.html#events_class_eventemitter)
 - The `EventEmitter` class is defined and exposed by the `events` module.
 - All `EventEmitter`s emit the event `newListener` when new listeners are added and `removeListener` when existing listeners are removed.

### [HTTP](https://nodejs.org/api/http.html#http_http)
To use the HTTP server and client one must `require('http')`.

The HTTP interfaces in Node.js are designed to support many features of the protocol which have been traditionally difficult to use. In particular, large, possibly chunk-encoded, messages. The interface is careful to never buffer entire requests or responses--the user is able to stream data.

[http.createServer([requestListener])](https://nodejs.org/api/http.html#http_http_createserver_requestlistener)
 - Returns a new instance of `http.Server`.
 - The `requestListener` is a function which is automatically added to the `request` event.

[response.writeHead(statusCode[, statusMessage][,  headers])](https://nodejs.org/api/http.html#http_response_writehead_statuscode_statusmessage_headers)
 - Sends a response header to the request. The status code is a 3-digit HTTP status code, like `404`. The last argument, `headers`, are the response headers. Optionally one can give a human-readable `statusMessage` as the second argument.

[request.end([data][, encoding][, callback])](https://nodejs.org/api/http.html#http_request_end_data_encoding_callback)
 - Finishes sending the request. If any parts of the body are unsent, it will flush them to the stream. If the request is chunked, this will send the terminating `0\r\n\r\n`.
 - If `data` is specified, it is equivalent to calling `response.write(data, encoding)` followed by `request.end(callback)`.
 - If `callback` is specified, it will be called when the request stream is finished.

[server.listen([port][, hostname][, backlog][, callback])](https://nodejs.org/api/http.html#http_server_listen_port_hostname_backlog_callback)
 - Begin accepting connections on the specified `port` and `hostname`. If the `hostname` is omitted, the server will accept connections on the unspecified IPv6 address (::) when IPv6 is available, or the unspecified IPv4 address (0.0.0.0) otherwise.
 - Note: in most operating systems, listening to the unspecified IPv6 address (::) may cause the `net.Server` to also listen on the unspecified IPv4 address (0.0.0.0).
 - Omit the port argument, or use a port value of 0, to have the operating system assign a random port, which can be retrieved by using `server.address().port` after the `listening` event has been emitted.
 - To listen to a unix socket, supply a filename instead of port and hostname.
 - `backlog` is the maximum length of the queue of pending connections. The actual length will be determined by your OS through `sysctl` settings such as `tcp_max_syn_backlog` and `somaxconn` on linux. The default value of this parameter is 511 (not 512).
 - This function is asynchronous. `callback` will be added as a listener for the `listening` event.
 - Note: The `server.listen()` method may be called multiple times. Each subsequent call will re-open the server using the provided options.

[response.write(chunk[, encoding][, callback])](https://nodejs.org/api/http.html#http_response_write_chunk_encoding_callback)
 - If this method is called and `response.writeHead()` has not been called, it will switch to implicit header mode and flush the implicit headers.
 - This sends a chunk of the response body. This method may be called multiple times to provide successive parts of the body.
 - `chunk` can be a string or a buffer. If `chunk` is a string, the second parameter specifies how to encode it into a byte stream. By default the encoding is `utf8`. `callback` will be called when this chunk of data is flushed.
 - Note: This is the raw HTTP body and has nothing to do with higher-level multi-part body encodings that may be used.
 - The first time `response.write()` is called, it will send the buffered header information and the first body to the client. The second time `response.write()` is called, Node.js assumes you're going to be streaming data, and sends that separately. That is, the response is buffered up to the first chunk of body.
 - Returns `true` if the entire data was flushed successfully to the kernel buffer. Returns `false` if all or part of the data was queued in user memory. `drain` will be emitted when the buffer is free again.

[message.method](https://nodejs.org/api/http.html#http_message_method)
 - Only valid for request obtained from `http.Server`.
 - The request method as a string. Read only. Example: `GET`, `DELETE`.

### [FS](https://nodejs.org/api/fs.html#fs_file_system)
File I/O is provided by simple wrappers around standard POSIX functions. To use this module do `require('fs')`. All the methods have asynchronous and synchronous forms.

The asynchronous form always takes a completion callback as its last argument. The arguments passed to the completion callback depend on the method, but the first argument is always reserved for an exception. If the operation was completed successfully, then the first argument will be `null` or `undefined`.

When using the synchronous form any exceptions are immediately thrown. You can use try/catch to handle exceptions or allow them to bubble up.

[fs.readFile(file[, options], callback)](https://nodejs.org/api/fs.html#fs_fs_readfile_file_options_callback)
 - Asynchronously reads the entire contents of a file.
 - The callback is passed two arguments `(err, data)`, where `data` is the contents of the file.
 - If no encoding is specified, then the raw buffer is returned.
 - If `options` is a string, then it specifies the encoding. 
 - Any specified file descriptor has to support reading.
 - Note: If a file descriptor is specified as the `file`, it will not be closed automatically.

[fs.readFileSync(file[, options])](https://nodejs.org/api/fs.html#fs_fs_readfilesync_file_options)
 - Synchronous version of `fs.readFile`. Returns the contents of the file.
 - If the encoding option is specified then this function returns a string. Otherwise it returns a buffer.

### [Stream](https://nodejs.org/api/stream.html#stream_stream)
A stream is an abstract interface for working with streaming data in Node.js. The `stream` module provides a base API that makes it easy to build objects that implement the stream interface.

There are many stream objects provided by Node.js. For instance, a request to an HTTP server and `process.stdout` are both stream instances.

Streams can be readable, writable, or both. All streams are instances of `EventEmitter`.

### [Query String](https://nodejs.org/api/querystring.html#querystring_query_string)
The `querystring` module provides utilities for parsing and formatting URL query strings.

[querystring.stringify(obj[, sep[, eq[, options]]])](https://nodejs.org/api/querystring.html#querystring_querystring_stringify_obj_sep_eq_options)
 - The `querystring.stringify()` method produces a URL query string from a given `obj` by iterating through the object's "own properties".

[querystring.parse(str[, sep[, eq[, options]]])](https://nodejs.org/api/querystring.html#querystring_querystring_parse_str_sep_eq_options)
 - The `querystring.parse()` method parses a URL query string (`str`) into a collection of key and value pairs.
