<!-- YAML
added: v0.9.4
-->

* `size` {number} Optional argument to specify how much data to read.
* Return {string|Buffer|null}

`readable.read（）`方法从内部缓冲区中抽出并返回一些数据。 如果没有可读的数据，返回null。`readable.read()`方法默认数据将作为“Buffer”对象返回
，除非已经使用`readable.setEncoding（）`方法设置编码或流运行在对象模式。

可选的`size`参数指定要读取的特定数量的字节。如果`size`字节不可读，将返回`null`*除非*流已经结束，在这种情况下所有保留在内部缓冲区的数据将被返回（*即使它超过`size` 字节 *）

如果没有指定`size`参数，则内部缓冲区包含的所有数据将返回。

`readable.read()`方法只应该在暂停模式下的可读流上运行。在流模式下，`readable.read()`自动调用直到内部缓冲区的数据完全耗尽。

```js
const readable = getReadableStreamSomehow();
readable.on('readable', () => {
  let chunk;
  while (null !== (chunk = readable.read())) {
    console.log(`Received ${chunk.length} bytes of data.`);
  }
});
```
一般来说，建议开发人员避免使用`'readable'`事件和`readable.read（）`方法，使用`readable.pipe()`或`'data'`事件代替。

无论`size`参数的值是什么，对象模式中的可读流将始终返回调用[`readable.read(size)`][stream-read]的单个项目。

*注意*：如果`readable.read()`方法返回一个数据块，那么一个`'data'`事件也将被发送。

*注意*：在已经被发出的[`'end'`] []事件后调用[`stream.read（[size]）`] [stream-read]事件将返回`null`。不会抛出运行时错误。
