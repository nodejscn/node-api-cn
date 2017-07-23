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
  * `persistent` {boolean} 指明如果文件正在被监视，进程是否应该继续运行。默认 = `true`
  * `recursive` {boolean} 指明是否全部子目录应该被监视，或只是当前目录。
    适用于当一个目录被指定时，且只在支持的平台（详见 [Caveats]）。默认 = `false`
  * `encoding` {string} 指定用于传给监听器的文件名的字符编码。默认 = `'utf8'`
* `listener` {Function|undefined} **Default:** `undefined`

监视 `filename` 的变化，`filename` 可以是一个文件或一个目录。
返回的对象是一个 [`fs.FSWatcher`]。

第二个参数是可选的。
如果提供的 `options` 是一个字符串，则它指定了 `encoding`。
否则 `options` 应该以一个对象传入。

监听器回调有两个参数 `(eventType, filename)`。
`eventType` 可以是 `'rename'` 或 `'change'`，`filename` 是触发事件的文件的名称。

注意，在大多数平台，当一个文件出现或消失在一个目录里时，`'rename'` 会被触发。

还需要注意，监听器回调是绑定在由 [`fs.FSWatcher`] 触发的 `'change'` 事件上，但它跟 `eventType` 的 `'change'` 值不是同一个东西。

