<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} 通过管道流入到可写流的来源流。

在可读流（readable stream）上调用 [`stream.pipe()`][] 方法，并在目标流向 (destinations) 中添加当前可写流 ( writable ) 时，将会在可写流上触发 `'pipe'` 事件。

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('pipe', (src) => {
  console.error('有数据正通过管道流入写入器');
  assert.equal(src, reader);
});
reader.pipe(writer);
```

