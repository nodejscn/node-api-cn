<!-- YAML
added: v0.9.4
-->

* `chunk` {Buffer|string|any} 数据片段。对于非对象模式的可读流，这是一个字符串或者 `Buffer`。
  对于对象模式的可读流，这可以是除 `null` 以外的任意类型 JavaScript 值。

`'data'` 事件会在流将数据传递给消费者时触发。当流转换到 flowing 模式时会触发该事件。调用 `readable.pipe()`， `readable.resume()` 方法，或为 `'data'` 事件添加回调可以将流转换到 flowing 模式。 `'data'` 事件也会在调用 `readable.read()` 方法并有数据返回时触发。

在没有明确暂停的流上添加 `'data'` 事件监听会将流转换为 flowing 模式。 数据会在可用时尽快传递给下个流程。

如果调用 `readable.setEncoding()` 方法明确为流指定了默认编码，回调函数将接收到一个字符串，否则接收到的数据将是一个
`Buffer` 实例。

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data.`);
});
```

