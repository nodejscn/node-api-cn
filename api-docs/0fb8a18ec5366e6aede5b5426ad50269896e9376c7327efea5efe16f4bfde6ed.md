<!-- YAML
added: v0.1.90
changes:
  - version: v10.0.0
    pr-url: https://github.com/nodejs/node/pull/18780
    description: This method now returns a reference to `ClientRequest`.
-->

* `data` {string|Buffer}
* `encoding` {string}
* `callback` {Function}
* 返回: {this}

完成发送请求。 
如果部分请求主体还未发送，则将它们刷新到流中。
如果请求被分块，则发送终止符 `'0\r\n\r\n'`。

如果指定了 `data`，则相当于调用 [`request.write(data, encoding)`] 之后再调用 `request.end(callback)`。

如果指定了 `callback`，则当请求流完成时将调用它。


