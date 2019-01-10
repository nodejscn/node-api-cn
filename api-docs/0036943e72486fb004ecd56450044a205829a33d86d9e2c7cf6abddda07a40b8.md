<!-- YAML
added: v0.9.4
-->

* `chunk` {Buffer|string|any} 数据块。
  对于非对象模式的流， `chunk` 可以是字符串或 `Buffer`。
  对于对象模式的流，`chunk` 可以是任何 JavaScript 值，除了 `null`。

当流将数据块传送给消费者后触发。
当调用 `readable.pipe()`，`readable.resume()` 或绑定监听器到 `'data'` 事件时，流会转换到流动模式。
当调用 `readable.read()` 且有数据块返回时，也会触发 `'data'` 事件。

如果使用 `readable.setEncoding()` 为流指定了默认的字符编码，则监听器回调传入的数据为字符串，否则传入的数据为 `Buffer`。

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`接收到 ${chunk.length} 个字节的数据`);
});
```

