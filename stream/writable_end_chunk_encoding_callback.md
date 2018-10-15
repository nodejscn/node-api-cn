<!-- YAML
added: v0.9.4
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18780
    description: This method now returns a reference to `writable`.
  - version: v8.0.0
    pr-url: https://github.com/nodejs/node/pull/11608
    description: The `chunk` argument can now be a `Uint8Array` instance.
-->

* `chunk` {string|Buffer|Uint8Array|any} 要写入的数据。
	对于非对象模式的流，`chunk` 必须是字符串、`Buffer`、或 `Uint8Array`。
	对于对象模式的流， `chunk` 可以是任何 JavaScript 值，除了 `null`。
* `encoding` {string} 如果 `chunk` 是字符串，则指定字符编码。
* `callback` {Function} 当流结束时的回调函数。
* 返回: {this}

调用 `writable.end()` 表明已没有数据要被写入[可写流]。
可选的 `chunk` 和 `encoding` 参数可以在关闭流之前再写入一块数据。
如果传入了 `callback` 函数，则会做为监听器添加到 [`'finish'`][] 事件。

调用 [`stream.end()`][stream-end] 之后再调用 [`stream.write()`][stream-write] 会导致错误。

```js
// 先写入 'hello, '，结束前再写入 'world!'。
const fs = require('fs');
const file = fs.createWriteStream('例子.txt');
file.write('hello, ');
file.end('world!');
// 后面不允许再写入数据！
```

