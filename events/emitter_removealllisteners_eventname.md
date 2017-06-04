<!-- YAML
added: v0.1.26
-->
- `eventName` {any}

移除全部或指定 `eventName` 的监听器。

注意，在代码中移除其他地方添加的监听器是一个不好的做法，尤其是当 `EventEmitter` 实例是其他组件或模块（如 socket 或文件流）创建的。

返回一个 `EventEmitter` 引用，可以链式调用。

