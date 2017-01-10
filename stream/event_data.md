<!-- YAML
added: v0.9.4
-->

* `chunk` {Buffer|String|any} The chunk of data. For streams that are not
  operating in object mode, the chunk will be either a string or `Buffer`.
  For streams that are in object mode, the chunk can be any JavaScript value
  other than `null`.

The `'data'` event is emitted whenever the stream is relinquishing ownership of
a chunk of data to a consumer. This may occur whenever the stream is switched
in flowing mode by calling `readable.pipe()`, `readable.resume()`, or by
attaching a listener callback to the `'data'` event. The `'data'` event will
also be emitted whenever the `readable.read()` method is called and a chunk of
data is available to be returned.

Attaching a `'data'` event listener to a stream that has not been explicitly
paused will switch the stream into flowing mode. Data will then be passed as
soon as it is available.

The listener callback will be passed the chunk of data as a string if a default
encoding has been specified for the stream using the
`readable.setEncoding()` method; otherwise the data will be passed as a
`Buffer`.

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data.`);
});
```

