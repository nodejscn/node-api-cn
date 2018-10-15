<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} [被移除可写流管道][`stream.unpipe()`]的来源流。

当在可读流上调用 [`stream.unpipe()`] 时触发。

当可读流通过管道流向可写流发生错误时，也会触发 `'unpipe'` 事件。

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('unpipe', (src) => {
  console.error('已移除可写流管道');
  assert.equal(src, reader);
});
reader.pipe(writer);
reader.unpipe(writer);
```

