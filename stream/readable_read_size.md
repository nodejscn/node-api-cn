<!-- YAML
added: v0.9.4
-->

* `size` {number} 要读取的数据的字节数。
* 返回: {string|Buffer|null|any}

从内部缓冲拉取并返回数据。
如果没有可读的数据，则返回 `null`。
默认情况下，`readable.read()` 返回的数据是 `Buffer` 对象，除非使用 `readable.setEncoding()` 指定字符编码或流处于对象模式。

可选的 `size` 参数指定要读取的特定字节数。 
如果无法读取 `size` 个字节，则除非流已结束，否则将会返回 `null`，在这种情况下，将会返回内部 buffer 中剩余的所有数据。

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

使用 `readable.read()` 处理数据时，`while` 循环是必需的。 
只有在 `readable.read()` 返回 `null` 之后，才会触发 [`'readable'`]。

对象模式下的可读流将会始终从调用 [`readable.read(size)`][stream-read] 返回单个子项，而不管 `size` 参数的值如何。

如果 `readable.read()` 返回一个数据块，则 `'data'` 事件也会触发。

在 [`'end'`] 事件触发后再调用 [`stream.read([size])`][stream-read] 会返回 `null`。
不会引发运行时错误。

