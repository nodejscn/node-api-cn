<!-- YAML
added: v8.4.0
-->

* `name` {string}
* `value` {string | string[]}

Sets a single header value for implicit headers.  If this header already exists
in the to-be-sent headers, its value will be replaced.  Use an array of strings
here to send multiple headers with the same name.

Example:

```js
response.setHeader('Content-Type', 'text/html');
```

or

```js
response.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
```

Attempting to set a header field name or value that contains invalid characters
will result in a [`TypeError`][] being thrown.

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

