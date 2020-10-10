<!-- YAML
added: v0.9.12
changes:
  - version: v13.0.0
    pr-url: https://github.com/nodejs/node/pull/27558
    description: The default timeout changed from 120s to 0 (no timeout).
-->

* {number} 超时时间（以毫秒为单位）。**默认值:** `120000`（2 分钟）。

认定套接字超时的不活动毫秒数。

值为 `0` 将禁用传入连接的超时行为。

套接字超时逻辑在连接时设置，因此更改此值仅影响到服务器的新连接，而不影响任何现有连接。


