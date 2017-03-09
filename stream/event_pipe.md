<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} 输出到目标可写流（writable）的源流（source stream）

在可读流（readable stream）上调用 [`stream.pipe()`][] 方法，并在目标流向 (destinations) 中添加当前可写流 ( writable ) 时，将会在可写流上触发 `'pipe'` 事件。

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('pipe', (src) => {
  console.error('something is piping into the writer');
  assert.equal(src, reader);
});
reader.pipe(writer);
```

