<!-- YAML
added: v0.1.8
-->

* `path` {String | Buffer}
* `mode` {Integer}
* `callback` {Function}

异步的 mkdir(2)。
完成回调只有一个可能的异常参数。
`mode` 默认为 `0o777`。

