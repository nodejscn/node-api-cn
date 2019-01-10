<!-- YAML
added: v10.12.0
-->

* `origins` { string | URL | Object } One or more URL Strings passed as
  separate arguments.

Submits an `ORIGIN` frame (as defined by [RFC 8336][]) to the connected client
to advertise the set of origins for which the server is capable of providing
authoritative responses.

```js
const http2 = require('http2');
const options = getSecureOptionsSomehow();
const server = http2.createSecureServer(options);
server.on('stream', (stream) => {
  stream.respond();
  stream.end('ok');
});
server.on('session', (session) => {
  session.origin('https://example.com', 'https://example.org');
});
```

When a string is passed as an `origin`, it will be parsed as a URL and the
origin will be derived. For instance, the origin for the HTTP URL
`'https://example.org/foo/bar'` is the ASCII string
`'https://example.org'`. An error will be thrown if either the given string
cannot be parsed as a URL or if a valid origin cannot be derived.

A `URL` object, or any object with an `origin` property, may be passed as
an `origin`, in which case the value of the `origin` property will be
used. The value of the `origin` property *must* be a properly serialized
ASCII origin.

Alternatively, the `origins` option may be used when creating a new HTTP/2
server using the `http2.createSecureServer()` method:

```js
const http2 = require('http2');
const options = getSecureOptionsSomehow();
options.origins = ['https://example.com', 'https://example.org'];
const server = http2.createSecureServer(options);
server.on('stream', (stream) => {
  stream.respond();
  stream.end('ok');
});
```

