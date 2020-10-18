<!-- YAML
added: v0.1.13
changes:
  - version:
     - v13.8.0
     - v12.15.0
     - v10.19.0
    pr-url: https://github.com/nodejs/node/pull/31448
    description: 支持 `insecureHTTPParser` 选项。
  - version: v13.3.0
    pr-url: https://github.com/nodejs/node/pull/30570
    description: 支持 `maxHeaderSize` 选项。
  - version:
    - v9.6.0
    - v8.12.0
    pr-url: https://github.com/nodejs/node/pull/15752
    description: 支持 `options` 参数。
-->

* `options` {Object}
  * `IncomingMessage` {http.IncomingMessage} 指定要使用的 `IncomingMessage` 类。
    对于扩展原始的 `IncomingMessage` 很有用。
    **默认值:** `IncomingMessage`。
  * `ServerResponse` {http.ServerResponse} 指定要使用的 `ServerResponse` 类。
    对于扩展原始的 `ServerResponse` 很有用。
    **默认值:** `ServerResponse`。
  * `insecureHTTPParser` {boolean} 使用不安全的 HTTP 解析器，当为 `true` 时可以接受无效的 HTTP 请求头。
    应避免使用不安全的解析器。
    详见 [`--insecure-http-parser`]。
    **默认值:** `false`。
  * `maxHeaderSize` {number} 可选地重写 [`--max-http-header-size`]（用于服务器接收的请求）的值，即请求头的最大长度（以字节为单位）。 
    **默认值:** 16384（16KB）。
* `requestListener` {Function}
* 返回: {http.Server}

返回新的 [`http.Server`] 实例。

`requestListener` 是一个函数，会被自动添加到 [`'request'`] 事件。


