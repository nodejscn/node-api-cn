<!-- YAML
added: v0.9.4
-->

* {Error}

如果在写入或管道数据时发生错误，则会触发 `'error'` 事件。 
当调用时，监听器回调会传入一个 `Error` 参数。

除非在创建流时将 [`autoDestroy`][writable-new] 选项设置为 `true`，否则在触发 `'error'` 事件时不会关闭流。

