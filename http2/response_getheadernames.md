<!-- YAML
added: v8.4.0
-->

* Returns: {Array}

Returns an array containing the unique names of the current outgoing headers.
All header names are lowercase.

Example:

```js
response.setHeader('Foo', 'bar');
response.setHeader('Set-Cookie', ['foo=bar', 'bar=baz']);

const headerNames = response.getHeaderNames();
// headerNames === ['foo', 'set-cookie']
```

