<!-- YAML
added: v0.7.7
changes:
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28674
    description: The stream's write() callback and return value are exposed.
-->

* `stream` {stream.Writable}
* `dir` {number}
  * `-1`: 从光标向左。
  * `1`: 从光标向右
  * `0`: 整行。
* `callback` {Function} 操作完成后调用。
* 返回: {boolean} 如果 `stream` 希望调用的代码在继续写入附加的数据之前等待 `'drain'` 事件触发，则为 `false`，否则为 `true`。
  
`readline.clearLine()` 方法在由 `dir` 标识的指定方向上清除给定的 [TTY] 流的当前行。

