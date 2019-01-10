<!-- YAML
added: v0.9.4
-->

调用 [`stream.end()`][stream-end] 且缓冲数据都已传给底层系统之后触发。

```js
const writer = getWritableStreamSomehow();
for (let i = 0; i < 100; i++) {
  writer.write(`写入 #${i}!\n`);
}
writer.end('写入结尾\n');
writer.on('finish', () => {
  console.error('写入已完成');
});
```

