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
  * `persistent` {boolean} 指明如果文件正在被监视，进程是否继续运行。默认为 `true`。
  * `recursive` {boolean} 指明是监视全部子目录还是只有当前目录。
    适用于监视目录时，且只在支持的平台有效（详见[注意事项][Caveats]）。
    默认为 `false`。
  * `encoding` {string} 指定用于传给监听器的文件名的字符编码。默认为 `'utf8'`。
* `listener` {Function|undefined} 默认为 `undefined`。
  * `eventType` {string}
  * `filename` {string|Buffer}
* 返回: {fs.FSWatcher}

监视 `filename` 的变化，`filename` 可以是一个文件或一个目录。

如果提供的 `options` 是一个字符串，则它指定了 `encoding`。
否则 `options` 应该传入一个对象。

监听器回调有两个参数 `(eventType, filename)`。
`eventType` 可能是 `'rename'` 或 `'change'`，`filename` 是触发事件的文件的名称。

在大多数平台，当目录中一个文件出现或消失时，就会触发 `'rename'` 事件。

监听器回调是绑定在由 [`fs.FSWatcher`] 触发的 `'change'` 事件上，但它跟 `eventType` 的 `'change'` 不是同一个东西。

