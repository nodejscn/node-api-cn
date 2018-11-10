<!-- YAML
added: v0.1.31
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是一个使用 `file:` 协议的 WHATWG `URL` 对象。
                 该支持目前仍为试验性的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: 传入的 `options` 对象不会被修改。
  - version: v2.3.0
    pr-url: https://github.com/nodejs/node/pull/1845
    description: 参数 `options` 现在可以是一个字符串。
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `flags` {string} 详见[支持的文件系统标志][support of file system `flags`]。默认为 `'r'`。
  * `encoding` {string} 默认为 `null`。
  * `fd` {integer} 默认为 `null`。
  * `mode` {integer} 默认为 `0o666`。
  * `autoClose` {boolean} 默认为 `true`。
  * `start` {integer}
  * `end` {integer} 默认为 `Infinity`。
  * `highWaterMark` {integer} 默认为 `64 * 1024`。
* 返回: {fs.ReadStream} 详见[可读流][Readable Streams]。

不同于 `highWaterMark` 默认值为 16 kb 的可读流，该方法返回的流的 `highWaterMark` 默认为 64 kb。

`options` 可以包括 `start` 和 `end` 值，用于从文件读取一定范围的字节而不是整个文件。
`start` 和 `end` 都是包括在内的，且从 0 开始。
如果指定了 `fd` 且 `start` 不传或为 `undefined`，则 `fs.createReadStream()` 从当前文件位置按顺序地读取。
`encoding` 可以是任何可以被 [`Buffer`] 接受的值。

如果指定了 `fd`，则 `ReadStream` 会忽略 `path` 参数并且会使用指定的文件描述符。
这意味着不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `fd` 指向一个只支持阻塞读取（比如键盘或声卡）的字符设备，则读取操作不会结束直到有可用的数据。
这可以避免进程退出或流被关闭。

```js
const fs = require('fs');
// 从字符设备创建一个流。
const stream = fs.createReadStream('/dev/input/event0');
setTimeout(() => {
  stream.close(); // 这不会关闭流。
  // 手动地指示流已到尽头，使流关闭。
  // 这不会取消读取操作的等待，进程在读取完成前不会退出。
  stream.push(null);
  stream.read(0);
}, 100);
```

如果 `autoClose` 为 `false`，则文件描述符不会被关闭，即使有错误。
应用程序需要负责关闭它，并且确保没有文件描述符泄漏。
如果 `autoClose` 被设置为 `true`（默认），则文件描述符在 `error` 事件或 `end` 事件时会被自动关闭。

`mode` 用于设置文件模式（权限和粘滞位），但仅限创建文件时有效。

例子，从一个大小为 100 字节的文件中读取最后 10 个字节：

```js
fs.createReadStream('sample.txt', { start: 90, end: 99 });
```

如果 `options` 是一个字符串，则它指定字符编码。

