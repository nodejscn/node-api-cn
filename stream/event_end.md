<!-- YAML
added: v0.9.4
-->

当流中没有数据可供消费时触发。

`'end'` 事件只有在数据被完全消费掉后才会触发。
要想触发该事件，可以将流转换到流动模式，或反复调用 [`stream.read()`][stream-read] 直到数据被消费完。

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`接收到 ${chunk.length} 个字节的数据`);
});
readable.on('end', () => {
  console.log('已没有数据');
});
```

