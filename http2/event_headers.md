<!-- YAML
added: v8.4.0
-->

The `'headers'` event is emitted when an additional block of headers is received
for a stream, such as when a block of `1xx` informational headers are received.
The listener callback is passed the [Headers Object][] and flags associated with
the headers.

```js
stream.on('headers', (headers, flags) => {
  console.log(headers);
});
```

