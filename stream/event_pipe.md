<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} 通过管道流入到可写流的来源流。

当在可读流上调用 [`stream.pipe()`] 方法时会发出 `'pipe'` 事件，并将此可写流添加到其目标集。

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('pipe', (src) => {
  console.log('有数据正通过管道流入写入器');
  assert.equal(src, reader);
});
reader.pipe(writer);
```

