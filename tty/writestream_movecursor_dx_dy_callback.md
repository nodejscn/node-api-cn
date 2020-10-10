<!-- YAML
added: v0.7.7
changes:
  - version: v12.7.0
    pr-url: https://github.com/nodejs/node/pull/28721
    description: 流的 write() 回调和返回值会被导出。
-->

* `dx` {number}
* `dy` {number}
* `callback` {Function} 当操作完成时调用。
* 返回: {boolean} 如果流期望调用的代码在继续写入其他数据之前等待 `'drain'` 事件触发，则为 `false`，否则为 `true`。

`writeStream.moveCursor()` 会将 `WriteStream` 的光标相对于其当前的位置移动。

