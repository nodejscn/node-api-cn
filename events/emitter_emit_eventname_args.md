<!-- YAML
added: v0.1.26
-->
- `eventName` {any}
- `...args` {any}

按监听器的注册顺序，同步地调用每个注册到名为 `eventName` 事件的监听器，并传入提供的参数。

如果事件有监听器，则返回 `true` ，否则返回 `false`。

