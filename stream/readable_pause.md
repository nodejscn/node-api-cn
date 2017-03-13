<!-- YAML
added: v0.9.4
-->

* 返回： `this`

`readable.pause()` 方法将会使 flowing 模式的流停止触发 [`'data'`][] 事件， 进而切出 flowing 模式。任何可用的数据都将保存在内部缓存中。

```js
const readable = getReadableStreamSomehow();
readable.on('data', (chunk) => {
  console.log(`Received ${chunk.length} bytes of data.`);
  readable.pause();
  console.log('There will be no additional data for 1 second.');
  setTimeout(() => {
    console.log('Now data will start flowing again.');
    readable.resume();
  }, 1000);
});
```

