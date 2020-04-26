<!-- YAML
added: v0.1.31
changes:
  - version: v12.10.0
    pr-url: https://github.com/nodejs/node/pull/29212
    description: 启用 `emitClose` 选项。
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: 参数 `path` 可以是 WHATWG `URL` 对象（使用 `file:` 协议）。 
      该支持目前仍是实验的。
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: 传入的 `options` 对象无法再被修改。
  - version: v5.5.0
    pr-url: https://github.com/nodejs/node/pull/3679
    description: 支持 `autoClose` 选项。
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
     **默认值:** `'w'`。
  * `encoding` {string} **默认值:** `'utf8'`。
  * `fd` {integer} **默认值:** `null`。
  * `mode` {integer} **默认值:** `0o666`。
  * `autoClose` {boolean} **默认值:** `true`。
  * `emitClose` {boolean} **默认值:** `false`。
  * `start` {integer}
  * `fs` {Object|null} **默认值:** `null`。
* 返回: {fs.WriteStream} 参见[可写流][Writable Stream]。

`options` 还可以包括 `start` 选项，用于写入数据到文件开头之后的某个位置，允许的值在 [0, [`Number.MAX_SAFE_INTEGER`]] 的范围内。
若要修改文件而不是覆盖文件，则需要 `flags` 选项被设置为 `r+` 而不是默认的 `w`。
`encoding` 可以是能被 [`Buffer`] 接受的任何一种字符编码。

如果 `autoClose` 被设置为 true（默认的行为），则当 `'error'` 或 `'finish'` 事件时，文件描述符会被自动地关闭。
如果 `autoClose` 为 false，则即使发生错误，文件描述符也不会被关闭。
应用程序需要负责关闭它并确保没有文件描述符泄漏。

默认情况下，流被销毁之后不会触发 `'close'` 事件。
这与其他 `Writable` 流的默认设置是相反的。
设置 `emitClose` 选项为 `true` 可以更改此行为。

通过提供 `fs` 选项，可以重写对应的 `fs` 实现（用于 `open`、`write`、`writev` 和 `close`）。 
如果重写 `write()` 但没有重写 `writev()`，则会降低性能，因为某些优化（`_writev()`）会被禁用。 
当提供 `fs` 选项时，则必须重写 `open`、`close`、以及 `write` 和 `writev` 两者至少其中之一。

与 [`ReadStream`] 一样，如果指定了 `fd`，则 [`WriteStream`] 会忽略 `path` 参数，并且会使用指定的文件描述符。
这意味着不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `options` 是字符串，则它指定字符编码。

