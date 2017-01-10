<!-- YAML
added: v0.1.30
-->

* `statusCode` {Number}
* `statusMessage` {String}
* `headers` {Object}

Sends a response header to the request. The status code is a 3-digit HTTP
status code, like `404`. The last argument, `headers`, are the response headers.
Optionally one can give a human-readable `statusMessage` as the second
argument.

Example:

```js
var body = 'hello world';
response.writeHead(200, {
  'Content-Length': Buffer.byteLength(body),
  'Content-Type': 'text/plain' });
```

This method must only be called once on a message and it must
be called before [`response.end()`][] is called.

If you call [`response.write()`][] or [`response.end()`][] before calling this,
the implicit/mutable headers will be calculated and call this function for you.

When headers have been set with [`response.setHeader()`][], they will be merged with
any headers passed to [`response.writeHead()`][], with the headers passed to
[`response.writeHead()`][] given precedence.

```js
// returns content-type = text/plain
const server = http.createServer((req,res) => {
  res.setHeader('Content-Type', 'text/html');
  res.setHeader('X-Foo', 'bar');
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('ok');
});
```

Note that Content-Length is given in bytes not characters. The above example
works because the string `'hello world'` contains only single byte characters.
If the body contains higher coded characters then `Buffer.byteLength()`
should be used to determine the number of bytes in a given encoding.
And Node.js does not check whether Content-Length and the length of the body
which has been transmitted are equal or not.

Attempting to set a header field name or value that contains invalid characters
will result in a [`TypeError`][] being thrown.

