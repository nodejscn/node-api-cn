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
  * `persistent` {boolean} 如果文件已正在监视，是否继续运行进程。默认为 `true`。
  * `recursive` {boolean} 是否监视全部子目录。适用于监视目录，且只在支持的平台有效（参见[注意事项][Caveats]）。默认为 `false`。
  * `encoding` {string} `filename` 的字符编码。默认为 `'utf8'`。
* `listener` {Function|undefined} 默认为 `undefined`。
  * `eventType` {string}
  * `filename` {string|Buffer}
* 返回: {fs.FSWatcher}

监视 `filename` 的变化，`filename` 可以是文件或目录。

如果 `options` 是一个字符串，则指定字符编码。

`listener` 有两个参数 `(eventType, filename)`。
`eventType` 可能是 `'rename'` 或 `'change'`，`filename` 是触发事件的文件名。

在大多数平台上，当目录中有文件出现或消失时，会触发 `'rename'` 事件。

`listener` 绑定在由 [`fs.FSWatcher`] 触发的 `'change'` 事件上。

