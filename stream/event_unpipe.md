<!-- YAML
added: v0.9.4
-->

* `src` {stream.Readable} [被移除写入管道][`stream.unpipe()`]的来源流。

当在[可读流]上调用 [`stream.unpipe()`] 方法从目标流向中移除当前[可写流]时，触发 `'unpipe'` 事件。

当可读流通过管道流向可写流发生错误时，也会触发 `'unpipe'` 事件。

```js
const writer = getWritableStreamSomehow();
const reader = getReadableStreamSomehow();
writer.on('unpipe', (src) => {
  console.error('已停止写入流的管道。');
  assert.equal(src, reader);
});
reader.pipe(writer);
reader.unpipe(writer);
```

