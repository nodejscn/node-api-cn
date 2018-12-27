<!-- YAML
added: v0.1.31
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `path` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: The passed `options` object will never be modified.
  - version: v2.3.0
    pr-url: https://github.com/nodejs/node/pull/1845
    description: The passed `options` object can be a string now.
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `flags` {string} 详见[支持的 flag][support of file system `flags`]。默认为 `'r'`。
  * `encoding` {string} 默认为 `null`。
  * `fd` {integer} 默认为 `null`。文件描述符。
  * `mode` {integer} 默认为 `0o666`。
  * `autoClose` {boolean} 默认为 `true`。
  * `start` {integer}
  * `end` {integer} 默认为 `Infinity`。
  * `highWaterMark` {integer} 默认为 `64 * 1024`。
* 返回: {fs.ReadStream} 详见[可读流][Readable Streams]。

可读流的 `highWaterMark` 一般默认为 16 kb，但本方法返回的可读流默认为 64 kb。

`start` 与 `end` 用于从文件读取指定范围的字节。
`start` 与 `end` 都是包括在内的。
如果指定了 `fd` 且不指定 `start`，则从当前位置开始读取。

如果指定了 `fd`，则忽略 `path`。
这意味着不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `fd` 是一个只支持阻塞读取（比如键盘或声卡）的字符设备，则读取操作在读取到数据之前不会结束。
这可以避免进程退出或者流被关闭。

```js
const fs = require('fs');
// 从字符设备创建可读流。
const stream = fs.createReadStream('/dev/input/event0');
setTimeout(() => {
  stream.close(); // 这不会关闭流。
  // 必须手动地指示流已到尽头，流才会关闭。
  // 这不会取消读取操作的等待，进程在读取完成前不会退出。
  stream.push(null);
  stream.read(0);
}, 100);
```

如果 `autoClose` 设为 `false`，则文件描述符不会自动关闭，即使发生错误。
应用程序需要负责关闭它，并且确保没有文件描述符泄漏。
如果 `autoClose` 设为 `true`（默认），则文件描述符在 `error` 或 `end` 事件时会自动关闭。

`mode` 用于设置文件模式（权限），但仅限创建文件时有效。

例子，从一个大小为 100 字节的文件中读取最后 10 个字节：

```js
fs.createReadStream('sample.txt', { start: 90, end: 99 });
```

如果 `options` 是一个字符串，则指定字符编码。

