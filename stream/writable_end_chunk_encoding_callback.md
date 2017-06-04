<!-- YAML
added: v0.9.4
changes:
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
-->

* `chunk` {string|Buffer|Uint8Array|any} 可选的，需要写入的数据。对于非对象模式下的流， `chunk` 必须是字符串、或 `Buffer`、或 `Uint8Array`。对于对象模式下的流， `chunk` 可以是任意的 JavaScript 值，除了 `null`。
* `encoding` {string} 如果 `chunk` 是字符串，这里指定字符编码。
* `callback` {Function} 可选的，流结束时的回调函数。

调用 `writable.end()` 方法表明接下来没有数据要被写入 [Writable][]。通过传入可选的 `chunk` 和 `encoding` 参数，可以在关闭流之前再写入一段数据。如果传入了可选的 `callback` 函数，它将作为 [`'finish'`][] 事件的回调函数。

在调用了 [`stream.end()`][stream-end] 方法之后，再调用 [`stream.write()`][stream-write] 方法将会导致错误。

```js
// 写入 'hello, ' ，并用 'world!' 来结束写入
const file = fs.createWriteStream('example.txt');
file.write('hello, ');
file.end('world!');
// 后面不允许再写入数据！
```

