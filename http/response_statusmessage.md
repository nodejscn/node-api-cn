<!-- YAML
added: v0.11.8
-->

* {String}

When using implicit headers (not calling [`response.writeHead()`][] explicitly), this property
controls the status message that will be sent to the client when the headers get
flushed. If this is left as `undefined` then the standard message for the status
code will be used.

Example:

```js
response.statusMessage = 'Not found';
```

After response header was sent to the client, this property indicates the
status message which was sent out.

