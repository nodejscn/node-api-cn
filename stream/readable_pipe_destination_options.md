<!-- YAML
added: v0.9.4
-->

* `destination` {stream.Writable} 数据写入的目标。
* `options` {Object} 选项。
  * `end` {boolean} 当读取器结束时终止写入器。默认为 `true`。
* 返回: {stream.Writable} 目标可写流，如果是 [`Duplex`] 流或 [`Transform`] 流则可以形成管道链。

绑定可写流到可读流，将可读流自动切换到流动模式，并将可读流的所有数据推送到绑定的可写流。
数据流会被自动管理，所以即使可读流更快，目标可写流也不会超负荷。

例子，将可读流的所有数据通过管道推送到 `file.txt` 文件：

```js
const readable = getReadableStreamSomehow();
const writable = fs.createWriteStream('file.txt');
// readable 的所有数据都推送到 'file.txt'。
readable.pipe(writable);
```
可以在单个可读流上绑定多个可写流。

`readable.pipe()` 会返回目标流的引用，这样就可以对流进行链式地管道操作：

```js
const fs = require('fs');
const r = fs.createReadStream('file.txt');
const z = zlib.createGzip();
const w = fs.createWriteStream('file.txt.gz');
r.pipe(z).pipe(w);
```

默认情况下，当来源可读流触发 [`'end'`] 事件时，目标可写流也会调用 [`stream.end()`][stream-end] 结束写入。
若要禁用这种默认行为，`end` 选项应设为 `false`，这样目标流就会保持打开：

```js
reader.pipe(writer, { end: false });
reader.on('end', () => {
  writer.end('结束');
});
```

如果可读流发生错误，目标可写流不会自动关闭，需要手动关闭所有流以避免内存泄漏。

