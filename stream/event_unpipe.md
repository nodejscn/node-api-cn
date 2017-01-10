<!-- YAML
added: v0.9.4
-->

* `src` {[Readable][] Stream} The source stream that
  [unpiped][`stream.unpipe()`] this writable

The `'unpipe'` event is emitted when the [`stream.unpipe()`][] method is called
on a [Readable][] stream, removing this [Writable][] from its set of
destinations.

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('unpipe', (src) => {
  console.error('Something has stopped piping into the writer.');
  assert.equal(src, reader);
});
reader.pipe(writer);
reader.unpipe(writer);
```

