<!-- YAML
added: v0.9.4
-->

* `chunk` {String|Buffer} 要写入的数据
* `encoding` {String} 如果 `chunk` 是字符串，这里指定字符编码
* `callback` {Function} 缓冲数据输出时的回调函数
* 返回： {Boolean} 如果流需要等待 `'drain'` 事件触发才能继续写入数据，这里将返回 `false` ； 否则返回 `true`。

`writable.write()` 方法向流中写入数据，并在数据处理完成后调用 `callback` 。如果有错误发生， `callback` *不一定* 会接收到这个错误作为第一个参数。要确保可靠地检测到写入错误，应该监听
`'error'` 事件。

在确认了 `chunk` 后，如果内部缓冲区的大小小于创建流时设定的 `highWaterMark` 阈值，函数将返回 `true` 。
如果返回值为 `false` ，应该停止向流中写入数据，直到 [`'drain'`][] 事件被触发。

While a stream is not draining, calls to `write()` will buffer `chunk`, and
return false. Once all currently buffered chunks are drained (accepted for
delivery by the operating system), the `'drain'` event will be emitted.
It is recommended that once write() returns false, no more chunks be written
until the `'drain'` event is emitted. While calling `write()` on a stream that
is not draining is allowed, Node.js will buffer all written chunks until
maximum memory usage occurs, at which point it will abort unconditionally.
Even before it aborts, high memory usage will cause poor garbage collector
performance and high RSS (which is not typically released back to the system,
even after the memory is no longer required). Since TCP sockets may never
drain if the remote peer does not read the data, writing a socket that is
not draining may lead to a remotely exploitable vulnerability.

Writing data while the stream is not draining is particularly
problematic for a [Transform][], because the `Transform` streams are paused
by default until they are piped or an `'data'` or `'readable'` event handler
is added.

If the data to be written can be generated or fetched on demand, it is
recommended to encapsulate the logic into a [Readable][] and use
[`stream.pipe()`][]. However, if calling `write()` is preferred, it is
possible to respect backpressure and avoid memory issues using the
the [`'drain'`][] event:

```js
function write (data, cb) {
  if (!stream.write(data)) {
    stream.once('drain', cb)
  } else {
    process.nextTick(cb)
  }
}

// Wait for cb to be called before doing any other write.
write('hello', () => {
  console.log('write completed, do more writes now')
})
```

对象模式的写入流将忽略 `encoding` 参数。

