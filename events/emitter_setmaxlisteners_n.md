<!-- YAML
added: v0.3.5
-->
* `n` {integer}
* 返回: {EventEmitter}

默认情况下，如果为特定事件添加了超过 `10` 个监听器，则 `EventEmitter` 会打印一个警告。
这有助于发现内存泄露。
但是，并不是所有的事件都要限制 `10` 个监听器。
`emitter.setMaxListeners()` 方法可以为指定的 `EventEmitter` 实例修改限制。
值设为 `Infinity`（或 `0`）表示不限制监听器的数量。

返回对 `EventEmitter` 的引用，以便可以链式调用。

