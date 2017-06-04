<!-- YAML
added: v0.9.4
-->

* `destination` {stream.Writable} 数据写入目标
* `options` {Object} Pipe 选项
  * `end` {boolean} 在 reader 结束时结束 writer 。默认为 `true`。

`readable.pipe()` 绑定一个 [Writable][] 到 `readable` 上，
将可写流自动切换到 flowing 模式并将所有数据传给绑定的 [Writable][]。数据流将被自动管理。这样，即使是可读流较快，目标可写流也不会超负荷（overwhelmed）。

下面例子将 `readable` 中的所有数据通过管道传递给名为 `file.txt` 的文件：

```js
const readable = getReadableStreamSomehow();
const writable = fs.createWriteStream('file.txt');
// readable 中的所有数据都传给了 'file.txt'
readable.pipe(writable);
```
可以在单个可读流上绑定多个可写流。

`readable.pipe()` 方法返回 *目标流* 的引用，这样就可以对流进行链式地管道操作：

```js
const r = fs.createReadStream('file.txt');
const z = zlib.createGzip();
const w = fs.createWriteStream('file.txt.gz');
r.pipe(z).pipe(w);
```

默认情况下，当源可读流（the source Readable stream）触发 [`'end'`][] 事件时，目标流也会调用 [`stream.end()`][stream-end] 方法从而结束写入。要禁用这一默认行为， `end`
选项应该指定为 `false`， 这将使目标流保持打开，
如下面例子所示：

```js
reader.pipe(writer, { end: false });
reader.on('end', () => {
  writer.end('Goodbye\n');
});
```

这里有一点要警惕，如果可读流在处理时发生错误，目标可写流 *不会* 自动关闭。
如果发生错误，需要 *手动* 关闭所有流以避免内存泄漏。

*注意*：不管对 [`process.stderr`][] 和 [`process.stdout`][] 指定什么选项，它们都是直到 Node.js 进程退出才关闭。

