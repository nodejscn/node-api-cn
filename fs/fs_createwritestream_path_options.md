<!-- YAML
added: v0.1.31
-->

* `path` {String | Buffer}
* `options` {String | Object}
  * `flags` {String}
  * `defaultEncoding` {String}
  * `fd` {Integer}
  * `mode` {Integer}
  * `autoClose` {Boolean}
  * `start` {Integer}

返回一个新建的 [`WriteStream`] 对象（详见[可写流]）。

`options` 是一个带有以下默认值的对象或字符串：

```js
{
  flags: 'w',
  defaultEncoding: 'utf8',
  fd: null,
  mode: 0o666,
  autoClose: true
}
```

`options` 也可以包括一个 `start` 选项，使其可以写入数据到文件某个位置。
如果是修改一个文件而不是覆盖它，则需要`flags` 模式为 `r+` 而不是默认的 `w` 模式。
`defaultEncoding` 可以是任何可以被 [`Buffer`] 接受的值。

如果 `autoClose` 被设置为 `true`（默认），则在 `error` 或 `end` 时，文件描述符会被自动关闭。
如果 `autoClose` 为 `false`，则文件描述符不会被关闭，即使有错误。
你需要负责关闭它，并且确保没有文件描述符泄漏。

类似 [`ReadStream`]，如果指定了 `fd`，则 `WriteStream` 会忽略 `path` 参数并且会使用指定的文件描述符。
这意味着不会触发 `'open'` 事件。
注意，`fd` 应该是阻塞的；非阻塞的 `fd` 们应该传给 [`net.Socket`]。

如果 `options` 是一个字符串，则它指定了字符编码。

