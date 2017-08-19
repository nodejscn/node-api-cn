<!-- YAML
added: v8.4.0
-->

The `'trailers'` event is emitted when a block of headers associated with
trailing header fields is received. The listener callback is passed the
[Headers Object][] and flags associated with the headers.

```js
stream.on('trailers', (headers, flags) => {
  console.log(headers);
});
```

