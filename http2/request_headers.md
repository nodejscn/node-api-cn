<!-- YAML
added: v8.4.0
-->

* {Object}

The request/response headers object.

Key-value pairs of header names and values. Header names are lower-cased.
Example:

```js
// Prints something like:
//
// { 'user-agent': 'curl/7.22.0',
//   host: '127.0.0.1:8000',
//   accept: '*/*' }
console.log(request.headers);
```

See [Headers Object][].

*Note*: In HTTP/2, the request path, host name, protocol, and method are
represented as special headers prefixed with the `:` character (e.g. `':path'`).
These special headers will be included in the `request.headers` object. Care
must be taken not to inadvertently modify these special headers or errors may
occur. For instance, removing all headers from the request will cause errors
to occur:

```js
removeAllHeaders(request.headers);
assert(request.url);   // Fails because the :path header has been removed
```

