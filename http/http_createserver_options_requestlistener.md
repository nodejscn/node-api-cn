<!-- YAML
added: v0.1.13
changes:
  - version: v9.6.0
    pr-url: https://github.com/nodejs/node/pull/15752
    description: The `options` argument is supported now.
-->
* {Object}
  * `IncomingMessage` {http.IncomingMessage} 指定要使用的 `IncomingMessage`
    类，用于拓展原始的`IncomingMessage`类.
    **缺省:** `IncomingMessage`.
  * `ServerResponse` {http.ServerResponse} 指定要使用的 `ServerResponse`类，
 用于拓展原始的`ServerResponse`类. **缺省:**
    `ServerResponse`.
- `requestListener` {Function}

* 返回: {http.Server}

返回一个新的 [`http.Server`]实例。

 `requestListener`是一个自动添加到[`'request'`][]事件的方法。

