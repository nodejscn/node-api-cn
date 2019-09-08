<!-- YAML
added: v0.1.31
changes:
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/29212
    description: Enable `emitClose` option.
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/19898
    description: Impose new restrictions on `start` and `end`, throwing
                 more appropriate errors in cases when we cannot reasonably
                 handle the input values.
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
  * `flags` {string} 参阅[支持的文件系统标志][support of file system `flags`]。**默认值:** `'r'`。
  * `encoding` {string} **默认值:** `null`。
  * `fd` {integer} **默认值:** `null`。
  * `mode` {integer} **默认值:** `0o666`。
  * `autoClose` {boolean} **默认值:** `true`。
  * `emitClose` {boolean} **默认值:** `false`。
  * `start` {integer}
  * `end` {integer} **默认值:** `Infinity`。
  * `highWaterMark` {integer} **默认值:** `64 * 1024`。
* 返回: {fs.ReadStream}

与用于可读流的 16 kb 的默认的 `highWaterMark` 不同，此方法返回的流具有 64 kb 的默认的 `highWaterMark`。

`options` 可以包括 `start` 和 `end` 值，以从文件中读取一定范围的字节而不是整个文件。 
`start` 和 `end` 都包含在内并从 0 开始计数，允许的值在 [0, [`Number.MAX_SAFE_INTEGER`]] 的范围内。
如果指定了 `fd` 并且省略 `start` 或为 `undefined`，则 `fs.createReadStream()` 从当前的文件位置开始顺序地读取。
`encoding` 可以是 [`Buffer`] 接受的任何一种字符编码。

如果指定了 `fd`，则 `ReadStream` 将会忽略 `path` 参数并将会使用指定的文件描述符。
这意味着将不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `fd` 指向仅支持阻塞读取的字符设备（例如键盘或声卡），则在数据可用之前，读取操作不会完成。
这可以防止进程退出并且流自然地关闭。

默认情况下，流在销毁后将不会触发 `'close'` 事件。 
这与其他 `Readable` 流的默认行为相反。 
将 `emitClose` 选项设置为 `true` 可更改此行为。

```js
const fs = require('fs');
// 从某个字符设备创建一个流。
const stream = fs.createReadStream('/dev/input/event0');
setTimeout(() => {
  stream.close(); // 这可能不会关闭流。
  // 人工标记流的结束，就像底层的资源自身已表明文件的结束一样，允许流进行关闭。
  // 这不会取消挂起中的读取操作，如果存在此类操作，则过程可能仍无法成功地退出，直到完成。
  stream.push(null);
  stream.read(0);
}, 100);
```

如果 `autoClose` 为 `false`，则即使出现错误，文件描述符也不会被关闭。
应用程序负责关闭它并确保没有文件描述符泄漏。
如果 `autoClose` 设为 `true`（默认的行为），则在 `'error'` 或 `'end'` 事件时文件描述符将会被自动地关闭。

`mode` 用于设置文件模式（权限和粘滞位），但仅限于创建文件时。

示例，从一个大小为 100 个字节的文件中读取最后 10 个字节：

```js
fs.createReadStream('sample.txt', { start: 90, end: 99 });
```

如果 `options` 是字符串，则它指定字符编码。

