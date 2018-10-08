<!-- YAML
added: v0.1.26
-->
* `eventName` {string|symbol}
- `...args` {any}
* 返回: {boolean}

按照监听器注册的顺序，同步地调用每个注册到名为 `eventName` 的事件的监听器，并传入提供的参数。

如果事件有监听器，则返回 `true`，否则返回 `false`。

