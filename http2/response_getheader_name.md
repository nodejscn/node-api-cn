<!-- YAML
added: v8.4.0
-->

* `name` {string}
* Returns: {string}

Reads out a header that has already been queued but not sent to the client.
The name is case-insensitive.

```js
const contentType = response.getHeader('content-type');
```

