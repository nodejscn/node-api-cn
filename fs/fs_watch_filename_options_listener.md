<!-- YAML
added: v0.5.10
changes:
  - version: v7.6.0
    pr-url: https://github.com/nodejs/node/pull/10739
    description: The `filename` parameter can be a WHATWG `URL` object using
                 `file:` protocol. Support is currently still *experimental*.
  - version: v7.0.0
    pr-url: https://github.com/nodejs/node/pull/7831
    description: The passed `options` object will never be modified.
-->

* `filename` {string|Buffer|URL}
* `options` {string|Object}
  * `persistent` {boolean} 指示如果文件已正被监视，进程是否应继续运行。**默认值:** `true`。
  * `recursive` {boolean} 指示应该监视所有子目录，还是仅监视当前目录。这适用于监视目录时，并且仅适用于受支持的平台（参阅[注意事项][Caveats]）。**默认值:** `false`。
  * `encoding` {string} 指定用于传给监听器的文件名的字符编码。**默认值:** `'utf8'`。
* `listener` {Function|undefined} **默认值:** `undefined`。
  * `eventType` {string}
  * `filename` {string|Buffer}
* 返回: {fs.FSWatcher}

监视 `filename` 的更改，其中 `filename` 是文件或目录。

第二个参数是可选的。
如果 `options` 传入字符串，则它指定 `encoding`。
否则，`options` 应传入对象。

监听器回调有两个参数 `(eventType, filename)`。
`eventType` 是 `'rename'` 或 `'change'`，`filename` 是触发事件的文件的名称。

在大多数平台上，每当文件名在目录中出现或消失时，就会触发 `'rename'` 事件。

监听器回调绑定在由 [`fs.FSWatcher`] 触发的 `'change'` 事件上，但它与 `eventType` 的 `'change'` 值不是一回事。

