<!-- YAML
added: v0.3.4
-->

* `options` {Object} 代理的配置选项。有以下字段：
  * `keepAlive` {boolean} 保持 socket 可用即使没有请求，以便它们可被将来的请求使用而无需重新建立一个 TCP 连接。默认为 `false`。
  * `keepAliveMsecs` {number} 当使用了 `keepAlive` 选项时，该选项指定 TCP `Keep-Alive` 数据包的 [初始延迟]。
    当 `keepAlive` 选项为 `false` 或 `undefined` 时，该选项无效。
    默认为 `1000`。
  * `maxSockets` {number} 每个主机允许的最大 socket 数量。
    默认为 `Infinity`。
  * `maxFreeSockets` {number} 在空闲状态下允许打开的最大 socket 数量。
    仅当 `keepAlive` 为 `true` 时才有效。
    默认为 `256`。

[`http.request()`] 使用的默认 [`http.globalAgent`] 的选项均为各自的默认值。

若要配置其中任何一个，则需要创建自定义的 [`http.Agent`] 实例。

```js
const http = require('http');
const keepAliveAgent = new http.Agent({ keepAlive: true });
options.agent = keepAliveAgent;
http.request(options, onResponseCallback);
```

