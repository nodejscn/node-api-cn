<!-- YAML
added: v0.9.4
-->

调用 [`stream.end()`][stream-end] 方法且缓冲数据都已经传给底层系统之后，触发 `'finish'` 事件。

```js
const writer = getWritableStreamSomehow();
for (let i = 0; i < 100; i++) {
  writer.write(`你好，#${i}!\n`);
}
writer.end('这是结尾\n');
writer.on('finish', () => {
  console.error('所有写入已完成。');
});
```

