<!-- YAML
added: v0.3.5
-->
- `n` {integer}

默认情况下，如果为特定事件添加了超过 `10` 个监听器，则 `EventEmitter` 会打印一个警告。
此限制有助于寻找内存泄露。
但是，并不是所有的事件都要被限为 `10` 个。
`emitter.setMaxListeners()` 方法允许修改指定的 `EventEmitter` 实例的限制。
值设为 `Infinity`（或 `0`）表明不限制监听器的数量。

返回一个 `EventEmitter` 引用，可以链式调用。

