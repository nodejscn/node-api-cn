<!-- YAML
added: v0.9.4
-->

在调用了 [`stream.end()`][stream-end] 方法，且缓冲区数据都已经传给底层系统（underlying system）之后， `'finish'` 事件将被触发。

```js
const writer = getWritableStreamSomehow();
for (let i = 0; i < 100; i++) {
  writer.write(`hello, #${i}!\n`);
}
writer.end('This is the end\n');
writer.on('finish', () => {
  console.error('All writes are now complete.');
});
```

