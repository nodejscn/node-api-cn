<!-- YAML
added: v8.4.0
-->

The `'trailers'` event is emitted when a block of headers associated with
trailing header fields is received. The listener callback is passed the
[HTTP/2 Headers Object][] and flags associated with the headers.

Note that this event might not be emitted if `http2stream.end()` is called
before trailers are received and the incoming data is not being read or
listened for.

```js
stream.on('trailers', (headers, flags) => {
  console.log(headers);
});
```

