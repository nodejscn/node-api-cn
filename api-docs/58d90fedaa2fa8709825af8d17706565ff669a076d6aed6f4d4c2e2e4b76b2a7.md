<!-- YAML
added: v0.11.2
-->

默认情况下，每个事件可以注册最多 `10` 个监听器。
可以使用 [`emitter.setMaxListeners(n)`] 方法改变单个 `EventEmitter` 实例的限制。
可以使用 `EventEmitter.defaultMaxListeners` 属性改变所有 `EventEmitter` 实例的默认值。

设置 `EventEmitter.defaultMaxListeners` 要谨慎，因为会影响所有 `EventEmitter` 实例，包括之前创建的。
因而，优先使用 [`emitter.setMaxListeners(n)`] 而不是 `EventEmitter.defaultMaxListeners`。

限制不是硬性的。
`EventEmitter` 实例可以添加超过限制的监听器，但会向 `stderr` 输出跟踪警告，表明检测到可能的内存泄漏。
对于单个 `EventEmitter` 实例，可以使用 `emitter.getMaxListeners()` 和 `emitter.setMaxListeners()` 暂时地消除警告：


```js
emitter.setMaxListeners(emitter.getMaxListeners() + 1);
emitter.once('event', () => {
  // 做些操作
  emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
});
```

[`--trace-warnings`] 命令行标志可用于显示此类警告的堆栈跟踪。

触发的警告可以通过 [`process.on('warning')`] 进行检查，并具有附加的 `emitter`、`type` 和 `count` 属性，分别指向事件触发器实例、事件名称、以及附加的监听器数量。 
其 `name` 属性设置为 `'MaxListenersExceededWarning'`。

