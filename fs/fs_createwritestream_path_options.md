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
  - version: v5.5.0
    pr-url: https://github.com/nodejs/node/pull/3679
    description: The `autoClose` option is supported now.
  - version: v2.3.0
    pr-url: https://github.com/nodejs/node/pull/1845
    description: The passed `options` object can be a string now.
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `flags` {string} 请参阅[文件系统标志的支持][support of file system `flags`]。默认为 `'w'`。
  * `encoding` {string} 默认为 `'utf8'`。
  * `fd` {integer} 默认为 `null`。文件描述符。
  * `mode` {integer} 默认为 `0o666`。
  * `autoClose` {boolean} 默认为 `true`。
  * `start` {integer}
* 返回: {fs.WriteStream} 详见[可写流][Writable Stream]。

`start` 用于写入数据到文件的指定位置。
如果要修改文件而不是覆盖文件，则 `flags` 应为 `r+` 而不是默认的 `w`。

如果 `autoClose` 设为 `true`（默认），则文件描述符在 `error` 或 `finish` 事件时会自动关闭。
如果 `autoClose` 设为 `false`，则文件描述符不会自动关闭，即使发生错误。
应用程序需要负责关闭它，并且确保没有文件描述符泄漏。

如果指定了 `fd`，则忽略 `path`。
这意味着不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `options` 是一个字符串，则指定字符编码。

