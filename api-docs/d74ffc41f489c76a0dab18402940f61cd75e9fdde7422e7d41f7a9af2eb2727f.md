<!-- YAML
added: v0.1.90
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18780
    description: This method now returns a reference to `ServerResponse`.
-->

* `data` {string|Buffer}
* `encoding` {string}
* `callback` {Function}
* 返回: {this}

此方法向服务器发出信号，表明已发送所有响应头和主体，该服务器应该视为此消息已完成。 
必须在每个响应上调用此 `response.end()` 方法。

如果指定了 `data`，则相当于调用 [`response.write(data, encoding)`] 之后再调用 `response.end(callback)`。

如果指定了 `callback`，则当响应流完成时将调用它。

