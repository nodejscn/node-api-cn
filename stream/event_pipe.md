<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} 通过管道流入到可写流的来源流。

当在可读流上调用 [`stream.pipe()`] 时触发。

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('pipe', (src) => {
  console.error('有数据正通过管道流入写入器');
  assert.equal(src, reader);
});
reader.pipe(writer);
```

