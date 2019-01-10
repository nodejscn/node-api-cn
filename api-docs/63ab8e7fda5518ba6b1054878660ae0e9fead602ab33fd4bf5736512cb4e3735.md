<!-- YAML
added: v9.4.0
-->

* `alt` {string} A description of the alternative service configuration as
  defined by [RFC 7838][].
* `originOrStream` {number|string|URL|Object} Either a URL string specifying
  the origin (or an `Object` with an `origin` property) or the numeric
  identifier of an active `Http2Stream` as given by the `http2stream.id`
  property.

Submits an `ALTSVC` frame (as defined by [RFC 7838][]) to the connected client.

```js
const http2 = require('http2');

const server = http2.createServer();
server.on('session', (session) => {
  // Set altsvc for origin https://example.org:80
  session.altsvc('h2=":8000"', 'https://example.org:80');
});

server.on('stream', (stream) => {
  // Set altsvc for a specific stream
  stream.session.altsvc('h2=":8000"', stream.id);
});
```

Sending an `ALTSVC` frame with a specific stream ID indicates that the alternate
service is associated with the origin of the given `Http2Stream`.

The `alt` and origin string *must* contain only ASCII bytes and are
strictly interpreted as a sequence of ASCII bytes. The special value `'clear'`
may be passed to clear any previously set alternative service for a given
domain.

When a string is passed for the `originOrStream` argument, it will be parsed as
a URL and the origin will be derived. For instance, the origin for the
HTTP URL `'https://example.org/foo/bar'` is the ASCII string
`'https://example.org'`. An error will be thrown if either the given string
cannot be parsed as a URL or if a valid origin cannot be derived.

A `URL` object, or any object with an `origin` property, may be passed as
`originOrStream`, in which case the value of the `origin` property will be
used. The value of the `origin` property *must* be a properly serialized
ASCII origin.

