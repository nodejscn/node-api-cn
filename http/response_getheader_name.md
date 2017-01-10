<!-- YAML
added: v0.4.0
-->

* `name` {String}
* Returns: {String}

Reads out a header that's already been queued but not sent to the client.  Note
that the name is case insensitive.  This can only be called before headers get
implicitly flushed.

Example:

```js
var contentType = response.getHeader('content-type');
```

