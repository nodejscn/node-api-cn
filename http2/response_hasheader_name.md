<!-- YAML
added: v8.4.0
-->

* `name` {string}
* Returns: {boolean}

Returns `true` if the header identified by `name` is currently set in the
outgoing headers. The header name matching is case-insensitive.

```js
const hasContentType = response.hasHeader('content-type');
```

