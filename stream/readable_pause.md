<!-- YAML
added: v0.9.4
-->

* 返回: {this}

使流动模式的流停止触发 [`'data'`] 事件，并切换出流动模式。
任何可用的数据都会保留在内部缓存中。

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`接收到 ${chunk.length} 字节的数据`);
  readable.pause();
  console.log('暂停一秒');
  setTimeout(() => {
    console.log('数据重新开始流动');
    readable.resume();
  }, 1000);
});
```

如果存在 `'readable'` 事件监听器，则该方法不起作用。

