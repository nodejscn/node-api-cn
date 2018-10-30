<!-- YAML
added: v0.9.4
-->

* `size` {number} 要读取的数据的字节数。
* 返回: {string|Buffer|null|any}

从内部缓冲拉取并返回数据。
如果没有可读的数据，则返回 `null`。
默认情况下，`readable.read()` 返回的数据是 `Buffer` 对象，除非使用 `readable.setEncoding()` 指定字符编码或流处于对象模式。

如果可读的数据不足 `size` 个字节，则返回内部缓冲剩余的数据，如果流已经结束则返回 `null`。

如果没有指定 `size` 参数，则返回内部缓冲中的所有数据。

`readable.read()` 应该只对处于暂停模式的可读流调用。
在流动模式中，`readable.read()` 会自动调用直到内部缓冲的数据完全耗尽。

```js
const readable = getReadableStreamSomehow();
readable.on('readable', () => {
  let chunk;
  while (null !== (chunk = readable.read())) {
    console.log(`接收到 ${chunk.length} 字节的数据`);
  }
});
```

如果 `readable.read()` 返回一个数据块，则 `'data'`事件也会触发。

[`'end'`] 事件触发后再调用 [`stream.read([size])`][stream-read] 会返回`null`，不会抛出错误。

