<!-- YAML
added: v0.1.13
changes:
  - version: v9.6.0
    pr-url: https://github.com/nodejs/node/pull/15752
    description: The `options` argument is supported now.
-->
* `options` {Object}
  * `IncomingMessage` {http.IncomingMessage} 指定要使用的 `IncomingMessage` 类。
     用于拓展原始的 `IncomingMessage` 类。
     默认为 `IncomingMessage`。
  * `ServerResponse` {http.ServerResponse} 指定要使用的 `ServerResponse` 类。
     用于拓展原始的 `ServerResponse` 类。
     默认为 `ServerResponse`。
* `requestListener` {Function}
* 返回: {http.Server}

返回一个新建的 [`http.Server`] 实例。

`requestListener` 是一个函数，会被自动添加到 [`'request'`] 事件。


