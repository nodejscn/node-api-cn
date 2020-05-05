<!-- YAML
added: v12.12.0
-->

* `callback` {Function}
  * `err` {Error}

异步地关闭目录的底层资源句柄。 
后续的读取会导致错误。

关闭资源句柄之后将会调用 `callback`。

