<!-- YAML
added: v0.11.2
-->

每个事件默认可以注册最多 10 个监听器。
单个 `EventEmitter` 实例的限制可以使用 [`emitter.setMaxListeners(n)`] 方法改变。
所有 `EventEmitter` 实例的默认值可以使用 `EventEmitter.defaultMaxListeners` 属性改变。
如果这个值不是正数, 那将抛出 `TypeError`错误.

设置 `EventEmitter.defaultMaxListeners` 要谨慎，因为会影响所有 `EventEmitter` 实例，包括之前创建的。
因而，调用 [`emitter.setMaxListeners(n)`] 优先于 `EventEmitter.defaultMaxListeners`。

注意，这不是一个硬性限制。
`EventEmitter` 实例允许添加更多的监听器，但会向 `stderr` 输出跟踪警告，表明检测到一个可能的 EventEmitter 内存泄漏。
对于任何单个 `EventEmitter` 实例，`emitter.getMaxListeners()` 和 `emitter.setMaxListeners()` 方法可用于暂时地消除此警告：


```js
emitter.setMaxListeners(emitter.getMaxListeners() + 1);
emitter.once('event', () => {
  // 做些操作
  emitter.setMaxListeners(Math.max(emitter.getMaxListeners() - 1, 0));
});
```

[`--trace-warnings`] 命令行标志可用于显示此类警告的堆栈跟踪。

触发的警告可以使用 [`process.on('warning')`] 检查，还有额外的 `emitter`、`type` 和 `count` 属性，分别代表事件触发器实例的引用、事件的名称、和附加的监听器的数量。
Its `name` property is set to `'MaxListenersExceededWarning'`.

