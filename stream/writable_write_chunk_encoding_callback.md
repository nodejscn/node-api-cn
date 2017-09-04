<!-- YAML
added: v0.9.4
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
  - version: v6.0.0
    pr-url: https://github.com/nodejs/node/pull/6170
    description: Passing `null` as the `chunk` parameter will always be
                 considered invalid now, even in object mode.
-->

* `chunk` {string|Buffer|Uint8Array|any} 要写入的数据。可选的。
  对于非对象模式下的流， `chunk` 必须是字符串， `Buffer` 或者
  `Uint8Array`。对于对象模式下的流，`chunk` 可以是除 `null` 外的任意 JavaScript 值。
* `encoding` {string} 如果 `chunk` 是字符串，这里指定字符编码
* `callback` {Function} 缓冲数据输出时的回调函数
* 返回： {boolean} 如果流需要等待 `'drain'` 事件触发才能继续写入数据，这里将返回 `false` ； 否则返回 `true`。

`writable.write()` 方法向流中写入数据，并在数据处理完成后调用 `callback` 。如果有错误发生， `callback` *不一定* 以这个错误作为第一个参数并被调用。要确保可靠地检测到写入错误，应该监听
`'error'` 事件。

在确认了 `chunk` 后，如果内部缓冲区的大小小于创建流时设定的 `highWaterMark` 阈值，函数将返回 `true` 。
如果返回值为 `false` ，应该停止向流中写入数据，直到 [`'drain'`][] 事件被触发。

当一个流不处在 drain 的状态， 对 `write()` 的调用会缓存数据块， 并且返回 false。
一旦所有当前所有缓存的数据块都排空了（被操作系统接受来进行输出）， 那么 `'drain'` 事件就会被触发。
我们建议， 一旦 write() 返回 false， 在 `'drain'` 事件触发前， 不能写入任何数据块。 
然而，当流不处在 `'drain'` 状态时， 调用 `write()` 是被允许的， Node.js 会缓存所有已经写入的数据块， 
直到达到最大内存占用， 这时它会无条件中止。 甚至在它中止之前， 高内存占用将会导致差的垃圾回收器的性能和高的系统相对敏感性
（即使内存不再需要，也通常不会被释放回系统）。 如果远程的另一端没有读取数据， TCP sockets 可能永远也不会 drain ， 
所以写入到一个不会drain的socket可能会导致远程可利用的漏洞。 

对于一个 [Transform][], 写入数据到一个不会drain的流尤其成问题， 因为 `Transform` 流默认被暂停， 直到它们被pipe或者被添加了
 `'data'` 或 `'readable'` 事件处理函数。 

如果将要被写入的数据可以根据需要生成或者取得，我们建议将逻辑封装为一个 [Readable][] 流并且使用 
[`stream.pipe()`][]。 但是如果调用 `write()` 优先, 那么可以使用 [`'drain'`][] 事件来防止回压并且避免内存问题:

```js
function write(data, cb) {
  if (!stream.write(data)) {
    stream.once('drain', cb);
  } else {
    process.nextTick(cb);
  }
}

// 在回调函数被执行后再进行其他的写入
write('hello', () => {
  console.log('write completed, do more writes now');
});
```

对象模式的写入流将忽略 `encoding` 参数。

