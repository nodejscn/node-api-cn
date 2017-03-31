<!-- YAML
added: v0.9.4
-->

* `src` {[Readable][] Stream} [unpiped][`stream.unpipe()`] 当前可写流的源流

在 [Readable][] 上调用 [`stream.unpipe()`][] 方法，从目标流向中移除当前 [Writable][] 时，将会触发 `'unpipe'` 事件。

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

