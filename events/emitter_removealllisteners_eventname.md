<!-- YAML
added: v0.1.26
-->
* `eventName` {string|symbol}
* 返回: {EventEmitter}

移除全部监听器或指定的 `eventName` 事件的监听器。

注意，删除代码中其他位置添加的监听器是不好的做法，尤其是当 `EventEmitter` 实例是由某些其他组件或模块（例如套接字或文件流）创建时。

返回对 `EventEmitter` 的引用，以便可以链式调用。


