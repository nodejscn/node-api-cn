<!-- YAML
added: v8.4.0
-->

* `statusCode` {number}
* `statusMessage` {string}
* `headers` {Object}

Sends a response header to the request. The status code is a 3-digit HTTP
status code, like `404`. The last argument, `headers`, are the response headers.

For compatibility with [HTTP/1](), a human-readable `statusMessage` may be
passed as the second argument. However, because the `statusMessage` has no
meaning within HTTP/2, the argument will have no effect and a process warning
will be emitted.

Example:

```js
const body = 'hello world';
response.writeHead(200, {
  'Content-Length': Buffer.byteLength(body),
  'Content-Type': 'text/plain' });
```

Note that Content-Length is given in bytes not characters. The
`Buffer.byteLength()` API  may be used to determine the number of bytes in a
given encoding. On outbound messages, Node.js does not check if Content-Length
and the length of the body being transmitted are equal or not. However, when
receiving messages, Node.js will automatically reject messages when the
Content-Length does not match the actual payload size.

This method may be called at most one time on a message before
[`response.end()`][] is called.

If [`response.write()`][] or [`response.end()`][] are called before calling
this, the implicit/mutable headers will be calculated and call this function.

When headers have been set with [`response.setHeader()`][], they will be merged
with any headers passed to [`response.writeHead()`][], with the headers passed
to [`response.writeHead()`][] given precedence.

```js
// returns content-type = text/plain
const server = http2.createServer((req, res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('ok');
});
```

Attempting to set a header field name or value that contains invalid characters
will result in a [`TypeError`][] being thrown.

