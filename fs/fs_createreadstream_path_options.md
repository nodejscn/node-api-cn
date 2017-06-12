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
  * `flags` {string}
  * `encoding` {string}
  * `fd` {integer}
  * `mode` {integer}
  * `autoClose` {boolean}
  * `start` {integer}
  * `end` {integer}

返回一个新建的 [`ReadStream`] 对象（详见[可读流]）。

不同于在一个可读流上设置的 `highWaterMark` 默认值（16 kb），该方法在相同参数下返回的流具有 64 kb 的默认值。

`options` 是一个带有以下默认值的对象或字符串：

```js
const defaults = {
  flags: 'r',
  encoding: null,
  fd: null,
  mode: 0o666,
  autoClose: true
};
```

`options` 可以包括 `start` 和 `end` 值，使其可以从文件读取一定范围的字节而不是整个文件。
`start` 和 `end` 都是包括在内的，并且起始值是 0。
如果指定了 `fd` 且 `start` 不传或为 `undefined`，则 `fs.createReadStream()` 从当前文件位置按顺序地读取。
`encoding` 可以是任何可以被 [`Buffer`] 接受的值。

如果指定了 `fd`，则 `ReadStream` 会忽略 `path` 参数并且会使用指定的文件描述符。
这意味着不会触发 `'open'` 事件。
注意，`fd` 应该是阻塞的；非阻塞的 `fd` 们应该传给 [`net.Socket`]。

如果 `autoClose` 为 `false`，则文件描述符不会被关闭，即使有错误。
应用程序需要负责关闭它，并且确保没有文件描述符泄漏。
如果 `autoClose` 被设置为 `true`（默认），则在 `error` 或 `end` 时，文件描述符会被自动关闭。

`mode` 用于设置文件模式（权限和粘结位），但仅限创建文件时。

例子，从一个 100 字节长的文件中读取最后 10 个字节：

```js
fs.createReadStream('sample.txt', { start: 90, end: 99 });
```

如果 `options` 是一个字符串，则它指定了字符编码。

