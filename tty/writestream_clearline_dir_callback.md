<!-- YAML
added: v0.7.7
changes:
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28721
    description: The stream's write() callback and return value are exposed.
-->

* `dir` {number}
  * `-1` - 从光标向左。
  * `1` - 从光标向右。
  * `0` - 整行。
* `callback` {Function} 操作完成后调用。
* 返回: {boolean} 如果流希望调用的代码在继续写入附加的数据之前等待 `'drain'` 事件触发，则为 `false`，否则为 `true`。

`writeStream.clearLine()` 在 `dir` 标识的方向上清除此 `WriteStream` 的当前行。

