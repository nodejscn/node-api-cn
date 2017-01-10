<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} source stream that is piping to this writable

The `'pipe'` event is emitted when the [`stream.pipe()`][] method is called on
a readable stream, adding this writable to its set of destinations.

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('pipe', (src) => {
  console.error('something is piping into the writer');
  assert.equal(src, reader);
});
reader.pipe(writer);
```

