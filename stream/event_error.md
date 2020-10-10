<!-- YAML
added: v0.9.4
-->

* {Error}

如果在写入或管道数据时发生错误，则会触发 `'error'` 事件。 
当调用时，监听器回调会传入一个 `Error` 参数。

除非在创建流时将 [`autoDestroy`][writable-new] 选项设置为 `false`，否则在触发 `'error'` 事件时流会被关闭。

在 `'error'` 之后，除 `'close'` 事件外，不应再触发其他事件（包括 `'error'` 事件）。


