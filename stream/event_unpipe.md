<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} 要[移除][`stream.unpipe()`]可写流管道的来源流。

在可读流上调用 [`stream.unpipe()`] 方法时会发出 `'unpipe'`事件，从其目标集中移除此可写流。

当可读流通过管道流向可写流发生错误时，也会触发此事件。

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('unpipe', (src) => {
  console.log('已移除可写流管道');
  assert.equal(src, reader);
});
reader.pipe(writer);
reader.unpipe(writer);
```

