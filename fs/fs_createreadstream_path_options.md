<!-- YAML
added: v0.1.31
changes:
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/29212
    description: 启用 `emitClose` 选项。
  - version: v11.0.0
    pr-url: https://github.com/nodejs/node/pull/19898
    description: 对 `start` 和 `end` 施加新的约束，当无法合理地处理输入的值时，则抛出更恰当的错误。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: 传入的 `options` 对象无法再被修改。
  - version: v2.3.0
    pr-url: https://github.com/nodejs/node/pull/1845
    description: 传入的 `options` 对象可以是字符串。
  - version: v13.6.0
    pr-url: https://github.com/nodejs/node/pull/29083
    description: 选项 `fs` 可以重写使用的 `fs` 实现。
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `flags` {string} 参见[文件系统 `flag` 的支持][support of file system `flags`]。
     **默认值:** `'r'`。
  * `encoding` {string} **默认值:** `null`。
  * `fd` {integer} **默认值:** `null`。
  * `mode` {integer} **默认值:** `0o666`。
  * `autoClose` {boolean} **默认值:** `true`。
  * `emitClose` {boolean} **默认值:** `false`。
  * `start` {integer}
  * `end` {integer} **默认值:** `Infinity`。
  * `highWaterMark` {integer} **默认值:** `64 * 1024`。
  * `fs` {Object|null} **默认值:** `null`。
* 返回: {fs.ReadStream} 参见[可读流][Readable Stream]。

与可读流的 16 kb 的默认 `highWaterMark` 不同，此方法返回的流具有 64 kb 的默认 `highWaterMark`。

`options` 可以包括 `start` 和 `end` 值，用于从文件中读取一定范围的字节，而不是读取整个文件。 
`start` 和 `end` 都是包含的，并且从 0 开始计数，允许的值在 [0, [`Number.MAX_SAFE_INTEGER`]] 的范围内。
如果指定了 `fd`，并且省略 `start` 或为 `undefined`，则 `fs.createReadStream()` 会从当前的文件位置继续读取。
`encoding` 可以是能被 [`Buffer`] 接受的任何一种字符编码。

如果指定了 `fd`，则 `ReadStream` 会忽略 `path` 参数，并且会使用指定的文件描述符。
这意味着不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `fd` 指向仅支持阻塞读取的字符设备（例如键盘或声卡），则在数据可用之前，读取操作不会结束。
这可以防止进程的退出与流的自动关闭。

默认情况下，流被销毁之后不会触发 `'close'` 事件。
这与其他 `Readable` 流的默认设置是相反的。
设置 `emitClose` 选项为 `true` 可以更改此行为。

通过提供 `fs` 选项，可以重写对应的 `fs` 实现（用于 `open`、`read` 和 `close`）。 
当提供 `fs` 选项时，则必须重写 `open`、`read` 和 `close`。

```js
const fs = require('fs');
// 从某个字符设备创建流。
const stream = fs.createReadStream('设备');
setTimeout(() => {
  stream.close(); // 这可能不会关闭流。
  // 手动标记流的结束，就像底层的资源自身已表明文件的结束一样，使得流可以关闭。
  // 这不会取消待处理的读取操作，如果存在此类操作，则进程可能仍无法成功地退出，直到完成。
  stream.push(null);
  stream.read(0);
}, 100);
```

如果 `autoClose` 为 false，则即使发生错误，文件描述符也不会被关闭。
应用程序需要负责关闭它并确保没有文件描述符泄漏。
如果 `autoClose` 被设置为 true（默认的行为），则当 `'error'` 或 `'end'` 事件时，文件描述符会被自动地关闭。

`mode` 用于设置文件模式（权限和粘滞位），但仅限于文件被创建时。

示例，读取文件（长度为 100 个字节）的最后 10 个字节：

```js
fs.createReadStream('文件', { start: 90, end: 99 });
```

如果 `options` 是字符串，则它指定字符编码。

