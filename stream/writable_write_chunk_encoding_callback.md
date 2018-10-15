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

* `chunk` {string|Buffer|Uint8Array|any} 要写入的数据。
  对于非对象模式的流，`chunk` 必须是字符串、`Buffer` 或 `Uint8Array`。
  对于对象模式的流，`chunk` 可以是任何 JavaScript 值，除了 `null`。
* `encoding` {string} 如果 `chunk` 是字符串，则指定字符编码。
* `callback` {Function} 当数据块被输出到目标后的回调函数。
* 返回: {boolean} 如果流需要等待 `'drain'` 事件触发才能继续写入更多数据，则返回 `false`，否则返回 `true`。

`writable.write()` 写入数据到流，并在数据被完全处理之后调用 `callback`。
如果发生错误，则 `callback` 可能被调用也可能不被调用。
为了可靠地检测错误，可以为 `'error'` 事件添加监听器。

在接收了 `chunk` 后，如果内部的缓冲小于创建流时配置的 `highWaterMark`，则返回 `true` 。
如果返回 `false` ，则应该停止向流写入数据，直到 [`'drain'`][] 事件被触发。

当流还未被排空时，调用 `write()` 会缓冲 `chunk`，并返回 `false`。
一旦所有当前缓冲的数据块都被排空了（被操作系统接收并传输），则触发 `'drain'` 事件。
建议一旦 `write()` 返回 false，则不再写入任何数据块，直到 `'drain'` 事件被触发。 
当流还未被排空时，也是可以调用 `write()`，Node.js 会缓冲所有被写入的数据块，直到达到最大内存占用，这时它会无条件中止。 
甚至在它中止之前， 高内存占用将会导致垃圾回收器的性能变差和 RSS 变高（即使内存不再需要，通常也不会被释放回系统）。 
如果远程的另一端没有读取数据，TCP 的 socket 可能永远也不会排空，所以写入到一个不会排空的 socket 可能会导致远程可利用的漏洞。 

对于 [`Transform`][], 写入数据到一个不会排空的流尤其成问题，因为 `Transform` 流默认会被暂停，直到它们被 pipe 或者添加了 `'data'` 或 `'readable'` 事件句柄。 

如果要被写入的数据可以根据需要生成或者取得，建议将逻辑封装为一个[可读流]并且使用 [`stream.pipe()`][]。
如果要优先调用 `write()`，则可以使用 [`'drain'`][] 事件来防止背压与避免内存问题:

```js
function write(data, cb) {
  if (!stream.write(data)) {
    stream.once('drain', cb);
  } else {
    process.nextTick(cb);
  }
}

// 在回调函数被执行后再进行其他的写入。
write('hello', () => {
  console.log('完成写入，可以进行更多的写入');
});
```

