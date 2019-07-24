<!-- YAML
added: v0.3.4
-->

* `options` {Object} 要在代理上设置的可配置选项集。可以包含以下字段： 
  * `keepAlive` {boolean} 即使没有未完成的请求，也要保持套接字，这样它们就可以被用于将来的请求而无需重新建立 TCP 连接。**默认值:** `false`。
  * `keepAliveMsecs` {number} 当使用 `keepAlive` 选项时，指定用于 TCP Keep-Alive 数据包的[初始延迟][initial delay]。当 `keepAlive` 选项为 `false` 或 `undefined` 时则忽略。**默认值:** `1000`。
  * `maxSockets` {number} 每个主机允许的套接字的最大数量。**默认值:** `Infinity`。
  * `maxFreeSockets` {number} 在空闲状态下保持打开的套接字的最大数量。仅当 `keepAlive` 被设置为 `true` 时才相关。**默认值:** `256`。
  * `timeout` {number} 套接字的超时时间，以毫秒为单位。这会在套接字被连接之后设置超时时间。

[`socket.connect()`] 中的 `options` 也受支持。
 
被 [`http.request()`] 使用的默认的 [`http.globalAgent`] 具有所有这些值且被设置为各自的默认值。

要配置其中任何一个，则必须创建自定义的 [`http.Agent`] 实例。

```js
const http = require('http');
const keepAliveAgent = new http.Agent({ keepAlive: true });
options.agent = keepAliveAgent;
http.request(options, onResponseCallback);
```

