<!-- YAML
added: v1.6.0
-->

* `name` {string}
* `value` {string}

Sets a single header value for headers object. If this header already exists in
the to-be-sent headers, its value will be replaced. Use an array of strings
here to send multiple headers with the same name.

Example:
```js
request.setHeader('Content-Type', 'application/json');
```

or

```js
request.setHeader('Set-Cookie', ['type=ninja', 'language=javascript']);
```

