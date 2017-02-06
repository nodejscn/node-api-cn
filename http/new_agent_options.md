<!-- YAML
added: v0.3.4
-->

* `options` {Object} 用于设置代理的配置选项的集合。可以有以下字段：
  * `keepAlive` {Boolean} 保持池周围的 socket 在未来可被其他请求使用。默认 = `false`。
  * `keepAliveMsecs` {Integer} 当使用 HTTP 的 KeepAlive 时，多久发送 TCP KeepAlive 数据包使得 socket 保持活跃。
    默认 = `1000`。
    仅当 `keepAlive` 被设为 `true` 有效。
  * `maxSockets` {Number} 每个主机允许的最大 socket 数。默认= `Infinity`。
  * `maxFreeSockets` {Number} 在空闲状态下允许打开的最大 socket 数。
    仅当 `keepAlive` 被设为 `true` 有效。
    默认 = `256`.

[`http.request()`] 使用的默认的 [`http.globalAgent`] 会将所有这些值设为各自的默认值。

要配置其中任何一个，必须创建自己的 [`http.Agent`] 对象。

```js
const http = require('http');
var keepAliveAgent = new http.Agent({ keepAlive: true });
options.agent = keepAliveAgent;
http.request(options, onResponseCallback);
```

