<!-- YAML
added: v1.6.0
-->

* `name` {string}
* Returns: {string}

Reads out a header on the request. Note that the name is case insensitive.

Example:
```js
const contentType = request.getHeader('Content-Type');
```

