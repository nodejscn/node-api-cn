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
  - version: v5.5.0
    pr-url: https://github.com/nodejs/node/pull/3679
    description: 支持 `autoClose` 选项。
  - version: v2.3.0
    pr-url: https://github.com/nodejs/node/pull/1845
    description: 参数 `options` 现在可以是一个字符串。
-->

* `path` {string|Buffer|URL}
* `options` {string|Object}
  * `flags` {string} 详见[支持的文件系统flag]。默认为 `'w'`。
  * `encoding` {string} 默认为 `'utf8'`。
  * `fd` {integer} 默认为 `null`。
  * `mode` {integer} 默认为 `0o666`。
  * `autoClose` {boolean} 默认为 `true`。
  * `start` {integer}
* 返回: {fs.WriteStream} 详见[可写流]。

`options` 也有 `start` 选项，用于写入数据到文件指定位置。
如果是修改文件而不是覆盖它，则 `flags` 模式需为 `r+` 模式而不是默认的 `w` 模式。
`encoding` 可以是任何可以被 [`Buffer`] 接受的值。

如果 `autoClose` 被设置为 `true`（默认），则在 `error` 或 `finish` 时，文件描述符会被自动关闭。
如果 `autoClose` 为 `false`，则文件描述符不会被关闭，即使有错误。
应用程序需要负责关闭它，并且确保没有文件描述符泄漏。

类似 [`ReadStream`]，如果指定了 `fd`，则 `WriteStream` 会忽略 `path` 参数并且会使用指定的文件描述符。
这意味着不会触发 `'open'` 事件。
`fd` 必须是阻塞的，非阻塞的 `fd` 应该传给 [`net.Socket`]。

如果 `options` 是一个字符串，则它指定字符编码。

