<!-- YAML
added: v8.4.0
-->

* `name` {string}
* Returns: {string}

Reads out a header that has already been queued but not sent to the client.
Note that the name is case insensitive.

Example:

```js
const contentType = response.getHeader('content-type');
```

